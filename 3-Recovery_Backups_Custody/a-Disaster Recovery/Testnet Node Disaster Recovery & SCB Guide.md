**

Testnet Node Disaster Recovery & SCB Guide

Role: Bitcoin Node Consultant (LATAM Market)  
Phase: Disaster Recovery, Backups, & Custody Ops Drill

I have created a comprehensive Google Doc for your disaster recovery drills. This document serves as a standard operating procedure (SOP) that you can reference while practicing on Testnet and eventually use as a framework when rescuing client nodes.
### Key Concepts in the Guide:

1. **The "Break":** How to simulate a catastrophic drive failure by wiping the `~/.lnd/data/` directory while the daemon is offline.
2. **On-Chain Recovery:** Using `lncli create` to input your 24-word Aezeed seed phrase and trigger a blockchain rescan to recover on-chain funds.
3. **Lightning Recovery:** Using the `channel.backup` file (`lncli restorechanbackup`) to execute the Data Loss Protection (DLP) protocol. It's crucial to understand (and explain to clients) that SCBs **do not restore channels to a working state**. They force your peers to close the channels and refund your local balance back on-chain after a timelock delay.
4. **Client Communication:** A brief script in Spanish on how to explain the timelock delay to an anxious client so they know their funds are secure.
Practicing this on Testnet multiple times is the best way to build the confidence needed to handle high-stress, high-value recovery scenarios for your consulting business.
# 1. Objective

This drill is designed to simulate a catastrophic hardware failure on a Lightning node and walk through the complete recovery process using only a 24-word seed phrase and a Static Channel Backup (SCB) file. Mastering this process is critical for consulting, as clients will inevitably face hardware corruption, and recovering their funds securely is the highest-value service you provide.

# 2. Prerequisites & Preparation

Before you break the node, you must set up the environment and secure your backups.

- The Node: A synced Bitcoin and LND node running on Testnet (do not practice this on Mainnet until you have done it 5 times successfully on Testnet).
    
- Funds: Fund your on-chain wallet with Testnet BTC (tBTC) from a faucet.
    
- Channels: Open 2–3 Lightning channels with other Testnet nodes. Wait for them to become active.
    
- The Crucial Backups:
    

1. Seed Phrase: Write down the 24-word Aezeed seed phrase.
    
2. SCB File: Download the channel.backup file to your local computer. (In Umbrel, this is found in the LND advanced settings; via CLI, you can copy it from ~/.lnd/data/chain/bitcoin/testnet/channel.backup).
    
# 3. Phase 1: Intentional Destruction (The Break)

To simulate a drive failure, we will completely wipe the LND database and state while the node is stopped.

1. Stop the LND service. If you are on bare-metal, run sudo systemctl stop lnd. If on Umbrel/Docker, stop the specific LND container.
    
2. Navigate to your LND directory (e.g., ~/.lnd/).
    
3. The Wipe: Delete the entire data directory. Run rm -rf ~/.lnd/data/. This removes the wallet database (wallet.db), the channel graph, and all channel state (channel.db).
    
4. Restart the LND service. Your node is now effectively factory-reset and locked out of its previous identity.
    
# 4. Phase 2: On-Chain Wallet Recovery

The first step is to regain control of your on-chain funds.

Note: Aezeed seed phrases (used by LND) include the wallet birthday, which speeds up block rescanning.

1. Initialize Recovery: Connect to your node via SSH and use the LND CLI:  
    lncli create
    
2. Input Seed: When asked if you have an existing cipher seed, type y. Enter your 24 words exactly.
    
3. Set Password: Set a new unlock password (it does not have to be the old one, but for simplicity, keep it consistent).
    
4. The Rescan: LND will now rescan the blockchain from the wallet's birthday to find your on-chain UTXOs. You can monitor the progress in the LND logs (tail -f ~/.lnd/logs/bitcoin/testnet/lnd.log).
    
5. Verify: Once the rescan is complete, run lncli walletbalance. You will see your on-chain tBTC, but your Lightning funds are still missing because the channels are gone.
    
# 5. Phase 3: Lightning Channel Recovery (SCB)

Critical Concept: An SCB (channel.backup) does not restore your channel state so you can keep routing. It only contains the cryptographic keys needed to ask your channel peers to force-close the channels. The funds will be swept back to your on-chain wallet.

1. Upload the channel.backup file from your laptop back to the node's server (e.g., to the /tmp/ directory).
    
2. Execute the restore command:  
    lncli restorechanbackup --multi_file /tmp/channel.backup
    
3. The Process: LND reads the file, connects to your former channel peers, and sends a Data Loss Protection (DLP) protocol request. Your peers will execute a force-close transaction on the blockchain.
    
4. Monitor pending channels:  
    lncli pendingchannels
    
5. The Waiting Game: Because these are force-closures, your funds are encumbered by a timelock (CSV delay). This can take anywhere from a few hours to 2 weeks (in blocks) depending on the initial channel parameters.
    
# 6. Verification & Client Explanation

- Keep checking lncli pendingchannels over the next few days (or hours, if the timelock is short).
    
- Eventually, the funds will shift from "limbo" into your regular on-chain walletbalance.
    

How to Explain This to a LATAM Client:"Hemos recuperado tu billetera principal y hemos activado el protocolo de emergencia para tus canales de Lightning. Los otros nodos ya han cerrado los canales y tus fondos están asegurados en la cadena de bloques. Por razones de seguridad del protocolo Bitcoin, hay un tiempo de espera (timelock) antes de que puedas gastarlos. Todo está bajo control."

**
#### Walk me through how to integrate hardware wallets with a node for commercial clients who require cold storage.####

For commercial clients, security is paramount. When you are managing corporate treasuries, large merchants, or business reserves, simply plugging a hardware wallet into a USB port on an internet-connected computer is often considered a security risk.

For the highest tier of cold storage consulting, we use an **Air-Gapped PSBT (Partially Signed Bitcoin Transaction)** workflow. This means the hardware wallet is _never_ connected to a PC via USB. It only ever plugs into a wall outlet or battery pack for power.

Here is how you set up and train a commercial client on an air-gapped cold storage vault using their own node.
### The Architecture

1. **The Node (Backend):** Bitcoin Core + Electrs running on a Linux server.
2. **The Interface (Frontend):** Sparrow Wallet running on the business's office computer, securely connected to the node.
3. **The Cold Storage (The Vault):** An air-gapped hardware wallet (like a Coldcard or Foundation Passport) that communicates only via MicroSD cards or QR codes.
### Step 1: Create the "Watch-Only" Office Wallet

The beauty of this setup is that the business accountant or staff can monitor the balance and generate receiving addresses without ever having the power to spend the funds.

1. **Export the `xpub`:** On the air-gapped hardware wallet, navigate to the export menu and save the wallet's configuration (which includes the Extended Public Key, or `xpub`) to a MicroSD card.
2. **Import to Sparrow:** Take the MicroSD card and plug it into the office computer. Open Sparrow Wallet (which is connected to the company's node).
3. **Create Watch-Only:** Go to **File > New Wallet**. Under Keystores, instead of clicking "Connected Hardware Wallet", select **Airgapped Hardware Wallet**. Choose the brand (e.g., Coldcard) and import the file from the SD card.
4. **Result:** Click Apply. The office now has a "Watch-Only" wallet. They can click the "Receive" tab to generate invoices for clients, and they can watch funds arrive securely verified by their own node, but the "Send" button will lack the private keys to execute a transaction.
### Step 2: Proposing a Transaction (The PSBT)

When the business needs to pay a vendor or move funds out of cold storage, the staff initiates the process using a PSBT.

1. **Draft the Payment:** The accountant goes to the "Send" tab in the Watch-Only Sparrow Wallet, enters the vendor's address, and sets the fee.
2. **Create the PSBT:** Instead of clicking "Sign" (which they can't do), they click **Create Transaction**.
3. **Export the PSBT:** Sparrow will generate a PSBT file. The accountant clicks **Export PSBT** and saves it to the MicroSD card.
4. **Hand-off:** The accountant physically hands the MicroSD card to the business owner or CEO (who holds the physical hardware wallet and the PIN).
### Step 3: Air-Gapped Signing (The CEO's Job)

This is where the magic happens. The private keys remain completely isolated from the internet.

1. The CEO plugs the hardware wallet into a wall outlet (power only) and enters their PIN.
2. They insert the MicroSD card into the hardware wallet.
3. They select "Ready to Sign" on the device. The hardware wallet reads the PSBT file.
4. **Verification:** The hardware wallet's screen will display the exact amount being sent, the fee, and the destination address. The CEO verifies this matches the vendor's invoice.
5. **Sign:** The CEO approves it on the device. The hardware wallet cryptographically signs the transaction and saves a new file to the SD card called a _Signed PSBT_.
### Step 4: Broadcasting the Payment

1. The CEO hands the MicroSD card back to the accountant.
2. The accountant puts the SD card into the office computer, opens Sparrow Wallet, and clicks **Load Transaction**.
3. They load the Signed PSBT. Sparrow merges the signatures and the **Broadcast** button lights up.
4. The accountant clicks Broadcast. Sparrow routes the finalized transaction through their private Linux node and out to the Bitcoin network.
### How to Pitch This to a LATAM Business Owner

As a consultant, your value is translating this technical process into business confidence.

"Señor/Señora, con este sistema de 'Bóveda Fría' (Cold Vault), sus empleados o contadores pueden recibir pagos, generar facturas y ver los saldos desde la computadora de la oficina. Sin embargo, es físicamente imposible que un hacker, un empleado descontento o un virus robe los fondos. Para que salga un solo centavo de la empresa, usted tiene que aprobarlo físicamente en este dispositivo desconectado del internet. Además, al usar nuestro propio servidor (nodo), ningún banco ni empresa externa puede rastrear sus balances ni congelar sus cuentas."

#### What are the best strategies for managing inbound and outbound liquidity on a routing node?####

A routing node relies on having sufficient liquidity on both sides of a channel—inbound to receive funds and outbound to send them. Because routing continuously shifts these balances, maintaining equilibrium requires a mix of passive economic incentives and active technical adjustments.
### 1. Dynamic Fee Adjustments (Passive Management)

The most capital-efficient way to balance channels is to let the network do it for you by dynamically adjusting your `fee_rate_ppm`.

- **Depleted Outbound:** If a channel's funds are entirely on the peer's side, raise your routing fee heavily. This signals to the network that the path is expensive, halting outbound flow until inbound payments refill your side.
- **High Outbound:** If a channel is saturated on your side, drop the fee rate to near zero. This incentivizes routing algorithms to push traffic through that channel, naturally pushing the balance back toward the middle.
### 2. Peer-to-Peer Atomic Swaps (PeerSwap)

When passive fee adjustments aren't fast enough, PeerSwap enables atomic swaps directly with whitelisted channel partners without a centralized coordinator.

- You can trade on-chain assets for Lightning inbound or outbound liquidity.
- Using the Liquid Network (L-BTC) for these swaps is highly recommended during high-fee environments.
- Liquid swaps confirm in about two minutes and bypass the mainchain completely.
- Refilling existing channels this way is far more capital efficient than closing depleted channels and opening new ones.
### 3. Automated Submarine Swaps (Lightning Loop)

Lightning Loop moves Bitcoin between your channels and the blockchain. Running this on your server allows you to manage liquidity without relying solely on direct channel peers.

- Use "Loop Out" to move Lightning funds back to an on-chain address, which replenishes your inbound liquidity.
- Use "Loop In" to push on-chain funds into your channels, replenishing outbound liquidity.
- The `autoloop` daemon can be configured to execute these swaps automatically based on a predefined budget.
### 4. Liquidity Marketplaces (Lightning Pool)

When setting up a new node, sourcing inbound capacity is the biggest hurdle because all newly opened channels start with 100% outbound liquidity.

- Lightning Pool acts as a peer-to-peer marketplace where node operators buy and sell inbound channel liquidity.
- You can purchase inbound liquidity on demand, or lease your excess liquidity to others to earn a yield.

Would you like to look into setting up the Elements daemon required to execute L-BTC PeerSwaps, or should we pivot to building Python scripts for automated channel monitoring?