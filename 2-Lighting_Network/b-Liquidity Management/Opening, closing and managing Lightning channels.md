# Opening, closing and managing Lightning channels

Sep 30, 2026 · @Manuel Duenas

A channel is a 2-of-2 multisig output on the Bitcoin blockchain plus a pair of continuously updated transactions that neither party has broadcast. Everything in this tutorial follows from that: opening costs an on-chain transaction, closing costs at least one more, and the interesting part is everything in between. Commands are given for LND with Core Lightning equivalents alongside.

## What a channel is, and its lifecycle

A channel is a single on-chain output locked to a 2-of-2 multisig between you and your peer. Both parties hold a **commitment transaction** that spends that output back to each of them in the current proportions. Making a payment means exchanging a new pair of commitment transactions and revoking the old ones.

Nobody broadcasts anything while the channel is open. The blockchain sees exactly two transactions in a healthy channel's entire life: the funding transaction and the closing transaction.

![[Screenshot 2026-10-02 at 2.18.21 PM.png]]

### Why the two exits differ so much

A **cooperative close** is a negotiation. Both nodes agree on a fee, co-sign a single transaction paying each side its current balance, and broadcast it. One transaction, a fee you both agreed, funds spendable on confirmation.

A **force close** is unilateral. You broadcast your latest commitment transaction, which the protocol encumbers with a `to_self_delay` timelock on _your_ output — commonly 144 blocks, around a day — while your peer's output is immediately spendable. The delay exists so that if you broadcast an old, revoked state, your peer has a window to take everything via the penalty path.

So a force close costs you: the commitment transaction, a later sweep transaction, possibly separate HTLC transactions, and a day of your capital being unavailable. Use it when the peer is unreachable or unresponsive, not as a default.

### The channel reserve

Each side must keep roughly 1% of the channel capacity in its own balance at all times, unspendable while the channel is open. It is the stake that makes cheating irrational — a party with nothing to lose has nothing to lose by broadcasting a revoked state.

Practically this means a 1,000,000 sat channel gives you at most about 990,000 sat of usable outbound, and your node will refuse to push the balance below the reserve.

### Anchor outputs

Modern channels are **anchor channels**, now the default. The commitment transaction carries a near-zero fee plus two tiny anchor outputs, one per party, whose only purpose is to let either side fee-bump the commitment with CPFP at the moment it is needed.

This fixes a real problem — older channels baked in a fee rate at signing time, which could be far too low years later — but it introduces an obligation: **you must keep on-chain funds available to bump an anchor.** A node with every satoshi committed into channels cannot force-close safely. LND enforces this with a wallet reserve, covered in the next section.

## Before you open anything

### Confirm the node is actually ready

```markdown
lncli getinfo | jq '{synced_to_chain, synced_to_graph, block_height, num_peers}'
```

Both `synced_to_chain` and `synced_to_graph` must be `true`. Opening a channel while the graph is still syncing works, but your node will not route anything sensibly until it has the network's channel map.

Core Lightning:

```markdown
lightning-cli getinfo
```

### Fund the on-chain wallet

```markdown
lncli newaddress p2tr
lncli walletbalance
```

The output has three numbers that people confuse:

|   |   |
|---|---|
|Field|Meaning|
|`total_balance`|Everything the wallet knows about|
|`confirmed_balance`|What you can actually open channels with|
|`reserved_balance_anchor_chan`|Held back for anchor fee-bumping — **not** available|

Core Lightning:

```markdown
lightning-cli newaddr p2tr
lightning-cli listfunds
```

### The anchor reserve is not optional

LND holds back roughly 10,000 sat per anchor channel, capped at about 100,000 sat, so that it can always CPFP a commitment transaction if it has to force-close. If you commit every satoshi into channels, you lose the ability to close them safely.

Beyond the automatic reserve, keep a deliberate on-chain buffer. A reasonable rule: **enough to pay for closing every channel at 50 sat/vB, plus a margin.** Roughly 20,000 to 30,000 sat per channel. A node that cannot afford to close its channels during a fee spike is a node whose funds are hostage to the mempool.

Also keep several separate UTXOs rather than one large one. Opening a channel spends a UTXO and returns change, and during the confirmation window that change is unavailable — so a single-UTXO wallet can only open one channel at a time.

### Choosing peers

This decision is made once, costs on-chain fees to reverse, and determines most of what the channel will ever be worth. The common mistake is connecting to the largest, best-known nodes: that is the most competitive part of the graph, where fees are driven toward zero and your liquidity is one of thousands of identical options.

Better questions to ask:

- **Where does payment flow actually go?** Exchanges, wallet providers, merchant processors and large routing nodes are endpoints people pay to and from.
- **Is the peer reliably online?** An offline peer is a dead channel. Check uptime on a node explorer before committing capital.
- **Will the channel be bidirectional?** A channel toward an exchange drains one way and stays drained. That is fine if you priced it to be, but know it going in.
- **What are their fee policies?** A peer charging 3,000 ppm outbound makes your inbound expensive for everyone.
- **Do they already have a channel with you?** A second channel to the same peer rarely helps; capacity on the existing one usually does.

Inspect a candidate before opening:

```markdown
lncli getnodeinfo --pub_key=<pubkey> --include_channels | jq '{
  alias: .node.alias,
  channels: .num_channels,
  capacity: .total_capacity,
  addresses: [.node.addresses[].addr]
}'
```

### Sizing

|   |   |
|---|---|
|Size|Reality|
|Under 500k sat|Channel reserve and commitment fees eat a meaningful share; closing costs are disproportionate|
|1M to 5M sat|Sensible range for a first routing channel|
|5M to 20M sat|Serious routing capacity|
|Over 16.7M sat|A **wumbo** channel. Supported by default in modern LND, but the peer must also accept them.|

The protocol minimum that matters in practice is about 20,000 sat, below which dust limits make the channel largely unusable.

Two principles. **Fewer, larger channels beat many small ones** — each channel costs two on-chain transactions over its life regardless of size, so small channels pay a proportionally brutal fixed cost. And **size for the flow you expect**, not for what you can afford: capacity that never moves earns nothing while still costing you its open and close.

## Opening channels

### Connect first

A channel requires an existing peer connection. Connecting and opening are separate steps.

```markdown
lncli connect 03abc...def@198.51.100.7:9735
lncli listpeers | jq '.peers[] | {pub_key, address, inbound}'
```

Core Lightning:

```markdown
lightning-cli connect 03abc...def 198.51.100.7 9735
```

If the connection fails, the peer is offline, behind a firewall, or reachable only over Tor. Nothing else will work until this does.

### The basic open

```markdown
lncli openchannel \
  --node_key=03abc...def \
  --local_amt=2000000 \
  --sat_per_vbyte=8
```

Core Lightning:

```markdown
lightning-cli fundchannel id=03abc...def amount=2000000 feerate=8000perkb
```

Always set the fee rate explicitly. The default estimate is frequently higher than necessary, and a funding transaction is not urgent — it can wait for confirmation. Check the mempool first:

```markdown
bitcoin-cli estimatesmartfee 6 | jq '.feerate * 100000'
```

### Options worth knowing

|   |   |
|---|---|
|Flag|Effect|
|`--local_amt`|Total channel capacity, in satoshis|
|`--push_amt`|Sats given to the peer at open, creating inbound liquidity. **Irreversibly a gift.**|
|`--private`|Channel is not announced to the network. Usable for your own payments, invisible to routing.|
|`--sat_per_vbyte`|Funding transaction fee rate|
|`--min_confs`|Minimum confirmations on the UTXOs being spent|
|`--close_address`|Pre-commits where funds go on cooperative close — useful if the node and the cold wallet are separate|
|`--remote_csv_delay`|Timelock you impose on the peer's force-close output|
|`--base_fee_msat`, `--fee_rate_ppm`|Set the channel's routing policy at open rather than afterwards|

**On `--push_amt`:** it is the simplest way to get inbound liquidity and the easiest way to lose money. Those sats become the peer's balance the moment the channel confirms, with no obligation of any kind. Use it for a peer you have an actual relationship with, or not at all. Buying inbound through a liquidity marketplace or a submarine swap is usually cheaper and always safer.

**On `--private`:** private channels are right for a merchant receiving payments and wrong for a routing node. An unannounced channel cannot be used by anyone else to route, so it earns nothing.

### Funding from cold storage with PSBT

This is how you open a channel without the node's hot wallet ever holding the funds — relevant for any client-facing deployment.

```markdown
lncli openchannel --node_key=03abc...def --local_amt=5000000 --psbt
```

The command pauses and prints a funding address and amount. You then:

1. Build a PSBT paying that address, in Sparrow or your coordinator
2. Sign it on the hardware device
3. Paste the signed PSBT back into the waiting `lncli` prompt
4. `lncli` verifies the output and broadcasts

The critical detail: **do not broadcast the funding transaction yourself.** Let `lncli` do it. Broadcasting out of band before the node has registered the channel can strand the funds in a 2-of-2 output your node does not know about.

### Batch opening

Several channels from one on-chain transaction, which saves meaningful fees:

```markdown
lncli batchopenchannel --sat_per_vbyte=8 '[
  {"node_pubkey": "03aaa...", "local_funding_amount": 2000000},
  {"node_pubkey": "03bbb...", "local_funding_amount": 3000000},
  {"node_pubkey": "03ccc...", "local_funding_amount": 2500000}
]'
```

Core Lightning has `multifundchannel` with the same intent. Connect to every peer first — the batch fails as a unit if any peer is unreachable.

### Watching it confirm

```markdown
lncli pendingchannels | jq '.pending_open_channels[] | {
  peer: .channel.remote_node_pub,
  capacity: .channel.capacity,
  confirmations: .confirmation_height
}'
```

Anchor-type channels need 3 confirmations for smaller sizes and 6 for larger. Until then the channel exists on-chain but cannot carry payments.

If the funding transaction is stuck at a fee that was too low, you can CPFP it from the node's wallet:

```markdown
lncli wallet bumpfee --sat_per_vbyte=25 <funding_txid>:<change_output_index>
```

That spends the change output at a higher rate, pulling the parent in with it.

## Inspecting channels

### The channel list

```markdown
lncli listchannels
```

Core Lightning:

```markdown
lightning-cli listpeerchannels
```

The fields that carry real information:

|   |   |
|---|---|
|Field|Meaning|
|`active`|Peer is online and the channel can carry payments right now|
|`channel_point`|`txid:index` — the identifier for close and policy commands|
|`chan_id`|Short channel ID, used in routing and gossip|
|`capacity`|Total, fixed at open|
|`local_balance`|Your outbound: what you can send or forward|
|`remote_balance`|Your inbound: what you can receive|
|`commit_fee`|Deducted from the initiator's side — yours, if you opened|
|`local_chan_reserve_sat`|Your unspendable 1%|
|`unsettled_balance`|Currently locked in pending HTLCs|
|`total_satoshis_sent` / `_received`|Lifetime flow, the basis for diagnosing a channel|
|`num_updates`|State changes. Near zero on an old channel means it has never been used.|
|`uptime` / `lifetime`|Ratio gives the peer's real reliability|
|`initiator`|Whether you opened it — determines who pays closing fees|
|`private`|Unannounced|

### A readable overview

```markdown
lncli listchannels | jq -r '
  ["ALIAS","CAP","LOCAL","REMOTE","RATIO","UP%","ACT"],
  (.channels[] | [
    (.peer_alias // .remote_pubkey[0:12]),
    (.capacity|tonumber/1000|round|tostring+"k"),
    (.local_balance|tonumber/1000|round|tostring+"k"),
    (.remote_balance|tonumber/1000|round|tostring+"k"),
    ((.local_balance|tonumber) / (.capacity|tonumber) * 100 | round | tostring + "%"),
    ((.uptime|tonumber) / (.lifetime|tonumber) * 100 | round | tostring),
    (if .active then "yes" else "NO" end)
  ]) | @tsv' | column -t
```

The uptime column is the one to act on. A peer below 95% is costing you: every hour it is offline, that capital earns nothing and the channel risks a stale-state close.

### Aggregate balances

```markdown
lncli channelbalance | jq '{
  outbound: .local_balance.sat,
  inbound: .remote_balance.sat,
  pending_outbound: .pending_open_local_balance.sat
}'
```

If inbound is near zero you cannot receive anything, which for a merchant node is total failure regardless of how much capacity you have deployed.

### Pending channels

```markdown
lncli pendingchannels
```

Four categories, each meaning something different:

|   |   |
|---|---|
|Category|State|
|`pending_open_channels`|Funding broadcast, waiting for confirmations|
|`pending_closing_channels`|Cooperative close broadcast, not yet confirmed|
|`pending_force_closing_channels`|Force close confirmed; your output is in its CSV timelock. Shows `blocks_til_maturity`.|
|`waiting_close_channels`|Close negotiated, transaction not yet broadcast|

`blocks_til_maturity` is the number to quote a client asking when their money comes back.

### A single channel's routing policy

```markdown
lncli getchaninfo --chan_id=<chan_id> | jq '{node1_policy, node2_policy}'
```

Shows both directions, so you can see what the peer charges to route _into_ you — which affects whether anyone can reach you cheaply.

### Forwarding history

```markdown
lncli fwdinghistory --start_time=$(date -d '30 days ago' +%s) --max_events=50000
```

Revenue per channel over the period:

```markdown
lncli fwdinghistory --start_time=$(date -d '30 days ago' +%s) --max_events=50000 |
  jq -r '.forwarding_events | group_by(.chan_id_out)[] |
    "\(.[0].chan_id_out)  \(length) fwds  \(map(.fee_msat|tonumber) | add / 1000 | round) sat"' |
  sort -k2 -rn
```

This is the report that matters. Run it monthly and you will find that a handful of channels earn almost everything, several break even, and some have never forwarded a payment at all.

## Day-to-day management

### Updating a channel's fee policy

```markdown
lncli updatechanpolicy \
  --base_fee_msat=0 \
  --fee_rate_ppm=400 \
  --time_lock_delta=40 \
  --chan_point=<txid>:<index>
```

Omit `--chan_point` and it applies to every channel — which is almost never what you want.

Core Lightning:

```markdown
lightning-cli setchannel id=<short_channel_id> feebase=0 feeppm=400
```

The policy governs payments **leaving** through that channel, spending your local balance. Check what took effect:

```markdown
lncli feereport | jq '.channel_fees[] | {chan_point, base_fee_msat, fee_per_mil}'
```

A practical default: base fee `0`, express everything in ppm. Pathfinding algorithms penalise base fee heavily on small payments, so a non-zero base can quietly remove you from consideration on the payments that flow most often.

### HTLC limits

```markdown
lncli updatechanpolicy \
  --min_htlc_msat=1000 \
  --max_htlc_msat=1500000000 \
  --base_fee_msat=0 --fee_rate_ppm=400 --time_lock_delta=40 \
  --chan_point=<txid>:<index>
```

`max_htlc_msat` is the underused tool here. When a channel is nearly drained, setting it below your remaining local balance stops large forwards without publishing an absurd fee. Senders route around the size limit rather than around your price, so you avoid a wall of failures that would damage your reputation in their pathfinding.

Note that `updatechanpolicy` replaces the whole policy — pass every field you want to keep, or you will silently reset the others.

### Keeping peers connected

An offline peer means a dead channel. Make reconnection automatic:

```markdown
lncli listchannels | jq -r '.channels[] | select(.active == false) |
  "\(.remote_pubkey)@\(.peer_alias // "unknown")"'
```

For peers that drop frequently, pin them in `lnd.conf`:

```markdown
[Application Options]
minbackoff=10s
maxbackoff=5m
```

If a specific peer is persistently unreachable, reconnect by hand and check whether their advertised address is stale:

```markdown
lncli getnodeinfo --pub_key=<pubkey> | jq '.node.addresses'
lncli connect <pubkey>@<address>
```

A peer whose uptime sits below 90% over a month is not a routing partner. Close the channel and redeploy the capital.

### Liquidity

Channels drain in the direction payments flow, and nothing inside the protocol pushes them back. Three ways to respond, cheapest first:

**Fee steering** is free. Raise the outbound rate on a draining channel and lower it on a full one, and let the network reposition your liquidity while paying you for the privilege.

**Circular rebalancing** routes a payment out one channel and back in another, costing other nodes' routing fees. Always cap the rate:

```markdown
bos rebalance --out <peer-a> --in <peer-b> --amount 500000 --max-fee-rate 300
```

The cap is the single most important setting. Without it, the tool will cheerfully pay 3,000 ppm to move sats you sell at 400, and report success.

**Submarine swaps** change the total liquidity on your side rather than moving it between channels. Use Boltz or Loop when circular rebalancing finds no route. Swapping via Liquid rather than mainchain avoids most of the on-chain fee.

### Routine checks

|   |   |
|---|---|
|Interval|Check|
|Daily|Alerts only: node down, channel force-closing, disk, peer offline|
|Weekly|Fee policy against channel balances; rebalance spend against revenue|
|Monthly|Net margin per channel; close the dead ones|
|Quarterly|Peer selection and capital allocation|

Automate fee policy with `charge-lnd` before you automate rebalancing. Fee steering is free and reduces how much rebalancing you need; automating rebalancing first just makes the expensive mistake happen faster.

## Closing channels

### Cooperative close

The default and the one you want. Both nodes must be online.

```markdown
lncli closechannel \
  --funding_txid=<txid> \
  --output_index=<index> \
  --sat_per_vbyte=6
```

Core Lightning:

```markdown
lightning-cli close id=<peer_id> unilateraltimeout=300
```

CLN's `unilateraltimeout` is how many seconds to wait for cooperation before falling back to a force close. Setting it to `0` waits indefinitely, which is usually what you want for a peer you expect to come back.

Set the fee rate deliberately. Closing is rarely urgent, and the difference between 5 and 50 sat/vB on a close is real money.

```markdown
lncli closechannel --funding_txid=<txid> --output_index=<n> \
  --delivery_address=bc1q...
```

`--delivery_address` sends the proceeds straight to an address you specify rather than the node's hot wallet. Worth using whenever the node and the custody wallet are separate.

### Who pays

The channel **initiator** pays the closing fee, for both cooperative and force closes. This is a real consideration when deciding whether to open a channel or ask the peer to open one toward you: the opener carries the on-chain cost at both ends of the channel's life.

### Force close

Only when the peer is unreachable or refuses to cooperate.

```markdown
lncli closechannel --funding_txid=<txid> --output_index=<n> --force
```

What happens next:

1. Your latest commitment transaction is broadcast
2. Your peer's output is spendable immediately
3. **Your** output is encumbered by a CSV timelock, typically 144 blocks
4. After maturity, your node broadcasts a sweep transaction claiming it
5. Any in-flight HTLCs require their own resolution transactions

So you pay for two or more on-chain transactions and wait roughly a day. Track it:

```markdown
lncli pendingchannels | jq '.pending_force_closing_channels[] | {
  channel_point: .channel.channel_point,
  limbo_balance: .limbo_balance,
  blocks_til_maturity: .blocks_til_maturity,
  recovered_balance: .recovered_balance
}'
```

`limbo_balance` is funds still locked. It should reach zero once every output is swept.

### Anchor outputs and fee bumping

An anchor commitment transaction carries almost no fee by design, so broadcasting it alone may leave it stuck in the mempool for a long time. The anchor output exists precisely so you can CPFP it:

```markdown
lncli wallet bumpforceclosefee --conf_target=6 <funding_txid>:<index>
```

Older LND versions used `bumpclosefee`; check `lncli wallet --help` for your build.

This is why the on-chain reserve matters. **A node with no spendable on-chain balance cannot bump an anchor**, and a stuck commitment transaction during a fee spike means funds inaccessible until the mempool clears. Keep the buffer.

### When the peer disappears mid-close

If a cooperative close hangs because the peer went offline partway through, the channel sits in `waiting_close_channels`. Options:

- Wait. If the peer returns, the close completes normally and cheaply.
- Force close, accepting the timelock and extra fees.

For a peer that has been gone a few hours, waiting is usually right. For one gone a week with no sign of returning, force close.

### What not to do

`lncli abandonchannel` removes a channel from your node's database **without** closing it on-chain. It exists for genuinely stuck pending channels whose funding transaction will never confirm, and it is a footgun: abandoning a real channel means your node forgets state it may need to claim funds or defend against a revoked broadcast. It requires `--i_know_what_i_am_doing` for a reason. Do not use it on a client's node without understanding exactly why.

Similarly, `lncli closeallchannels` exists. It will do precisely what it says, including force-closing every channel whose peer happens to be offline at that moment.

### Timing closes

Closing costs an on-chain transaction, so close when fees are low. Unless a peer is misbehaving or a channel is genuinely at risk, there is no urgency — batch your closes into a quiet mempool window and save the client real money.

```markdown
bitcoin-cli estimatesmartfee 144 | jq '.feerate * 100000'
```

If that number is in the low single digits, it is a good day to clean up dead channels.

## Backups and recovery

### The static channel backup

LND maintains `channel.backup` in the chain-specific data directory and rewrites it every time channel state changes. It is encrypted with your seed, so it is safe to store anywhere.

```markdown
lncli exportchanbackup --all --output_file=/tmp/channel.backup
lncli verifychanbackup --multi_file=/tmp/channel.backup
```

Automate copying it off the machine. A `systemd` path unit watching the file is the clean approach:

```markdown
# /etc/systemd/system/scb-backup.path
[Path]
PathChanged=/var/lib/lnd/data/chain/bitcoin/mainnet/channel.backup

[Install]
WantedBy=multi-user.target
```

Pair it with a service that copies the file to at least two destinations off the host.

Core Lightning takes a different approach — the `emergency.recover` file plus database replication, and optionally the `backup` plugin. Read its documentation; the semantics are not the same as LND's.

### What restoring actually does

This is the part that loses people money, so be precise about it.

An SCB is **not** a backup that restores your channels to working order. Restoring it triggers the Data Loss Protection protocol: your node contacts each peer, announces that it has lost state, and asks them to force-close. The peers broadcast their latest commitment transactions and you receive your balance on-chain, after the usual timelocks.

|   |   |
|---|---|
|What you get|What you do not get|
|Your on-chain balance back|Working channels|
|Funds from every channel in the backup|Any channel opened after the backup was taken|
|Protection against total node loss|Fast recovery — expect timelocks|

So it is a disaster instrument, not a restore path. Every channel closes, you pay force-close costs on all of them, and you rebuild from scratch.

### Recovery procedure

```markdown
lncli create
# choose: restore from existing seed
# supply the 24-word aezeed and the SCB file when prompted
```

Or for an already-initialised node:

```markdown
lncli restorechanbackup --multi_file=/path/to/channel.backup
```

Then watch the closes resolve:

```markdown
lncli pendingchannels
```

You need both the **seed** and the **backup file**. The seed alone recovers on-chain funds only. The backup alone recovers nothing, since it is encrypted to the seed.

### The way this loses funds

**Never restore an old `channel.db`.** This is the single most dangerous operation in Lightning. The database holds revoked commitment states; restoring a stale copy and resuming operation can cause your node to broadcast a revoked state, which your peer will punish by taking the entire channel balance. The penalty mechanism cannot distinguish an honest restore from an attempted cheat.

The rule: if `channel.db` is lost or suspect, use the SCB path and accept that every channel closes. Do not attempt to resurrect an old database because it looks like it would preserve the channels. It will not.

**Never run two nodes on the same seed and channel state.** Same failure, same penalty.

**Never restore a stale SCB and keep operating.** Channels opened after the backup was taken are not in it, and their funds are not recovered by it.

### Backup hygiene

|   |   |   |
|---|---|---|
|Item|Where|How often|
|`channel.backup`|Two off-host locations|On every change, automated|
|Seed phrase|Metal, offline, separate from the node|Once, at creation|
|`lnd.conf`|Config repo|On change|
|Fee policy export|Config repo|Monthly|
|Channel peer list|Documentation|Monthly|

That last row is worth the trouble. After an SCB recovery you will want to reopen channels to the same peers, and `listchannels` output from a working node is the only convenient record of who they were.

### Test it

On signet, build a node with a few channels, take the backup, destroy the node completely, and recover from seed plus SCB. Time it. Watch the force closes resolve.

Until you have done that once, you do not know whether your backup procedure works — and the client's node is the wrong place to find out.

## Troubleshooting

### Opening

|   |   |   |
|---|---|---|
|Symptom|Cause|Fix|
|`not enough witness outputs to create funding transaction`|Confirmed balance too low, or the anchor reserve is holding funds back|Check `walletbalance` and subtract `reserved_balance_anchor_chan`|
|`peer not online`|Not connected, or the connection dropped|`lncli connect` first, confirm with `listpeers`|
|`channel too large`|Peer does not accept wumbo channels|Open below 16.7M sat, or pick another peer|
|`channel too small`|Below the peer's minimum|Most peers want at least 100k to 1M sat|
|`received funding error: chan size below min`|Peer's own policy|Ask, or choose another peer|
|Funding tx stuck unconfirmed|Fee rate too low|`lncli wallet bumpfee` on the change output|
|Pending open never confirms, tx not in mempool|Transaction was dropped|Wait for LND to rebroadcast; as a last resort `abandonchannel` once you are certain it will never confirm|

### Operating

|   |   |   |
|---|---|---|
|Symptom|Cause|Fix|
|Channel shows `active: false`|Peer offline, or connection dropped|Reconnect; check their uptime before bothering|
|Forwards fail with `TEMPORARY_CHANNEL_FAILURE`|Insufficient local balance in that direction|Rebalance, or raise the fee and wait|
|Forwards fail with `FEE_INSUFFICIENT`|Sender used a stale policy from gossip|Normal after a fee change; stop changing fees so often|
|No forwards at all on a healthy channel|Priced out, or not on any useful path|Lower the fee to test; if still nothing, it is position, not price|
|`max_htlc` errors on large payments|Your own `max_htlc_msat` is set low|Check `feereport` and the channel policy|
|Payments fail with 483 HTLC limit|Protocol maximum of concurrent pending HTLCs reached|Rare; indicates very high throughput or stuck HTLCs|

### Closing

|   |   |   |
|---|---|---|
|Symptom|Cause|Fix|
|Cooperative close hangs|Peer went offline mid-negotiation|Wait, or force close|
|Force close tx stuck in mempool|Anchor commitment has near-zero fee|`lncli wallet bumpforceclosefee`|
|Cannot bump — no funds|On-chain wallet empty|This is why the reserve exists. Send sats to the node wallet, then bump.|
|`limbo_balance` not decreasing|CSV timelock has not matured|Read `blocks_til_maturity` and wait|
|Funds not swept after maturity|Node was offline at maturity, or fee too low|Restart the node; it resumes sweeping|
|Channel stuck in `waiting_close`|Close negotiated, not broadcast|Restart; if it persists, force close|

### Diagnostics that answer most questions

```markdown
lncli getinfo | jq '{synced_to_chain, synced_to_graph, num_active_channels, num_inactive_channels, num_pending_channels, block_height}'

lncli listchannels | jq -r '.channels[] | select(.active == false) |
  "INACTIVE: \(.peer_alias // .remote_pubkey[0:16])  local=\(.local_balance)"'

lncli pendingchannels | jq '{
  opening: (.pending_open_channels | length),
  closing: (.pending_closing_channels | length),
  force_closing: (.pending_force_closing_channels | length),
  waiting: (.waiting_close_channels | length)
}'

lncli walletbalance | jq '{confirmed: .confirmed_balance, reserved: .reserved_balance_anchor_chan}'
```

And the logs, which say more than any RPC:

```markdown
journalctl -u lnd -f
journalctl -u lnd --since '1 hour ago' | grep -iE 'error|fail|force|close'
```

### Three habits worth building

**Check the peer before blaming the channel.** Most "channel problems" are a peer that has been offline for six hours.

**Check the fee environment before closing anything.** A close at 80 sat/vB that could have waited a week for 4 sat/vB is money thrown away, and on a client's node it is money you threw away.

**Never run a command with `--force` or `--i_know_what_i_am_doing` until you can explain exactly what it will do on-chain.** Those flags exist because the operations behind them are irreversible.