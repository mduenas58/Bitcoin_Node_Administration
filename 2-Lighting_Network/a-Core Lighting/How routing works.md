Sep 27, 2026 · @Manuel Duenas

A routing node earns by forwarding payments others originate, and its profitability is decided almost entirely by two operator choices: where liquidity sits, and what it costs to use. This document covers the routing mechanism at the protocol level, how to set fee policies that actually produce revenue, and how to use submarine swaps to move liquidity without closing channels.

## How routing works

A Lightning payment is source-routed: the sender computes the entire path before sending, and each intermediate node learns only who handed it the payment and who to hand it to next.

![[Screenshot 2026-09-27 at 9.22.27 PM.png]]

Bob and Carol each keep the difference between what they receive and what they forward. Neither learns that Alice originated the payment or that Dave is its destination.

### What routing nodes actually know

Gossip distributes three message types: channel_announcement (a channel exists, proven by its on-chain funding output), channel_update (fee policy, CLTV delta and HTLC limits, one per direction) and node_announcement (addresses and feature bits).

Gossip publishes channel **capacity** but never **balance**. A 10M sat channel may hold 9.9M on one side. The sender cannot know, so pathfinding is probabilistic rather than deterministic. This single fact drives most of Lightning's routing behaviour.

### Pathfinding

The sender runs a shortest-path search over its local graph view, working backwards from the destination. Edges are weighted by a cost function combining the hop's fee, its CLTV delta (locked capital has a time cost) and an estimated probability of success.

LND calls its probability layer _mission control_. Every attempt updates a belief about how much a given channel can forward; a failure proves that channel held less than the attempted amount at that moment, and the estimate decays back toward optimism over the following hours.

### Onion construction

The sender wraps the routing instructions in a Sphinx onion, one encryption layer per hop. Each hop decrypts exactly one layer, learning the amount to forward, the outgoing CLTV and the next channel, then re-pads the packet to its original fixed length before passing it on.

Fixed size is the privacy property: because the packet never shrinks, a hop cannot infer its position in the route from what it holds.

### The HTLC chain

The receiver generates a random preimage and puts its hash in the invoice. Each hop then offers the next an HTLC conditional on revealing that preimage before a block-height deadline.

Amounts decrease along the route because each hop keeps its fee. Expiries decrease too, because each hop needs a safety margin to claim on-chain if the next one goes silent. Alice's HTLC to Bob therefore carries the longest timeout in the route.

### Settlement and failure

When the receiver reveals the preimage to claim its HTLC, the secret propagates backwards and each hop claims from its predecessor. The chain is atomic: either every hop settles or none does.

A failed payment returns an onion-encrypted error from the failing hop. The sender learns where it failed and why, updates its estimates, and retries. Large payments are usually split across several routes under one payment hash (MPP) so the parts settle together.

## The fee parameters

Seven values in channel_update define what a hop charges and what it will accept. They are set **per direction**: your policy on a channel governs payments leaving through it, spending your local balance.

   
|Parameter|Unit|What it controls|Common range|
|---|---|---|---|
|fee_base_msat|msat|Flat charge per forward, regardless of size|0 to 1,000|
|fee_proportional_millionths|ppm|Charge per million units forwarded|1 to 2,500|
|cltv_expiry_delta|blocks|Timelock margin this hop demands|40 to 144|
|htlc_minimum_msat|msat|Smallest forward accepted|1,000|
|htlc_maximum_msat|msat|Largest forward accepted|at or below local balance|
|max_htlc_value_in_flight_msat|msat|Cap on total pending HTLC value|set at channel open|
|max_accepted_htlcs|count|Concurrent pending HTLCs; protocol ceiling is 483|483|

  
  

The fee for a single forward:

![[Screenshot 2026-09-27 at 9.25.17 PM.png]]

Bob in the diagram above charges 1,000 msat base and 100 ppm. Forwarding 100,006 sat he earns 1,000 + 10,000 = 11,000 msat, or 11 sat. Carol charges the same base at 50 ppm and earns 6 sat on 100,000.

### Why base fee and ppm behave differently

Base fee dominates small payments and is invisible on large ones. At 1,000 msat base, a 1,000 sat forward pays 100 ppm-equivalent purely in base fee; a 1,000,000 sat forward pays 1 ppm-equivalent. A high base fee is therefore a filter against small payments, not a revenue source.

Most profitable routing nodes run a **base fee of 0** and express everything in ppm. Pathfinding algorithms penalise base fee heavily when evaluating small amounts, so a non-zero base can remove you from consideration entirely on the payments that flow most often.

### CLTV delta is a real cost

A larger cltv_expiry_delta is safer for you in a force-close race but makes your hop more expensive in the sender's cost function, because capital is locked longer if the payment stalls. It also raises the total route timelock, and routes exceeding the sender's maximum are discarded. 40 blocks is the common default; 144 is defensive and will cost you traffic.

### Inbound fees

Recent LND and Core Lightning releases support **inbound fees**, charged or discounted on the channel a payment arrives through rather than the one it leaves by. A negative inbound fee is a discount that makes it cheaper for others to route _into_ you through a specific channel, which is a direct tool for pulling liquidity back toward a depleted side without paying for a rebalance. Support across implementations and pathfinders is uneven, so treat it as an optimisation rather than a foundation.

### Propagation

A channel_update takes time to spread across the network, and peers rate-limit nodes that publish updates too often. A node rewriting its fees every few minutes will have senders routing against stale policy, producing failures that damage its reputation in their pathfinding. Batch policy changes and apply them on the order of hours, not minutes.

## Routing economics

Most routing nodes lose money. They earn a few thousand sats a month on capital that cost on-chain fees to deploy, and they spend more than that rebalancing. Understanding why is the difference between a node that pays for itself and an expensive hobby.

### The equation

Routing revenue is not a function of capacity. It is a function of how many times that capacity turns over:

![[Screenshot 2026-09-27 at 9.26.37 PM.png]]

A node whose capital forwards its own value twice a month at an average 500 ppm returns 1.2% annually, gross. At one turn a month and 200 ppm it returns 0.24%, which will not cover the on-chain cost of having opened the channels.

This is why capacity alone is a vanity metric. Ten million sats sitting in a channel that forwards nothing earns exactly nothing, and ties up capital that could have been deployed elsewhere.

### What you are actually paid for

You are not paid for having liquidity. You are paid for having liquidity **in the direction the payment is going, at the moment it arrives, at a price the sender will accept**. Three conditions, all of which must hold simultaneously.

  
|Variable|The question|How to influence it|
|---|---|---|
|Position|Are you on a path between places money actually moves?|Peer selection: connect toward the flow, not toward famous nodes|
|Balance|Is liquidity on the correct side when the payment arrives?|Rebalancing, fee-driven flow steering, inbound fees|
|Price|Is your ppm competitive with the alternatives?|Fee policy, adjusted per channel|

  
  

Position is decided when you open the channel and is expensive to change. Most operators get it wrong by connecting to large, well-known nodes, which puts them in the most competitive part of the graph where fees are driven toward zero. The money is in being the cheap bridge between two regions that are otherwise poorly connected.

### The full cost stack

Gross forwarding revenue is not profit. Subtract:

- **Rebalancing cost.** Every circular rebalance pays other nodes' fees. If you spend 300 ppm to reposition liquidity you then sell at 400 ppm, your real margin is 100 ppm.
    
- **On-chain cost.** Opening and closing each channel costs a transaction. A force-close costs considerably more, and sweeping the resulting HTLC outputs costs more again.
    
- **Opportunity cost of capital.** Bitcoin locked in channels is bitcoin not doing anything else, and it carries the price risk of the asset regardless.
    
- **Your time.** A node run seriously needs monitoring, fee adjustment and periodic intervention.
    

The practical consequence: a routing node becomes worth operating somewhere in the range of tens of millions of sats deployed, with deliberate peer selection, and it competes on being _reliably_ available in a direction rather than on being cheap.

## Setting fee policies

A fee is a price signal, not just a revenue setting. Raising the fee on a channel slows the rate at which it drains; lowering it invites traffic to drain it faster. Once you see fees as flow control, the policy follows from the state of each channel.

### The governing rule

**Your outbound fee must exceed what it costs you to refill that channel.** If repositioning liquidity into a channel costs 300 ppm in rebalancing fees, selling that liquidity at 200 ppm is a loss you are paying to provide. This single rule eliminates most unprofitable fee policies.

### Four approaches

   
|Approach|Mechanism|Suits|Weakness|
|---|---|---|---|
|Flat low, 0 to 50 ppm|One cheap rate everywhere|Bootstrapping a new node, earning routing history|Channels drain one way and stay drained; no margin to fund refills|
|Tiered static|A fixed rate per peer class, reviewed monthly|Small nodes, minimal maintenance|Ignores current balance; goes stale as the graph shifts|
|Balance-responsive|Fee is a function of the local balance ratio|Most serious routing nodes|Needs automation; can oscillate if the curve is too steep|
|Demand-responsive|Raise until forwards stop, then ease back|Mature nodes with enough volume to read a signal|Slow to converge; needs consistent traffic to produce data|

  
  

In practice the durable answer is balance-responsive as the base, with demand-responsive adjustment layered on top for your highest-volume channels.

### A concrete balance ladder

A workable starting policy, with your own baseline rate substituted for the middle band:

  
|Local balance|Fee|Intent|
|---|---|---|
|Above 90%|0 to 50 ppm|Nearly full; invite traffic to drain it|
|75 to 90%|100 ppm|Cheap, encourage outflow|
|25 to 75%|Your baseline, 300 to 600 ppm|The productive band; this is where you earn|
|10 to 25%|1,000 ppm|Scarce; only worth selling at a premium|
|Below 10%|2,500 ppm or higher|Effectively reserved; price out casual traffic|

  
  

The bands matter more than the numbers. The numbers are found by experiment on your own channels.

### Directional asymmetry

Channels are rarely symmetric, and you should not price them as though they were.

A **sink** is a peer that consistently pulls liquidity from you: an exchange taking deposits, a large custodial wallet. Price the outbound side high. You are selling a scarce resource and the flow will come anyway.

A **source** is a peer that consistently pushes liquidity to you. Its outbound side should be cheap, because you want that liquidity to move on through you rather than accumulate. A negative inbound fee on that channel, where supported, makes it cheaper still for senders to enter through it.

A channel that has only ever forwarded in one direction is not a routing channel. It is a one-time payment path that you are continuing to pay to maintain.

### htlc_maximum_msat as a soft brake

When a channel is nearly drained, lowering htlc_maximum_msat below your remaining local balance stops large forwards without publishing an absurd fee. Senders route around the size limit rather than around your price, so your fee policy stays legible and your reputation in their pathfinding is not damaged by a wall of failures.

### Tooling

**charge-lnd** applies declarative rules from a config file and is the standard for policy-as-code. **LNDg** adds a web interface with automated fee adjustment and rebalancing. **balanceofsatoshis** (bos) is the swiss-army CLI for one-off analysis and rebalancing. Core Lightning has the **feeadjuster** plugin. **Torq** offers a commercial dashboard with automation.

Whichever you use, change fees on the order of hours. Rapid churn produces stale policy in senders' graphs and failures that count against you.

## Why channels drain

A channel's total capacity is fixed at open and can only be changed on-chain. What moves is the split between your side and your peer's. Every forward shifts that split, and nothing inside the Lightning protocol ever shifts it back.

### Local and remote

Your **local balance** is your outbound capacity: what you can send or forward through that channel. Your peer's balance is your **inbound capacity**: what you can receive through it. The two always sum to the channel capacity, less two deductions.

The **channel reserve**, typically 1% per side, is permanently unspendable while the channel is open. It exists so each party always has something to lose if they try to cheat. Pending HTLCs also reduce what is available until they resolve, and on a busy channel there can be dozens in flight at once.

### Flow in the network is not symmetric

Payments in Lightning move in structural directions. Consumers pay merchants. Individuals deposit to exchanges more often than they withdraw. Wallet providers push funds out to users. These are not random walks that average out.

If you open a channel toward an exchange, your outbound liquidity will flow into it and stay there, because almost nobody is routing payments out of an exchange through your node. The channel is not broken. It is correctly reflecting a one-way flow you chose to sit on.

### Reading your channels

The useful measurement is not the current balance but **net flow over a period**. Forwarding history grouped by channel and direction, over two to four weeks, tells you what kind of channel each one is.

  
|Pattern|Diagnosis|Action|
|---|---|---|
|Drains outbound, never refills|You sit upstream of a sink|Price outbound high; refill only if the margin covers the cost|
|Fills inbound, never empties|You sit downstream of a source|Price outbound cheap to push the liquidity onward|
|Oscillates both directions|A genuine routing channel|Protect it; keep fees in the productive band|
|No movement either way|Dead capital|Close it and redeploy, or find out whether your fee priced you out|

  
  

The fourth row is the most common and the least acted on. A node with twenty channels typically earns nearly all its revenue from three or four of them.

### Balance is not the goal

The instinct to drive every channel toward 50/50 is expensive and usually wrong. A channel pointed at a sink should sit near empty most of the time, because that is where the traffic has put it and refilling it costs real money.

What you actually want is liquidity positioned where the next payment will need it, at a cost lower than the fee you will collect for providing it. Sometimes that means a deliberately lopsided channel. The question to ask of any rebalance is not _is this balanced_ but _will I earn back what this costs_.

## Submarine swaps

A submarine swap trades on-chain bitcoin for Lightning bitcoin atomically, using the same hash-locked primitive that makes routing work. It is the only way to change the **total** amount of liquidity on your side of the network. Rebalancing between your own channels moves sats around; a swap brings them in or takes them out.

![[Pasted image 20260927214259.png]]

### The two directions

**Loop Out**, or reverse submarine swap, is the flow drawn above: you pay over Lightning and receive on-chain. It spends local balance and gives you inbound capacity. Use it when your channels are full on your side and you cannot receive.

**Loop In**, the original submarine swap, runs the other way: you send on-chain and receive over Lightning. It converts cold funds into outbound capacity. Use it when your channels are drained and you cannot forward.

The naming is a persistent source of confusion. Anchor on the Lightning side: _out_ means sats leave your channels, _in_ means sats enter them.

### The hold invoice

The mechanism depends on a **hold invoice** (also called a HODL invoice): an invoice whose preimage the receiver does not know when it issues the invoice. An incoming payment against it locks into an HTLC and stays there, neither settled nor failed, until the receiver either learns the preimage or gives up.

In a Loop Out, your node generates the preimage and gives the provider only its hash. The provider issues a hold invoice against that hash, so your Lightning payment sits locked and unclaimable until the provider learns the secret. The only way it learns the secret is by watching you spend the on-chain HTLC, where the preimage appears in the witness.

### Why it is atomic

Every outcome is safe for both parties:

- You never claim on-chain → the provider never learns P → your Lightning HTLC expires and the funds return to you.
    
- The provider never broadcasts → you never reveal P → same result.
    
- You claim on-chain → P becomes public → the provider settles the Lightning side. Both legs complete.
    

Neither party can take one leg without giving up the other. The timelocks are set so the on-chain refund path always expires after the Lightning path, which prevents a race where you could claim on-chain and still have your Lightning payment refunded.

### Taproot swaps

Current Boltz and Loop implementations use Taproot with MuSig2 for the cooperative path. When both parties behave, the swap settles as a plain key-path spend that is indistinguishable on-chain from an ordinary payment: cheaper in fees and better for privacy. The hashlock script path remains as the fallback for when cooperation fails.

### What can still go wrong

Swaps are non-custodial in the sense that no one can steal your funds, but they are not free of risk:

- **Provider downtime mid-swap.** Your funds are safe but locked until a timelock expires, which can mean hours.
    
- **On-chain fee spikes.** If fees rise sharply between the swap starting and your claim transaction, the claim can become uneconomic relative to the amount swapped. Small swaps are disproportionately exposed.
    
- **Censorship.** A provider can decline to serve you. This is a liveness problem, not a custody one, but it is real.
    
- **Confirmation delay.** The on-chain leg needs confirmations. Plan for a swap to take tens of minutes, not seconds.
    

## Swap providers compared

Three implementations of the same cryptographic primitive, with different operational philosophies. Fees below are service fees only; on-chain miner fees are additional in every case and usually dominate the total.

   
||[Loop](https://www.spark.money/research/lightning-loop-submarine-swaps-guide)|[Boltz](https://boltz.exchange/)|[PeerSwap](https://www.spark.money/research/submarine-swaps-explained)|
|---|---|---|---|
|Operator|Lightning Labs|Boltz|None — direct peer to peer|
|Custody|Non-custodial|Non-custodial|Non-custodial|
|Service fee|Dynamic, from about 0.05%|0.1% to 0.5%, occasionally negative|None|
|Node support|LND|LND, CLN, Eclair|LND, CLN with the plugin|
|Accounts / KYC|Account required|None|None|
|Distinctive|autoloop automation; MuSig2 static deposit addresses|Liquid sidechain swaps|No third party, no service fee|
|Main limitation|LND only|Provider-dependent liveness|Both peers must run it|

  
  

### Loop

The default for LND operators, integrated into Lightning Terminal, Ride the Lightning and ThunderHub. Its fee model is dynamic, starting around 0.05% and scaling with network conditions.

Two developments matter operationally. In February 2025 Lightning Labs integrated MuSig2 to enable static reusable deposit addresses built on 2-of-2 taproot, so you can fund a Loop In address during a low-fee period and execute the swap later. As of March 2026, Loop can open new channels directly from those static address deposits.

autoloop is the feature that makes Loop worth running: it executes swaps automatically against thresholds you define per channel, rather than requiring you to notice an imbalance and act.

### Boltz

Implementation-agnostic, no accounts, no KYC. Service fees run [0.1% to 0.5% and can go negative](https://www.spark.money/tools/bitcoin-lightning-channel-rebalancing-comparison) — a rebate — when Boltz needs to move its own inventory in the direction you are asking for. Checking for a negative-fee direction before swapping is free money often enough to be worth the habit.

The real differentiator is **Liquid**. Because L-BTC transactions are cheap and the fee rate is stable, swapping via Liquid instead of mainchain collapses the dominant cost. Boltz's own worked example: obtaining 100,000 sats of inbound liquidity at 50 sat/vB costs roughly [15,050 sats on mainchain against 527 sats via Liquid](https://blog.boltz.exchange/p/launching-liquid-swaps-unfairly-cheap), because the mainchain swap pays 291 vbytes of miner fees where the Liquid swap pays 3,881 bytes at 0.11 sat/vbyte.

That is a 96% reduction, and it changes the arithmetic of rebalancing entirely. Liquid becomes a holding area: swap out to L-BTC cheaply, hold, swap back into whichever channel needs it, without touching mainchain fees at all. The tradeoff is Liquid's federated security model, which is weaker than Bitcoin's and should be treated as a short-term parking place rather than storage.

Boltz [added USDT swaps via Arbitrum in March 2026](https://www.spark.money/tools/bitcoin-atomic-swap-protocols), which is outside the scope of node liquidity management but signals the direction of the product.

### PeerSwap

The cheapest option and the most constrained. Two node operators who share a channel swap directly with each other: one sends on-chain, the other sends the equivalent over the channel. There is no service fee at all — only miner costs — because there is no intermediary.

The limitation is coordination. Both peers must run the plugin, and one must have on-chain funds available at the time. For operators with established bilateral relationships and a mutual interest in a healthy channel, it is the most cost-efficient method available. For everything else it is unusable, because you cannot make your peer install software.

### One planning note

Channel reserves are not swappable. The 1% held back on each side is unavailable, so your effective swappable balance is always slightly below what your node management interface reports as the channel balance. Size swaps against the usable figure, not the displayed one.

## The rebalancing decision

Most rebalancing destroys value. The operator sees an empty channel, feels the itch, pays 1,200 ppm to refill it, then sells that liquidity at 400 ppm. Repeat monthly and the node is a machine for converting bitcoin into other people's routing fees.

### The break-even condition

![[Screenshot 2026-09-27 at 9.31.22 PM.png]] You earn your outbound rate **once** per unit of repositioned liquidity. So the cost of moving it must sit below what you charge, discounted by the real probability that it gets used at all. On a channel that forwards reliably, that probability approaches 1. On a channel you are refilling out of hope, it is closer to 0.3, and the arithmetic collapses.

### What each method actually costs

Rebalancing 2,000,000 sats, with the on-chain rows priced at the fee rate shown:

    
|Method|Service fee|Chain fee|Total|Cost in ppm|
|---|---|---|---|---|
|Fee steering|0|0|0|**0**|
|Circular rebalance at 250 ppm|500|0|500|**250**|
|PeerSwap at 2 sat/vB|0|~580|~580|**290**|
|PeerSwap at 10 sat/vB|0|~2,910|~2,910|**1,455**|
|Liquid swap, 0.1% service|2,000|~430|~2,430|**1,215**|
|Mainchain swap, 0.5% at 50 sat/vB|10,000|~14,550|~24,550|**12,275**|

  
  

Two things fall out of this table.

First, **mainchain swaps are not a rebalancing tool** at normal routing margins. At 12,275 ppm you would need to charge more than 1.2% outbound to break even on a single turn. Mainchain swaps are for structural moves — taking profit to cold storage, funding a node from scratch — not for routine liquidity maintenance.

Second, the on-chain rows swing by an order of magnitude with the mempool. The same PeerSwap costs 290 ppm at 2 sat/vB and 1,455 ppm at 10. Any rebalancing strategy that ignores the fee environment will be wrong most of the time, which is the argument for Liquid: its fee rate barely moves.

### The decision ladder

Work down this list and stop at the first step that works.

1. **Change the fee policy.** Free, and often sufficient. Raise the outbound rate on the draining channel, drop it on the full one, and let the network reposition your liquidity for you while paying you to do it. If inbound fees are available, a discount on the depleted channel pulls flow toward it directly.
    
2. **Let it sit.** A channel pointed at a structural sink will drain again within days of any refill. The correct action is often to price it high and leave it empty until someone pays a premium for it.
    
3. **Circular rebalance**, if a route exists below your outbound rate. Cheapest active method, and it needs no on-chain transaction. Use bos rebalance, LNDg or rebalance-lnd with a maximum fee rate set explicitly below what you charge.
    
4. **Liquid swap**, when circular rebalancing finds no route or the mempool is busy. Around 1,200 ppm and stable regardless of mainchain conditions.
    
5. **PeerSwap**, if the peer runs it and fees are low. Cheapest of the swaps when both conditions hold.
    
6. **Splice**, if the channel is structurally the wrong size. Modern LND and CLN can resize a channel in place with a single on-chain transaction, avoiding a close-and-reopen and preserving channel age and history.
    
7. **Close it.** If a channel has not forwarded in a month and no fee level changes that, it is dead capital. The on-chain cost of closing is a one-time expense; leaving the capital stranded is a permanent one.
    

### Set a maximum fee rate, always

Every rebalancing tool accepts a ceiling. Set it. A circular rebalance with no cap will happily pay 3,000 ppm to move sats you sell at 500, and the tool will report success while doing it. The cap is the single most important configuration value in any rebalancing setup.

## Operational playbook

### The one report that matters

Most node dashboards show gross forwarding revenue, which flatters you. The number to track is **net margin per channel**: forwarding revenue earned on that channel, minus the rebalancing cost spent refilling it, over the same period.

Run it monthly per channel. The result is usually uncomfortable and always actionable: a handful of channels carry the node, several break even, and one or two are actively losing money while appearing busy.

  
|Metric|Why it matters|Where to get it|
|---|---|---|
|Forwards by channel and direction|Identifies sources, sinks and dead channels|lncli fwdinghistory, LNDg, Torq|
|Revenue per channel|The numerator|Same|
|Rebalance spend per channel|The denominator everyone omits|bos, LNDg attributes this properly|
|Turnover: volume ÷ capital|The real efficiency measure|Computed|
|Failed forwards by reason|insufficient_balance means you were priced right but empty|lncli fwdinghistory, htlc stream|

  
  

That last row is the most underused signal on a Lightning node. A channel failing forwards for insufficient balance is telling you there is demand you could not serve — which is exactly the channel worth refilling, and the only case where paying to rebalance is reliably correct.

### Automation

  
|Layer|Tool|What to set|
|---|---|---|
|Fee policy|charge-lnd, feeadjuster (CLN)|Balance-ladder rules in a config file, applied hourly|
|Rebalancing|bos rebalance, LNDg, rebalance-lnd|A max fee rate below your outbound rate, always|
|Swaps|autoloop, Boltz API|Per-channel thresholds, a fee ceiling, Liquid where available|
|Monitoring|Prometheus + Grafana, Amboss|Alerts, not dashboards|

  
  

Automate fee policy before you automate rebalancing. Fee steering is free and reduces how much rebalancing you need; automating rebalancing first just makes the expensive mistake happen faster.

### Alerts worth having

- Node unreachable or lnd not responding
    
- Chain backend out of sync beyond a few blocks
    
- Any channel force-closing, yours or theirs
    
- Disk below a threshold — a full disk during a channel update is how nodes get corrupted
    
- Rebalance spend exceeding a daily cap
    
- A peer offline beyond some hours, since an offline peer's channel earns nothing and risks a stale-state close
    

### Backups

The static channel backup file (channel.backup in LND) must be copied off the machine every time channel state changes. Automate it.

Understand what it does and does not do: it is **not** a wallet backup that restores your channels to working order. Restoring from an SCB force-closes every channel and asks your peers to pay you out on-chain. It recovers funds, not operations. Restoring a _stale_ backup can lose funds outright, because you may publish a revoked state and be penalised for it. Treat it as a disaster instrument, never as a routine restore path.

### Review cadence

 
|Interval|Task|
|---|---|
|Daily|Glance at alerts only. Resist touching fees.|
|Weekly|Review fee policy against the balance ladder; check rebalance spend against revenue|
|Monthly|Net margin per channel; close the dead ones; review peer selection|
|Quarterly|Capital review: total return on deployed sats against the alternatives|

  
  

The discipline that separates profitable nodes from busy ones is doing less, slower. Fees changed hourly by automation are fine; fees changed hourly by a human chasing a feeling are not.

### Sources and currency

Provider fees, limits and features change frequently. Figures here reflect published rates as of the as-of date in the byline: Boltz service fees and the Liquid cost comparison from [Boltz's own writeup](https://blog.boltz.exchange/p/launching-liquid-swaps-unfairly-cheap), and Loop's pricing and MuSig2 static address timeline from [this rebalancing comparison](https://www.spark.money/tools/bitcoin-lightning-channel-rebalancing-comparison). Verify current rates with each provider before sizing a swap.