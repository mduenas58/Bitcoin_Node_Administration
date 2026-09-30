Let me verify a few things that move fast — Core versions, the node-framework landscape, and the LATAM regulatory picture. Before the roadmap, one piece of market data you should build around rather than discover in month five.

## The honest market read

Chainalysis's 2026 regional report found that **self-custodied bitcoin in Latin America fell 78% in value over the report period while self-custodied stablecoins rose 66%**, lifting stablecoins to roughly a fifth of the region's self-custodied holdings. Meanwhile **64% of LATAM crypto activity happens on centralized exchanges**, higher than North America (49%) or Europe (53%). Brazil alone now receives 43.7% of the region's crypto value.

Translated: the mass-market LATAM user is not running a node. They're on Binance or Bitso holding USDT, and they're right to, given their problem is inflation rather than sovereignty.

That doesn't kill the business — it relocates it. The people who pay for node work are:

1. **Merchants and payment operators** needing self-hosted BTCPay/Lightning infrastructure — real, growing demand
2. **High-net-worth individuals and family offices** needing multisig custody, inheritance planning and recovery rehearsal — this is where the actual consulting fees live, by a wide margin
3. **Circular-economy and community projects** — Bitcoin Beach-style deployments, Fedimint federations, community mints
4. **Remittance operators** on the US→LATAM corridor
5. **The US Hispanic diaspora**, which is your local market in Denver, pays in dollars, and is far easier to collect from than a client in Buenos Aires

Point 5 deserves weight. You live in Colorado. A Spanish-speaking Bitcoin custody consultant serving Hispanic business owners in the US is a better-paying and more collectible business than the same service sold into LATAM, and it builds the reputation that makes the LATAM work possible later.

So the roadmap below weights **custody and merchant infrastructure heavily** and treats "install a node" as the entry point rather than the product. Nobody pays much for an Umbrel install. They pay a great deal to be confident their $2M in cold storage is recoverable by their children.

---

## Skills gap audit

|Domain|Your likely level|Target|Gap|
|---|---|---|---|
|Linux, networking, systemd, Docker|Expert|Expert|None — this is your moat|
|Node installation (bare metal, Umbrel, MyNode)|Solid|Expert|Modest|
|Bitcoin Core config depth (indexes, assumeutxo, descriptors)|Partial|Expert|**Real gap**|
|Protocol literacy (UTXO, script, PSBT, descriptors, Taproot)|Unknown|Working fluency|**Likely large gap**|
|Electrum servers, explorers, monitoring|Partial|Expert|Moderate|
|Lightning (implementations, liquidity, backup)|Unknown|Competent|**Likely large gap**|
|Multisig design & key ceremony|Unknown|Expert|**Largest gap, highest value**|
|Inheritance & recovery engineering|Unknown|Expert|**Largest gap, highest value**|
|BTCPay Server / merchant stack|Unknown|Expert|Moderate–large|
|Fedimint / Cashu / community stack|Unknown|Working|Large but niche|
|Privacy tooling (post-CoinJoin landscape)|Unknown|Competent|Moderate|
|LATAM regulatory landscape|Unknown|Working|**Business-critical gap**|

The pattern: your infrastructure skills are done. What's missing is everything _above_ the operating system — protocol semantics, key management as a discipline, and the commercial layer.

---

# Month 1 — Protocol depth and Core mastery

The goal is to stop being someone who installs Bitcoin software and start being someone who understands what it's doing. You cannot debug a failed multisig recovery from the sysadmin layer.

### Protocol fundamentals

Work through **"Learning Bitcoin from the Command Line"** (Blockchain Commons, free, on GitHub). It's written precisely for your profile — a command-line person who wants real fluency — and it will occupy a couple of weeks.

Core concepts to reach genuine comfort with, not just recognition:

- **UTXO model and transaction structure**: inputs, outputs, witness data, weight vs vbytes, why fee estimation works the way it does
- **Output descriptors** (BIP380 family). This is the single most important modern concept and the one most self-taught node people have never internalized. A descriptor is the actual backup artifact for anything beyond a single-sig wallet — a seed phrase alone will not recover a multisig, and clients who don't know this will eventually lose money. You will build a business partly on explaining this.
- **PSBT** (BIP174): the format that makes air-gapped and multi-party signing work. Construct, sign and finalize one by hand on signet.
- **Miniscript**: how complex spending conditions get expressed and analyzed. Needed for timelock and inheritance designs.
- **Taproot/Schnorr** (BIPs 340–342): key aggregation, script path vs key path, why it matters for multisig privacy
- **Fee mechanics**: RBF, CPFP, package relay, mempool policy vs consensus rules. Clients get stuck transactions; you need to unstick them.

### Bitcoin Core operations

Current stable is **31.1** (July 2026). **v32.0rc1 was tagged September 14, 2026 with the final release targeting October 10** — start testing it now, because release notes are where you find the things that break client deployments. Core ships a major release roughly every six months on an 18-month support cycle, so 29.x, 30.x and 31.x are the currently supported majors.

Master these specifically:

- `assumeutxo` — snapshot-based fast sync. Transformative for client onboarding: a usable node in hours instead of days, while background validation completes. Learn the security model and its limits well enough to explain the tradeoff.
- **Index economics**: `txindex`, `blockfilterindex`, `coinstatsindex`. Which ones a given deployment actually needs, and what each costs in disk and IBD time.
- **Pruning strategies** and what they foreclose (you can't run an Electrum server against a pruned node).
- **Descriptor wallet migration**. Legacy wallets are being phased out and there are clients still sitting on them. This is a billable service _right now_.
- **Guix reproducible builds and signature verification.** Learn to verify a release properly, then learn to build one. This is a credibility marker — when a client asks why they should trust your binaries, "I built them deterministically and the hash matches the signed manifest" is the answer that separates you from every Umbrel installer.
- `asmap` — **v31.0 embedded asmap data for the first time**, so the feature works without an external file, though it remains off by default and requires `-asmap` explicitly. Understand what ASN bucketing defends against.
- Tor, I2P and CJDNS configuration; onion service setup; why network-level privacy matters for a merchant.

### Lab build

You need a permanent testing environment:

- **regtest** for instant iteration and scripted scenarios
- **signet** for realistic multi-party testing — this is where you'll rehearse multisig ceremonies and recoveries
- **mainnet** node, pruned, for real-world reference

Everything in Docker Compose, versioned in git. This repository becomes your deployment tooling and eventually your product.

**Month 1 deliverable:** a scripted, reproducible regtest/signet environment plus written documentation of a Core node build from source with verified signatures.

---

# Month 2 — The service layer

A node alone is useless to a client. What they actually want is what the node _powers_.

### Electrum servers

The workhorse of any real deployment, because this is what connects a client's wallet to their own node.

- **electrs** vs **Fulcrum**: Fulcrum indexes faster and queries faster but demands far more RAM and disk; electrs is lighter. Know the resource curves well enough to spec hardware from a client's requirements.
- Full index build times on various hardware — measure this yourself so you can quote honestly.
- SSL termination, authentication, remote access patterns.

### Explorers and monitoring

- **mempool.space** self-hosted. Clients love this; it makes the abstract visible.
- **BTC RPC Explorer** as the lighter alternative.
- **Prometheus + Grafana** with a Bitcoin Core exporter. Block height lag, peer count, mempool size, disk headroom, IBD progress. This is your managed-service product — you can't sell monitoring you haven't built.
- Alerting that actually reaches you: node stalled, chain tip stale, disk threshold, reorg detected.

### Wallet connectivity

Get hands-on with each, connected to your own node:

- **Sparrow** — the professional's choice, best descriptor and PSBT handling, your primary tool
- **Specter Desktop** — multisig coordination
- **Nunchuk** — multisig with inheritance features
- **BlueWallet**, **Electrum** — what clients will actually have on their phones
- **Blockstream Green**

### Hardening

Full disk encryption with remote unlock, firewall policy, SSH key-only with hardware token, automatic security updates, fail2ban, unattended-upgrades tuning, backup of chainstate and wallet artifacts, and — critically — **a tested restore onto different hardware**.

**Month 2 deliverable:** a complete node stack (Core + Fulcrum + mempool.space + Grafana + Tor) deployable from your repo in under an hour, documented in Spanish and English.

---

# Month 3 — Lightning

Where merchant money lives, and where most consultants are dangerously shallow.

### Implementations

- **LND** — largest ecosystem, most tooling, most client deployments
- **Core Lightning (CLN)** — more modular, plugin architecture, favored by the technically serious
- **LDK** — library, not daemon; relevant if you ever build something custom
- Know when each is appropriate. Defaulting to LND because Umbrel does is not an answer a client should accept.

### Operations that separate professionals from hobbyists

- **Channel and liquidity management**: inbound vs outbound, why a merchant needs inbound liquidity and how to get it
- **Submarine swaps**: Boltz, Loop, PeerSwap
- **LSPs** — when to use one instead of running your own routing
- **Watchtowers** and the justice transaction model
- **Backup**, and this is the critical one: static channel backups are _not_ like a seed phrase. Restoring from an SCB force-closes channels and can lose funds if done wrong. Understand `channel.backup` semantics, the danger of restoring stale state, and why "just back up the folder" is advice that loses client money.
- **BOLT12 offers** — reusable payment codes, increasingly deployed

### Merchant-oriented Lightning

- **LNbits** — extensions, accounts, sub-wallets. The Swiss army knife for community and small-merchant deployments.
- **Phoenixd** — server daemon with automated channel management, genuinely good for small merchants who don't want liquidity management
- **Alby Hub**
- The operational difference between a routing node (optimizing for fees) and a merchant node (optimizing for reliable receipt)

**Month 3 deliverable:** a merchant Lightning stack on signet, plus a written runbook covering channel backup, restore procedure, and the failure modes of each.

---

# Month 4 — Custody, multisig and inheritance

**This is the highest-value month.** Node installation is a commodity; nobody else in your market is doing serious key-management engineering, and it's what wealthy clients actually lose sleep over.

### Multisig design

- Quorum selection: 2-of-3 vs 3-of-5, and the honest tradeoffs (2-of-3 is right for most individuals; 3-of-5 for institutions and families)
- **Geographic and custodial distribution** of keys — safe deposit boxes, trusted parties, professional custodians
- **Vendor diversity**: never all keys on the same hardware brand. A firmware flaw shouldn't be a single point of failure.
- Descriptor management as the true backup. Repeat to every client: seed phrases without the descriptor do not recover a multisig.

### Hardware signers — get hands-on with all of them

**Coldcard Q / Mk4** (air-gapped, NFC/SD, the professional standard), **BitBox02**, **Blockstream Jade**, **Trezor Safe 5**, **SeedSigner** and **Krux** (DIY, stateless, relevant where import costs or customs are a problem — which in LATAM they often are), **Foundation Passport**.

Air-gapped workflows in practice: SD card transfer, QR animation (BBQr, UR), NFC. Build and verify one SeedSigner yourself; it's cheap and it teaches you more about signing than reading ever will.

### Backup engineering

- BIP39 mnemonics, passphrases (the 25th word), and the ways passphrases destroy funds when documented badly
- **SLIP39 / Shamir** — and the honest case _against_ it for most clients: added complexity usually exceeds added safety
- Metal backup products, and the failure modes of each (fire rating, crush, corrosion)
- What goes in the recovery package: descriptor, xpubs, quorum, device list, passphrase location, step-by-step instructions written for someone who is grieving and not technical

### Inheritance and timelocks

- **Liana** — timelock-based wallets with degrading spending conditions. Study it closely; it's the most practical inheritance tool available and almost nobody in your market knows it exists.
- **Nunchuk** inheritance features
- Miniscript policies for dead-man-switch designs
- The legal layer: how this interacts with a will, an executor, a trust. You are not a lawyer — build a referral relationship with an estate attorney and say so explicitly to clients.

### The key ceremony as a product

Design and document a repeatable procedure: air-gapped environment, device verification, entropy generation, seed recording, descriptor export, verification spend, recovery rehearsal, signed documentation. Rehearse it end to end three times on signet before you ever run it for a client.

**Month 4 deliverable:** a written key ceremony protocol, a recovery documentation template in both languages, and three completed signet rehearsals including a full recovery from backup artifacts alone.

### The rule that protects your business

**Never take custody. Never hold a key. Never touch a client's seed.** You design, you document, you supervise, you verify — the client performs every key-generating and key-holding action themselves, and your contract says so in bold. The moment you hold key material you've acquired unlimited liability, probably triggered money-transmitter questions in multiple jurisdictions, and made yourself a physical target. This is the single most important business rule on this page.

---

# Month 5 — Commerce and community stacks

### BTCPay Server — study this deeply

The most commercially relevant single piece of software for LATAM merchant work. **Prague alone hosts 25+ in-person BTCPay merchants**, and the pattern replicates.

- Full self-hosted deployment, not the Docker one-click: understand NBXplorer, the database layer, the reverse proxy
- Store configuration, point-of-sale app, payment requests, pull payments
- Plugin ecosystem, Greenfield API for custom integration
- WooCommerce, Shopify and Medusa integrations
- Lightning backend selection and liquidity planning for a real merchant
- **Accounting exports and fiat conversion** — the question every merchant asks first and most consultants can't answer
- Refunds, partial payments, overpayment handling, expired invoices

### Community and federated stacks — the LATAM differentiator

- **Fedimint**: federated ecash with guardian-based custody. This is the most interesting thing happening for LATAM community banking — a village-scale institution where no single person holds the keys. Learn guardian setup, threshold configuration, the gateway to Lightning, and the trust model's real limits.
- **Cashu** mints: simpler, single-operator ecash. Appropriate for smaller communities.
- **Galoy / Blink** stack: the open-source infrastructure behind Bitcoin Beach. If you ever get a circular-economy engagement, this is the reference implementation.
- Study the existing projects in detail — Bitcoin Beach (El Zonte), Bitcoin Jungle (Costa Rica), Bitcoin Lake (Guatemala), Praia Bitcoin (Brazil). Read their postmortems, not their marketing. The failure patterns are more instructive than the successes.

### Privacy, current state

Be accurate here, because the landscape changed. Samourai's coordinator was seized and Wasabi shut its coordinator down — **the CoinJoin era is substantially over** and consultants still recommending it are working from stale information. What remains:

- Coin control and UTXO hygiene as the primary practical defense
- **BIP329** label export — portable labels across wallets
- **Payjoin** (BIP78, and v2 which removed the receiver-online requirement)
- **Silent payments** (BIP352) — reusable addresses without address reuse
- Honest conversation about chain surveillance capability, which is considerable

**Month 5 deliverable:** a deployed BTCPay instance with a working POS demo you can hand a merchant, and a Fedimint federation running on signet.

---

# Month 6 — Credentials, positioning and first clients

### Credentials worth having

There's no meaningful certification in this field, so credibility comes from demonstrable work and community standing.

|What|Why it matters|
|---|---|
|**Mi Primer Bitcoin — Bitcoin Diploma**|Salvadoran nonprofit, free, Spanish-language, enormous LATAM community credibility. Consider becoming a certified educator; the network is the real asset.|
|**Base58** (base58.school)|Serious technical courses on protocol internals and multisig. The most respected paid training available.|
|**Chaincode Labs seminars**|Free, competitive admission, high signal|
|**Plan ₿ Network**|Free curriculum with Spanish material|
|**Librería de Satoshi**|Spanish-language technical content|

**Books:** _Mastering Bitcoin_ 3rd edition (Antonopoulos & Harding), _Mastering the Lightning Network_, _Programming Bitcoin_ (Song), _Grokking Bitcoin_.

### Regulatory groundwork

Necessary for credibility and for staying out of trouble. **Ten countries in the region now have formal crypto frameworks of some kind**, and divergence is significant:

- **Brazil** — 43.7% of regional value and the tightest regime; VASP registration under the central bank, and higher barriers that may prove difficult for smaller firms. Highest-value market, highest compliance burden.
- **Argentina** — mandatory exchange registration since 2025; high grassroots adoption, weak currency, strong self-custody culture among the wealthy
- **El Salvador** — **legal tender status was made voluntary in January 2025 to comply with a $1.4 billion IMF agreement**, though the state continues accumulating and holds 7,605 BTC as of March 2026. Still the best ecosystem and event calendar in the region.
- **Mexico** — Fintech Law; Bitso handles roughly 10% of US–Mexico transfers
- **Bolivia** — reversed its decade-long ban in June 2024

The line that matters commercially: **non-custodial technical consulting is not money transmission anywhere.** Stay unambiguously on that side and most of this becomes background knowledge rather than compliance obligation. Get a lawyer's opinion in writing for any jurisdiction where you take real revenue — I'm not one, and this is exactly the kind of question where a wrong guess is expensive.

### Productize

|Service|Scope|Indicative price|
|---|---|---|
|Node deployment + hardening|Hardware spec, install, Tor, Electrum, monitoring, docs, training|$1,500–3,500|
|Multisig design + key ceremony|Design, ceremony supervision, descriptor package, recovery rehearsal, documentation|$3,000–8,000|
|Inheritance architecture|Timelock design, heir documentation, attorney coordination, annual rehearsal|$4,000–10,000|
|Merchant Lightning + BTCPay|Full stack, POS, staff training, 30 days support|$2,500–6,000|
|Managed node operations|Monitoring, updates, backup verification, support hours|$200–600/month|
|Recovery audit|Verify an existing setup is actually recoverable|$800–2,000|

That last one is your best door-opener. Most people with significant holdings have a setup they've never tested. Offering to prove it works — or find out that it doesn't — is an easy first yes and converts to everything else.

### Market entry

- **Conferences**: Adopting Bitcoin (San Salvador, typically November), Labitconf (Argentina), Satsconf (Brazil), Bitcoin Medellín. Go to one in person; this ecosystem runs on personal relationships and almost nothing else.
- **Content in Spanish.** Technical Bitcoin content in Spanish at the professional level barely exists. Document your multisig rehearsals, your BTCPay deployments, your Fedimint experiments. This is the same play as the AI business and the same audience-building mechanism.
- **Local first.** Denver's Hispanic business community, Bitcoin meetups, and any local wealth managers with crypto-holding clients who don't know how to advise them.

---

## The strategic connection you should exploit

This roadmap and the private-AI-deployment plan you asked about earlier share a customer and a pitch: **sovereign infrastructure for people who can't or won't put sensitive things in someone else's cloud.** Same buyer psychology, same Linux skills, same bilingual advantage, same on-premises install-and-maintain service model, often literally the same client — a law firm that wants private AI is a law firm whose partners might also hold bitcoin.

Don't run them as two businesses. Run one practice with two service lines and let each fund the other's slow months.

---

## Honest risks

**The node market alone is small and shrinking in relative terms.** The data above is clear that LATAM's mass market went to exchanges and stablecoins. Bet on custody engineering and merchant infrastructure; treat node installation as a lead-in.

**Collection from LATAM clients is genuinely hard.** Currency controls, banking friction, willingness to pay. Price in dollars, take payment up front, and weight your pipeline toward the US diaspora early.

**Liability is real.** A multisig you designed badly loses somebody's savings. Get E&O insurance, cap liability in your contract, never touch keys, and document everything you told the client and everything they decided.

**Physical security.** Being publicly known as "the guy who sets up Bitcoin cold storage for wealthy people" carries a risk profile that Linux consulting doesn't. Be thoughtful about how publicly you associate specific clients with specific holdings — which is to say, never.

---

Want me to expand any month into a week-by-week plan, draft the key ceremony protocol document, or work up the bilingual recovery documentation template that clients would actually hand to their heirs?