The Lightning Network operates on a completely different paradigm than on-chain Bitcoin. Instead of broadcasting transactions to a global ledger, nodes act like miniature banks, shifting balances back and forth across pre-funded payment channels. When you understand how to manage liquidity and set fees, you turn a passive node into an active, profitable routing engine.

Here is your comprehensive tutorial on routing, fee policies, and channel balancing using submarine swaps.
## 1. How Routing Works: The Mechanics

The Lightning Network relies on **Hashed Time-Locked Contracts (HTLCs)** and **Source Routing**.

When a user in Argentina wants to pay a merchant in Mexico, they don't need a direct channel. Their wallet finds a path through the network—say, Alice → You (The LATAM Consultant) → Bob → Merchant.

Here is what happens mechanically:

1. **The Invoice:** The merchant generates an invoice with a cryptographic hash (the "lock").
    
2. **The Route:** The sender's wallet computes a path using the public graph data and wraps the payment in multiple layers of encryption (Onion Routing). You, the routing node, only know who handed you the payment and who to hand it to next—you do not know the original sender or final destination.
    
3. **The HTLC Forward:**
    
    - Alice sends you an HTLC (a promise to pay you if you produce the secret key). 
        
    - You forward an identical HTLC to Bob.
          
    - Bob forwards it to the Merchant.
        
4. **The Settlement:** The merchant reveals the secret key to claim the funds from Bob. Bob uses that key to claim from you. You use it to claim from Alice.
    
The payment shifts your balances. If Alice sent 500,000 sats through you to Bob:

- Your inbound liquidity with Alice _decreases_ by 500k.
    
- Your outbound liquidity with Bob _decreases_ by 500k (plus routing fees).
## 2. Setting Fee Policies for Profitability

Every node charges a routing fee to compensate for the capital locked in channels. Lightning fees are defined by two components:

- **Base Fee (msat):** A flat fee charged per forwarded transaction, regardless of size. (Often set to 0 or 1 sat to encourage micropayments).

- **Fee Rate / PPM (Parts Per Million):** A proportional fee based on the payment size. A rate of 1,000 ppm means you charge 1 satoshi for every 1,000 sats routed.
### The Dynamic Fee Strategy

Do not set a flat fee across your whole node. Fees should be used as a tool to incentivize or disincentivize traffic to balance your channels.

**High Outbound Liquidity (The channel is full on your side):**

If you have a 5M sat channel with `Kraken` and 4.8M sats are on your side, you want people to route _through_ this channel.

- **Action:** Lower the PPM (e.g., 10 to 50 ppm). Make it cheap so wallets preferentially route payments out through Kraken.
    
**Low Outbound Liquidity (The channel is empty on your side):**

If your channel with `Bitfinex` only has 50k sats on your side, you cannot route large payments through it. If a payment tries to route and fails, it hurts your node's reliability score.

- **Action:** Raise the PPM (e.g., 2,500+ ppm). This signals to the network: "Do not route this way unless you are willing to pay a massive premium."
    
### Setting Fees via CLI (LND Example)

To update the fee for a specific channel using `lncli`:

Bash

```
# Set base fee to 1000 msat (1 sat) and fee rate to 500 ppm for a specific channel point
lncli updatechanpolicy --base_fee_msat 1000 --fee_rate_ppm 500 --chan_point <txid:output_index>
```

_Pro Tip for Consultants:_ Tools like `charge-lnd` or `lndmanage` can automate fee policies using scripts. You write a rule (e.g., "If local balance > 80%, set fee to 10 ppm") and run it via a cron job.
## 3. Submarine Swaps: Balancing with Loop and Boltz

Fee adjustments are passive. If you need to actively fix a depleted channel, you use a **Submarine Swap**—an atomic exchange between off-chain Lightning funds and on-chain Bitcoin. The two primary tools are Lightning Labs' **Loop** and the **Boltz CLI**.

### Scenario A: You need INBOUND liquidity (Loop Out)

Your node is too popular. Everyone is paying you, and all your channels have the balance stuck on your side. You cannot receive any more payments.

- **The Fix:** You send Lightning sats to the swap provider, and they send on-chain Bitcoin to your cold storage or node wallet. This pushes your Lightning balances to the other side of the channel, opening up inbound capacity.
    
**Using Loop CLI:**

Bash

```
# Get a quote for swapping 1,000,000 sats to on-chain
loop quote out 1000000

# Execute the Loop Out
loop out 1000000
```

_Note: Loop Out incurs the provider's swap fee plus an on-chain sweep fee._
### Scenario B: You need OUTBOUND liquidity (Loop In / Reverse Swap)

You want to pay invoices or route payments, but all the funds are on your peers' side of the channels.

- **The Fix:** You send on-chain Bitcoin to the swap provider, and they push Lightning sats into your node, refilling your local balances.
    
**Using Boltz CLI (Often cheaper/faster for reverse swaps):**

Bash

```
# Create a reverse swap (you pay on-chain, you receive Lightning)
boltz reverse-swap create --amount 500000

# The CLI will output an on-chain address.
# Send exactly 500,000 sats (plus on-chain fees) to that address. 
# Once confirmed, Boltz pays your node 500,000 sats via Lightning.
```
### Automating the Swaps

If you are managing nodes for commercial clients (like a busy LATAM merchant), you cannot manually monitor liquidity 24/7. Lightning Loop includes an `autoloop` daemon.

Bash

```
# Enable autoloop to automatically dispatch Loop Outs when inbound liquidity drops
loop setparams --autoloop=true --type=out
```

This ensures a merchant's node is constantly clearing its Lightning balance to cold storage automatically, guaranteeing they never fail a customer's payment due to full channels.