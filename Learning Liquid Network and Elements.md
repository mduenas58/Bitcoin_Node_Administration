# Liquid & Elements: 3-month learning plan

Oct 21, 2026 · @Manuel Duenas

## Overview

In 12 weeks (about 6–8 hours a week) you go from Bitcoin protocol knowledge to running Elements nodes, building Liquid wallets with LWK, and writing a first Simplicity contract.

- **Elements** is the open-source codebase (a fork of Bitcoin Core) that adds sidechain pegs, Confidential Transactions, issued assets and extra opcodes. It can sync Liquid (`-chain=liquidv1`), run a local regtest, or launch a custom chain.
- **Liquid** is the production federated sidechain built on Elements: about 1-minute blocks, 2-block finality, a federation of functionaries that signs blocks and controls the peg, L-BTC as the pegged bitcoin, and confidential amounts and assets by default.
- **Simplicity** has been live on Liquid mainnet since July 2025, programmed through the higher-level language SimplicityHL ([Blockstream blog](https://blog.blockstream.com/simplicity-launches-on-liquid-mainnet/)).

The plan follows three phases: Month 1 refreshes the Bitcoin internals Elements builds on and gets a node running; Month 2 covers what is new in Elements (confidentiality, assets, the peg); Month 3 is development, ending in a capstone project.

## Bitcoin skills to review

Elements inherits almost everything from Bitcoin Core, so gaps here become blockers later. Use the self-check to decide how much time each needs.

|   |   |   |
|---|---|---|
|Skill|Why it matters for Liquid / Elements|Self-check: can you…|
|UTXO model and transaction serialization|Elements transactions extend Bitcoin's format (asset, value and nonce commitments, witness extensions)|Decode a raw segwit transaction by hand?|
|Script and opcodes|Elements keeps Script and adds opcodes (introspection, 64-bit arithmetic, `OP_CAT` and others)|Write and trace a P2WSH multisig or timelock script?|
|SegWit and Taproot (BIP 341/342)|Liquid supports Taproot; tapscript is where the new opcodes live|Explain key-path vs script-path spends and build a Taproot tree?|
|Keys, HD wallets, descriptors (BIP 32/39/84/86, output descriptors)|Liquid wallets use CT descriptors, which extend Bitcoin descriptors with a blinding key|Write a descriptor and derive addresses from it?|
|PSBT (BIP 174/370)|Liquid uses PSET, the Elements version of PSBT v2|Walk a PSBT through creator, updater, signer, finalizer roles?|
|Elliptic-curve cryptography (secp256k1, Schnorr, ECDH, Pedersen basics)|Confidential Transactions rely on commitments, range proofs and ECDH-derived blinding|Explain what a commitment hides and how ECDH creates a shared secret?|
|Bitcoin Core RPC and `bitcoind` regtest|`elementsd` and `elements-cli` behave like Bitcoin Core; a peg-in lab needs both daemons|Spin up regtest, mine blocks and fund a wallet from the CLI?|
|Multisig and timelocks (CLTV/CSV)|The federation peg and emergency recovery keys are multisig and timelock constructions|Build a 2-of-3 with a CSV fallback path?|
|Consensus, mining and SPV proofs|Peg-ins are proven with Bitcoin merkle proofs; Liquid blocks are signed, not mined|Verify a transaction's merkle proof against a block header?|
|Lightning basics (optional)|Swaps between Liquid and Lightning (for example Boltz) are common in practice|Explain an HTLC and a submarine swap?|

## New skills to acquire

These are specific to Elements and Liquid, grouped by area.

|   |   |   |
|---|---|---|
|Area|Skill|What to learn|
|Architecture|Federated sidechains and two-way pegs|Strong federations, functionaries, watchmen, HSMs; peg-in (102 Bitcoin confirmations), peg-out flow; trust model vs Bitcoin and Lightning|
|Architecture|Signed-block consensus|Block signing by the federation, dynamic federations (DynaFed), 1-minute blocks and 2-block finality|
|Privacy|Confidential Transactions|Pedersen commitments, range proofs, surjection proofs, blinding and unblinding, explicit vs confidential outputs|
|Privacy|Blinding keys and confidential addresses|SLIP-77 master blinding keys, CT descriptors, confidential vs unconfidential addresses|
|Assets|Issued Assets|Asset issuance, reissuance tokens, burning, asset IDs and contract hashes, the Liquid Asset Registry|
|Assets|Securities and regulated assets|AMP (Blockstream Asset Management Platform) concepts: whitelisting and authorized transfers|
|Transactions|PSET and fee handling|Elements PSBT v2 fields, explicit fee outputs, L-BTC as policy asset|
|Scripting|Elements opcodes|Tapscript introspection opcodes, 64-bit arithmetic, `OP_CHECKSIGFROMSTACK`; covenants built from them|
|Scripting|Simplicity and SimplicityHL|Combinator model, jets, writing and testing contracts, program cost budget|
|Tooling|`elementsd` / `elements-cli`|Running liquidv1, liquidtestnet and regtest; asset and peg RPCs|
|Tooling|Liquid Wallet Kit (LWK)|Watch-only `wollet`, signers (software, Jade, Ledger), multisig, asset lifecycle; Rust, Python, Node and WASM bindings|
|Tooling|Explorers and indexers|Esplora / Electrs for Liquid, the Blockstream Liquid explorer, unblinding in the explorer|
|Ecosystem|Swaps and integrations|Atomic swaps, Liquid–Lightning swaps (Boltz), SideSwap, Green and Aqua wallets|
|Programming|Rust (recommended)|LWK, rust-elements and rust-simplicity are Rust; Python is enough for scripting the RPC and LWK bindings|

## Month 1 — Review and foundations (weeks 1–4)

Goal: close any Bitcoin gaps and understand Liquid's design well enough to explain its trust model.

|   |   |   |   |
|---|---|---|---|
|Week|Focus|Resources|Deliverable|
|1|Transactions, Script, SegWit, Taproot refresher|_Mastering Bitcoin_ 3rd ed. (ch. 6–7, 11, 14); _Learning Bitcoin from the Command Line_; BIPs 141, 341, 342|Hand-decode one segwit and one Taproot transaction from regtest|
|2|Descriptors, PSBT, ECC refresher|BIP 174/370 and descriptor docs in Bitcoin Core; _Programming Bitcoin_ (Jimmy Song) ch. 1–4|Build, sign and finalize a 2-of-3 PSBT on regtest with `bitcoin-cli`|
|3|Sidechains and Liquid architecture|Sidechains whitepaper (Back et al., 2014); Strong Federations paper (Dilley et al., 2016); Liquid docs "Technical overview"|One-page diagram of Liquid: functionaries, peg-in, peg-out, block signing|
|4|Install Elements, first chain|Elements GitHub README; elementsproject.org "Elements code tutorial"; Docker `blockstream/elementsd`|Run `elementsd` on regtest, send L-BTC between two wallets, inspect a transaction with `decoderawtransaction`|

**Checkpoint:** you can explain, without notes, how Liquid differs from Bitcoin in consensus, finality and trust assumptions.

## Month 2 — Elements core features (weeks 5–8)

Goal: master what Elements adds to Bitcoin, hands-on in a local lab.

|   |   |   |   |
|---|---|---|---|
|Week|Focus|Resources|Deliverable|
|5|Confidential Transactions|Greg Maxwell's CT write-up; _Confidential Assets_ paper (Poelstra et al., 2017); Elements CT tutorial|Send blinded and unblinded outputs; unblind one with `unblindrawtransaction` and explain each commitment|
|6|Issued Assets|Elements "Issued Assets" tutorial; Liquid docs on issuance and the Asset Registry|Issue, reissue and burn an asset on regtest; register a test asset's contract hash format|
|7|Peg-in and peg-out|Elements docs on federated pegs; Liquid docs "Peg-ins and peg-outs"|Run `bitcoind` + `elementsd` on regtest and complete a full peg-in (`getpeginaddress`, `claimpegin`) and a peg-out|
|8|Liquid testnet and real tooling|Liquid testnet faucet; Blockstream Green or Aqua wallet; Blockstream Liquid explorer|Sync `-chain=liquidtestnet`, receive testnet L-BTC, trace a confidential transaction in the explorer|

**Checkpoint:** you can draw a Liquid transaction's structure (inputs, asset and value commitments, range and surjection proofs, fee output) and explain why each part exists.

## Month 3 — Development and capstone (weeks 9–12)

Goal: build working software on Liquid and finish one project you can show.

|   |   |   |   |
|---|---|---|---|
|Week|Focus|Resources|Deliverable|
|9|Liquid Wallet Kit|[LWK book](https://blockstream.github.io/lwk/book/index.md); [LWK overview and examples](https://docs.liquid.net/v1/docs/lwk-overview-and-examples); `pip install lwk` or the Rust crates|Create a CT-descriptor watch-only wallet, then a 2-of-2 multisig that issues and spends an asset|
|10|Elements Script and covenants|Elements opcode docs (tapscript introspection, 64-bit arithmetic); rust-elements|Write a tapscript covenant that restricts where an output can be sent; test it on regtest|
|11|Simplicity and SimplicityHL|[simplicity-lang.org](https://simplicity-lang.org) docs and examples; Simplicity whitepaper (O'Connor, 2017); Simplicity SDK for local testing|Write, test locally and deploy a simple SimplicityHL contract (for example a timelocked or 2-of-3 vault) to Liquid testnet|
|12|Capstone|Everything above; community feedback|Ship one project (ideas below), with a README explaining design and trust assumptions|

**Capstone ideas** (pick one):

- A small LWK-based web or CLI wallet that shows unblinded balances per asset.
- A token issuance tool: issue an asset, publish registry metadata, distribute to several addresses.
- A SimplicityHL vault or escrow contract with a written threat model.
- A Liquid–Lightning swap integration using Boltz's API.

**Checkpoint:** a public repository with working code, tests and a clear write-up.

## Resources

Links marked as opened were checked on the as-of date; the rest are well-known references to search by title.

**Official docs and code (opened)**

- [Elements repository](https://github.com/elementsProject/elements) — source, chain modes, links to the code tutorial and Confidential Assets material
- [blockstream/elementsd Docker image](https://hub.docker.com/r/blockstream/elementsd) — fastest way to run a node
- [Liquid Wallet Kit book](https://blockstream.github.io/lwk/book/index.md) and [LWK overview and examples](https://docs.liquid.net/v1/docs/lwk-overview-and-examples)
- [Simplicity launches on Liquid mainnet](https://blog.blockstream.com/simplicity-launches-on-liquid-mainnet/) and [Building on Simplicity: what ships today](https://blog.blockstream.com/building-on-simplicity-what-ships-today-what-is-coming-next/)
- [simplicity-lang.org](https://simplicity-lang.org) — SimplicityHL docs, examples and SDK

**Other references (search by title)**

- elementsproject.org and docs.liquid.net — tutorials, RPC reference, peg and issuance guides
- _Mastering Bitcoin_, 3rd ed. (Antonopoulos and Harding) — free on GitHub
- _Programming Bitcoin_ (Jimmy Song)
- _Learning Bitcoin from the Command Line_ (Blockchain Commons, GitHub)
- Papers: _Enabling Blockchain Innovations with Pegged Sidechains_ (2014); _Strong Federations_ (2016); _Confidential Assets_ (2017); _Simplicity: A New Language for Blockchains_ (2017)
- Blockstream Liquid explorer and Esplora (blockstream.info/liquid)

**Community**

- Liquid Network Telegram (t.me/liquid) and Simplicity Telegram — announcements, bootcamps, hackathons
- blog.liquid.net — federation quarterly updates and development roadmap
- Bitcoin Stack Exchange (tags `liquid`, `elements`)