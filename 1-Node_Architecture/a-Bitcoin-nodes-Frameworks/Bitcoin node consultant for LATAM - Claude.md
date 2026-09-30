Your earlier framing was "Bitcoin node consultant for LATAM." This one adds a constraint that changes the skill list: **online**. Worth being explicit about what that rules in and out before the audit, because it determines which skills are worth six months of your life.

## What "online" decides

Fully deliverable remotely: node deployment over SSH into a client's hardware or VPS, BTCPay and Lightning merchant setup, managed monitoring and operations, recovery audits, supervised key ceremonies over video, training and documentation.

Not deliverable remotely: physically handling hardware signers, hardware procurement and delivery inside LATAM (customs alone will defeat you), anything requiring you to be in the room.

The consequence: your product mix should lean toward **recurring managed operations and merchant infrastructure**, with custody work delivered as _supervised_ ceremonies where the client does every physical action and you verify. That's a real methodology you'll need to build, and almost nobody has written it down. It's also the thing that makes an online custody practice possible at all.

Two more things "online" forces that people skip:

**Getting paid.** Bank transfers into and out of LATAM are slow, expensive and sometimes capital-controlled. Take payment in bitcoin or Lightning. You're selling Bitcoin infrastructure; being unable to accept it is a credibility problem, and it solves the collection issue entirely. Have a USD fallback (Wise, Stripe) for clients who need an invoice for accounting.

**Async support.** You'll be supporting clients across four time zones with no ability to walk over. That means your documentation has to be good enough to answer questions you're not awake for. Documentation stops being a deliverable and becomes a core competency.

---

# The skill audit

Three tiers. Be honest about which row you're in — the plan below allocates time accordingly.

## Tier 1 — Have it, needs validation (review, don't relearn)

|Skill|Self-test|Gap risk|
|---|---|---|
|Linux administration|Can you harden a public-facing box from memory: firewall, fail2ban, unattended-upgrades, SSH key-only, full-disk encryption with remote unlock?|Low|
|Command line|Comfortable with `systemd` units, `journalctl`, `ss`, `nft`, process tracing?|Low|
|Docker / Compose|Can you write a Compose file from scratch, debug a container network, and explain what Umbrel's `app_proxy` does?|**Medium**|
|Node installation|You've done bare, Umbrel, MyNode. Can you explain the tradeoffs to a client in one minute each?|Low|
|Backup / restore|Have you ever performed a full restore onto different hardware and timed it?|**High if never tested**|
|Spanish + English|Native Spanish, fluent English|None — this is your moat|

## Tier 2 — Partial, needs a real upgrade

|Skill|Where you likely are|Where you need to be|
|---|---|---|
|Bitcoin Core configuration|Installed it, used defaults|Index economics, `assumeutxo`, pruning tradeoffs, descriptor wallet migration, Guix signature verification|
|Python|Basic syntax|Type hints, `uv`, `pydantic`, FastAPI, `pytest`, packaging — enough to ship a client tool|
|Monitoring|Probably none in production|Prometheus + Grafana + alerting that reaches your phone|
|Technical Spanish|Native speaker, but Bitcoin vocabulary varies by country|Calibrated: _billetera_ vs _cartera_ vs _monedero_, _semilla_ vs _frase de recuperación_, and which terms your client's country actually uses|

That last row is easy to dismiss and shouldn't be. Technical Spanish is regionally fragmented, and using Argentine phrasing with a Mexican client marks you as an outsider in exactly the moment you need to be trusted.

## Tier 3 — Missing, must acquire

|Skill|Why it's required|
|---|---|
|**Protocol literacy** — UTXO model, output descriptors, PSBT, miniscript, Taproot|You cannot debug a failed recovery from the sysadmin layer. This is the largest gap and the one that limits everything else.|
|**Multisig design and key ceremony**|The highest-paid work in the field|
|**Inheritance and timelock architecture**|Wealthy clients' actual fear; nobody in your market offers it|
|**Lightning operations**|Channel management, liquidity, backup semantics|
|**BTCPay Server**|The merchant product — your most repeatable remote sale|
|**Remote delivery methodology**|Supervised ceremonies, verification protocols, async support. Doesn't exist as a discipline; you'll have to invent your version.|
|**Consulting business mechanics**|Scoping, pricing, contracts, liability limits, saying no|

---

# The six months

Assume 12–15 hours a week. Each month has four tracks: what you **review**, what you **acquire**, what you **build** (an artifact that exists afterward), and how you **prove** it.

---

## Month 1 — Protocol literacy and audit

The month that makes everything else possible. Resist the urge to skip to the fun parts.

**Review**  
Your existing lab. Rebuild the bare node from scratch on the desktop, from source, with verified signatures. Time it. Document every step. This tells you what you actually remember versus what you looked up last time.

**Acquire**  
Work through _Learning Bitcoin from the Command Line_ (Blockchain Commons, free). Target genuine comfort with:

- UTXO model, transaction structure, weight vs vbytes
- **Output descriptors** — the single most important gap. A seed phrase alone does not recover a multisig; the descriptor is the backup. You will build a business partly on explaining this.
- **PSBT** — construct, sign and finalize one by hand on signet
- **Miniscript** basics — needed for timelock designs later
- Fee mechanics: RBF, CPFP, why payments get stuck and how to unstick them

**Build**  
A reproducible lab in Docker Compose, versioned in git: regtest for iteration, signet for realistic multi-party testing, mainnet pruned for reference. This repo becomes your deployment tooling.

**Prove**  
Build a descriptor for a 2-of-3 on signet, fund it, then recover it on a clean machine using only the descriptor and two seeds. If you can't, you're not ready for Month 4.

---

## Month 2 — Node operations to professional grade, and remote delivery

**Review**  
Docker and Compose depth. Deconstruct Umbrel properly (the method I laid out earlier). Then run one Umbrel app standalone outside Umbrel, with every variable resolved by hand. This is the exercise that converts "I installed it" into "I understand it."

**Acquire**

- Bitcoin Core config: `txindex`, `blockfilterindex`, `coinstatsindex` and what each costs; `assumeutxo` and its security model; pruning and what it forecloses; descriptor wallet migration (a billable service _today_, for clients sitting on legacy wallets)
- Electrum servers: `electrs` vs `Fulcrum`, and their resource curves — enough to spec hardware from a client's requirements
- Tor, reverse proxy with automatic TLS (Caddy), `mempool.space` self-hosted
- Prometheus + Grafana with a Bitcoin Core exporter, and alerting that actually reaches you
- **Tailscale** — this is your remote-delivery backbone. Client boxes join your tailnet; you administer without exposing a single port.

**Build**  
A one-command deployment: Core + Fulcrum + mempool.space + Grafana + Tor + Caddy, from your repo, in under an hour. Documented in Spanish and English.

**Prove**  
Deploy it onto a fresh VPS you've never touched, from a different machine, entirely over SSH. That's the actual delivery motion of your business. Time it, then break it deliberately and write down every failure signature. That document becomes your troubleshooting playbook and is worth more than the deployment script.

---

## Month 3 — Lightning and the merchant product

Your most repeatable remote sale, and the one with the clearest LATAM demand.

**Review**  
Nothing. This is new territory.

**Acquire**

- LND vs Core Lightning vs Eclair — when each is appropriate, and why "because Umbrel defaults to LND" isn't an answer
- Channel and liquidity management; inbound vs outbound; why a merchant needs inbound
- **Backup semantics**, and this is the one that loses client money: an SCB is not a seed phrase. Restoring force-closes channels; restoring a stale one can lose funds. Understand this cold.
- **BTCPay Server** deployed properly, not via one-click: NBXplorer, the database layer, reverse proxy, store config, POS app, Greenfield API, WooCommerce integration, accounting exports, refunds and overpayment handling
- LNbits for community and small-merchant deployments
- Submarine swaps for liquidity (Boltz is implementation-agnostic and works without an account, which matters for LATAM clients)

**Build**  
A BTCPay instance on a VPS with a working POS demo you can screen-share to a prospect in five minutes. This is your primary sales asset.

**Prove**  
Take a real payment through it. Then refund it. Then handle a partial payment and an expired invoice. Merchants ask about all three within the first week.

---

## Month 4 — Custody and the remote ceremony

Highest value, and where the online constraint forces genuine innovation.

**Review**  
Your descriptor work from Month 1. You'll need it fluently now.

**Acquire**

- Multisig design: quorum selection, geographic key distribution, vendor diversity (never all keys on one hardware brand)
- Hardware signers hands-on: Coldcard, BitBox02, Jade, Trezor, and especially **SeedSigner and Krux** — DIY, stateless, buildable from parts, which matters enormously where import duties and customs make a Coldcard impractical
- Air-gapped workflows: SD card, animated QR (BBQr, UR), NFC
- Backup engineering: BIP39 passphrases and how they destroy funds when documented badly; the honest case _against_ Shamir for most clients
- **Liana** — timelock-based inheritance wallets. The most practical inheritance tool available and nearly unknown in your market.

**Build — the differentiating artifact**

A **remote key ceremony protocol**. Nobody has written this properly. Yours should specify:

- Pre-ceremony: environment checklist the client verifies, device authenticity verification over video, what the client must have physically present
- During: the client performs every action; you observe via screen share and camera, never touching key material
- Verification: a test spend on-chain before funds move, descriptor export and independent verification, recovery rehearsal from backup artifacts alone
- Documentation: a recovery package written for a grieving non-technical heir, in both languages
- Your contract language: you never see a seed, never hold a key, never take custody

**Prove**  
Run three full rehearsals on signet, remotely, with a friend or family member acting as client. Time them. The third one should be smooth. If it isn't, run more.

**The rule that protects the business:** never take custody, never hold a key, never touch a seed. Design, document, supervise, verify. The moment you hold key material you've acquired unlimited liability, likely triggered money-transmitter questions across several jurisdictions, and made yourself a physical target.

---

## Month 5 — Productize, automate, document

The month that converts capability into a business.

**Review**  
Everything you built. Package it.

**Acquire**

- Python to deliverable level: type hints, `uv`, `pydantic`, FastAPI, `pytest`. Enough to ship a small client-facing tool — a monitoring dashboard, a backup verifier, a status page.
- Business mechanics: scoping, fixed-price packages, 50% up front, limitation of liability, termination and data return
- **Regulatory literacy** for your target countries. The line that matters: non-custodial technical consulting is not money transmission anywhere. Stay unambiguously on that side and most compliance becomes background knowledge rather than obligation. Get a written lawyer's opinion for any jurisdiction where you take real revenue — I'm not one, and a wrong guess here is expensive.

**Build**  
Your service catalogue, as fixed packages rather than custom projects:

|Service|Delivery|Indicative|
|---|---|---|
|Recovery audit|Fully remote, video + screen share|$800–2,000|
|Node deployment + hardening|Remote, client's VPS or hardware|$1,500–3,500|
|BTCPay + Lightning merchant stack|Fully remote|$2,500–6,000|
|Supervised multisig ceremony|Remote, your protocol|$3,000–8,000|
|Inheritance architecture|Remote + attorney coordination|$4,000–10,000|
|**Managed operations**|Remote, recurring|**$200–600/month**|

The bolded row is the actual business. Ten managed clients at $400 is $4,000/month for maybe 20 hours of work, and it's the only line that compounds. Everything else exists to acquire managed clients.

**Prove**  
Write the contract, get it reviewed, and set up bitcoin/Lightning payment for it. Accepting payment through your own BTCPay instance is both practical and the best possible demo.

---

## Month 6 — Market entry and Spanish content

**Review**  
Your Spanish technical vocabulary, deliberately. Read Spanish-language Bitcoin documentation from several countries and note the divergences. Build a glossary with regional variants.

**Acquire**

- **Mi Primer Bitcoin** — the Salvadoran nonprofit's Bitcoin Diploma. Free, in Spanish, and the community credential that carries weight across LATAM. Consider the educator certification; the network is the real asset.
- **Base58** for protocol and multisig depth if you want the serious technical credential
- Content production: you don't need to be good at video, you need to be consistent

**Build**  
Spanish-language technical content, weekly, documenting exactly what you built in months 1–5. Not marketing — technical writeups. _"Cómo desplegué un nodo Bitcoin con Electrum server y monitoreo remoto"_ is content and lead generation simultaneously.

The niche to own: **professional-level Bitcoin infrastructure content in Spanish.** It barely exists. There's plenty of "qué es Bitcoin" and almost nothing on running production infrastructure.

**Prove**

- One paid engagement closed, even at a deliberately low price
- Ten published pieces
- Present once: a local Denver meetup, an online LATAM community, a Hispanic Chamber event
- If timing works, attend **Adopting Bitcoin** in San Salvador (typically November) — this ecosystem runs on personal relationships and nothing else

---

# The skills nobody puts on these lists

**Sales.** Nothing in a 30-year IT career prepares you for it. You will be bad at it for a year. Most technically excellent consultants fail here, not on delivery. Budget one non-negotiable hour a week from Month 1, not from Month 6.

**Saying no.** Scope creep kills fixed-price consulting. Learn to say "that's outside this package, here's what it would cost" without apologizing.

**Written explanation for non-technical readers.** Your recovery documentation will be read by someone's widow. That's a writing skill, and it's distinct from writing documentation for engineers.

**Knowing what you don't know.** The moment a client's question touches tax, law or estate planning, the correct answer is "I don't advise on that, here's someone who does." Build those referral relationships in Month 5, before you need them.

---

# Monthly checkpoints

Don't advance until each is true.

|End of|You can|
|---|---|
|Month 1|Recover a 2-of-3 on signet using only the descriptor and two seeds|
|Month 2|Deploy a hardened full stack to a fresh VPS, remotely, in under an hour|
|Month 3|Take, refund and troubleshoot a real Lightning payment through your own BTCPay|
|Month 4|Run a remote key ceremony end to end without touching key material|
|Month 5|Hand a prospect a fixed-price proposal and a contract|
|Month 6|Point to one paid engagement and ten published pieces|

And one honest gate at Month 6: did you enjoy it? You're retired. An unpleasant business that nets $3,000 a month is a bad trade. This plan is worth executing only if the work itself holds your interest — and if it does, the revenue arrives on a longer timeline than six months anyway.

---

If it'd help, I can put this in a document you can track against and check off, or draft the remote key ceremony protocol from Month 4 — that's the piece with no existing template and the one that would differentiate you fastest.