# Remote Multisig Key Ceremony Protocol

· @Manuel Duenas

This protocol lets a consultant design, supervise and verify a multisig wallet without ever seeing key material. The client performs every action that touches a seed; the consultant observes, verifies through public data, and proves the result works before any real funds move. Four sessions, roughly five hours total, delivered entirely over video.

## The custody line

Everything in this protocol follows from one rule: **you never see key material, and the client performs every action that touches it.** Not as a best practice — as the structural property that makes remote delivery possible and keeps you out of custody, out of money-transmitter questions in several jurisdictions, and off a target list.

![](file:///Users/manuel/Library/Application%20Support/LibreOffice/4/user/temp/lu22649f332kn.tmp/lu22649f3334l_tmp_5512b4f5.png)  
  

The design problem this creates is real: if you cannot see the seeds, how do you know the client did it correctly? The answer runs through every later section. You verify entirely through **derived public data** — extended public keys, the descriptor, addresses independently displayed by each device — and then through a **test spend across every valid signing path**. Public data plus a working spend proves the private side is correct without ever exposing it.

### The four things that make this work remotely

1. **Public keys prove private keys.** An xpub is safe to transmit and uniquely determines the keys behind it. If three devices produce three xpubs that combine into a descriptor which produces an address all three devices independently confirm, the setup is correct.
    
2. **A test spend proves the quorum.** For a 2-of-3 there are three valid signing pairs. Exercise all three on a small amount and you have proven every recovery path a future signer could need.
    
3. **A wipe-and-restore proves the backups.** The only way to know a seed backup works is to destroy the device state and rebuild from the written words. Anything less is a hope.
    
4. **A signed session log proves what happened.** You document each step and the client countersigns. This is your liability record and the heir's provenance trail.
    

### Camera discipline

The video call is the delivery mechanism and the single largest risk in the protocol. State these rules in writing before the first session and restate them aloud at the start of each one.

- Seed words appear **only** on the hardware signer's own screen. Never on a computer display, never typed into anything, never photographed.
    
- Before any device displays a seed, the client physically angles it away from the camera and confirms aloud. You look away. You say so.
    
- Screen sharing is limited to the coordinator software. The client shares a single application window, never the full desktop.
    
- **No recording.** Not by you, not by them, not by the platform. Disable cloud recording and transcription in the meeting settings and confirm it at the start of each session.
    
- If a seed enters the frame for even a moment, the ceremony aborts. That device is wiped and regenerated from scratch. Say this in advance so it is a known rule rather than an argument in the moment.
    

## Design decisions, settled before you schedule

These are decided in a paid design call, written down, and signed off before anyone buys hardware. Changing them afterwards means starting over.

### Quorum

|   |   |   |
|---|---|---|
  
|Quorum|Suits|Why|
|2-of-3|Individuals, couples, most clients|One key can be lost or destroyed with no loss of funds; one key can be stolen with no loss of funds. The right default.|
|3-of-5|Families, partnerships, businesses|Survives two simultaneous losses; supports distributed control across people|
|2-of-2|Almost nobody|No redundancy; a single loss is fatal|
|3-of-3|Nobody|Same failure, worse|

Start at 2-of-3 and require an argument to move off it. Every additional key adds a backup that must be maintained, verified annually and documented for an heir. Complexity that nobody maintains is worse than a simpler design that works.

### Vendor diversity

Never all three keys on the same hardware brand. A firmware flaw or a supply-chain compromise at one vendor should not be able to reach a quorum.

A workable 2-of-3 mix: one Coldcard, one BitBox02 or Jade, one SeedSigner or Krux. The last slot matters especially for LATAM clients — SeedSigner and Krux are built from generic parts, cost a fraction of a commercial signer, and avoid the import duties and customs delays that make a Coldcard impractical in several countries.

With a DIY signer in the mix, add a session before the ceremony for the client to build and verify it.

### Key geography

Write down, for each key, where the device lives and where its backup lives. They are different questions.

The test to apply: **no single event should reach a quorum.** A house fire, a burglary, a flood, a bank failure. If two keys sit in the same building, you have a 1-of-3 wearing a costume.

A common arrangement: one key at home, one in a bank safe deposit box, one with a trusted person or a second property. For clients in countries where bank access is politically uncertain, replace the safe deposit box with a second geography.

### Passphrase policy

The BIP39 passphrase is where more funds are lost than anywhere else in multisig, and the decision is binary.

**Default: no passphrase.** For a multisig, it adds a failure mode without adding meaningful security — an attacker already needs a quorum of devices, and the passphrase adds one more thing an heir can fail to find.

**If the client insists**, it must be documented as carefully as the seed itself, stored in a different location from the seed it belongs to, and included in the recovery package. A passphrase written on the same sheet as its seed provides nothing. A passphrase that exists only in someone's memory is a bearer instrument that dies with them.

Record the decision in the session log either way. It is the most common cause of an heir finding the seeds and still being unable to recover.

### Coordinator and descriptor policy

**Sparrow** as the coordinator: the best descriptor and PSBT handling available, and it connects to the client's own node or yours. **Nunchuk** if inheritance features are wanted and the client will use a phone.

Derivation: standard BIP48 native segwit multisig, `m/48'/0'/0'/2'`. Do not improvise paths. A non-standard derivation is a recovery obstacle for every future tool.

Decide now where the descriptor is stored, because **the descriptor is the backup**. Seeds alone do not recover a multisig. It goes in the recovery package, with each key's backup, and in your own records.

## The client preparation package

Sent at least a week before Session 1, in the client's language. The ceremony does not begin until every item is confirmed present. A client scrambling for a pen mid-session is a client making mistakes.

### What they buy and receive themselves

The client purchases every device directly from the manufacturer, never from a marketplace reseller, and receives it at their own address. You never touch the supply chain. If a device arrives and you handled it, its provenance is compromised and so is your position.

- Three hardware signers, different vendors, ordered direct
    
- Metal seed backup plates, one per key, from a reputable maker
    
- A stamping or punching tool if the plates require one
    
- Two microSD cards, new, for air-gapped transfer
    
- A computer capable of running the coordinator software
    
- A second device for the video call, so the computer's screen is free
    

That last item is not optional. Trying to run a screen share and a camera from one machine is where accidents happen.

### The room

- A private room, door closed, for the duration
    
- No other people present unless they are designated key holders
    
- Nothing reflective behind the seated position — a mirror, a window at night, a glass cabinet door
    
- Phone face down and out of reach; no smart speakers or cameras in the room
    
- Good light on the work surface, camera angled at the client's upper body rather than the desk
    

### Time blocked

|   |   |   |
|---|---|---|
  
|Session|Duration|Gap before the next|
|1 — Verification and key generation|90 min|At least a day|
|2 — Descriptor and address verification|60 min|Same day is fine|
|3 — Test spend, every path|60 min|Hours, for confirmations|
|4 — Recovery rehearsal|90 min|—|

Do not compress this into one day. Fatigue is the adversary in a key ceremony, and the gaps let the client absorb what they have done rather than perform it.

### Rules they agree to in advance

Send these as a separate one-page document and ask for written confirmation. Having them agreed in advance turns an awkward interruption into a rule they already accepted.

1. Seed words appear only on a hardware signer's own screen — never on a computer, never typed, never photographed.
    
2. Before any device shows a seed, the client angles it away from the camera and says so aloud.
    
3. The consultant will never ask to see a seed, and any request that appears to come from the consultant asking for one is fraudulent.
    
4. No recording of any session, by anyone.
    
5. If a seed is exposed to the camera, that key is wiped and regenerated. No exceptions and no discussion in the moment.
    
6. No funds move to the wallet until Session 3 completes successfully.
    

### What you prepare

- Session log template, one page per session, with space for the client's countersignature
    
- A signet or testnet rehearsal environment, so you can demonstrate any step before the client performs it for real
    
- The coordinator software installed and verified on your own machine, at the same version the client will run
    
- Verified download links and checksums for everything the client will install, sent in advance
    

That last point deserves emphasis. The client downloading Sparrow from a search result is a realistic attack vector. Send the link, send the signature, and walk them through verifying it in Session 1.

## Session 1 — Verification and key generation

90 minutes. The only session where key material exists in the open, and therefore the one with the strictest discipline.

### Opening, every session (5 min)

Read this aloud. Consistency is what makes it stick.

1. Confirm recording is off — platform settings, cloud recording, transcription, on both ends.
    
2. Confirm the room: door closed, alone, phone face down, nothing reflective behind them.
    
3. Restate the camera rules in full.
    
4. Confirm they have everything from the preparation package within reach.
    
5. State what this session will accomplish and what it will not.
    

### Software verification (15 min)

Before anything touches a key, the client verifies what they are running.

- Client downloads the coordinator from the link you sent, not from a search
    
- Client verifies the signature or checksum, on their machine, with you watching the output
    
- Client confirms the version matches yours
    
- Client connects the coordinator to a Bitcoin node — theirs, or one you deployed for them. **Not** a third-party public server, which would leak their entire wallet's addresses to an operator they do not know.
    

If signature verification fails, stop. Do not proceed with an unverified binary because the client is impatient.

### Device authenticity (20 min, per device)

Each device has its own procedure; know all three before the call.

|   |   |
|---|---|
 
|Check|What you watch for|
|Packaging|Tamper-evident seal intact, bag number matching the manufacturer's record where applicable|
|Firmware signature|Device reports genuine on first boot; the client reads the result aloud on camera|
|Version|Current firmware, updated before key generation if not|
|Supply chain|Client confirms on camera that they ordered direct and received it themselves|

Record each result in the session log. If any device fails, it does not get used — the client orders a replacement and that key waits for a later session. Do not substitute a device the client already had lying around.

### Key generation (40 min, roughly 12 per device)

For each device in turn:

1. **Client states the device and key position aloud.** "This is key 2, the BitBox, which will live in the safe deposit box."
    
2. **Client angles the device away from the camera and confirms.** You verbally acknowledge and look away. Say it: _"Confirmed, I am not looking at your device screen."_
    
3. **Client generates the seed on the device itself**, using the device's own entropy. Never a seed generated by software, never dice unless the client specifically wants it and you have rehearsed the procedure.
    
4. **Client writes the words to the metal backup immediately**, before doing anything else. Not to paper first with the intention of transferring later — that intermediate paper copy always survives longer than intended.
    
5. **Client verifies the backup by reading it back into the device**, using the device's own verification mode. A backup that has never been read back is an untested backup.
    
6. **Client confirms aloud** that the backup is complete, correct and verified.
    
7. **Client exports the xpub** to the microSD card or via QR, and sends it to you. This is public data and safe to transmit.
    
8. **You confirm receipt** and read the first and last four characters back so both parties have the same value on record.
    

Repeat for all three. Between devices, ask the client to take a moment. Rushing the third device after two successful ones is where errors concentrate.

### Close (10 min)

- Client stores each device and backup in its designated location before the next session, and confirms by message when done
    
- You record all three xpubs, the derivation path and every verification result in the session log
    
- You send the log; client countersigns
    
- **No funds move.** State this explicitly. Clients get excited after a successful generation session and the single most common protocol failure is a client funding the wallet before Session 3.
    

### Abort conditions

Stop the session immediately if any of these occur:

- A seed enters the camera frame — wipe and regenerate that device
    
- Anyone else enters the room who is not a designated key holder
    
- A device fails its authenticity check
    
- The client appears fatigued, distracted or under pressure — reschedule without negotiation
    
- The client asks you to hold a seed, photograph a backup, or "just keep a copy in case" — decline, and restate the custody line
    

## Session 2 — Descriptor and address verification

60 minutes. This is where you prove, without seeing a single seed, that all three devices hold the right keys and that the wallet is what everyone believes it is.

### Assemble the descriptor (15 min)

You build it from the three xpubs recorded in Session 1, on your machine, and share your screen as you do it. For a 2-of-3 native segwit multisig it takes the form:

```
wsh(sortedmulti(2,
```

Explain each part aloud as you build it. The client will not remember the syntax, but they need to understand that **this string, not the seed phrases, is what makes recovery possible** — and that it is public, safe to store anywhere, and must be present in every backup location.

Use `sortedmulti` rather than `multi`. It orders the keys deterministically, so recovery does not depend on anyone remembering which key was first.

### Import and independent confirmation (25 min)

This is the verification that replaces seeing the seeds.

1. **Client imports the descriptor into the coordinator.** The coordinator derives a first receive address.
    
2. **Client imports the descriptor into each hardware device in turn**, via microSD or QR. Each device now independently knows the wallet policy.
    
3. **Client asks each device to display the first receive address on its own screen**, and reads it aloud.
    
4. **All four values must match** — the coordinator and all three devices, character for character. Have the client read the first six and last six characters of each; check them against your copy.
    

If all four agree, you have proven, without ever seeing key material:

- each device holds a key that belongs to this wallet
    
- the descriptor is correct and complete
    
- the quorum and derivation path are what was designed
    
- no device was silently substituted between sessions
    

If any value disagrees, stop. The most common cause is the wrong derivation path on one device; the second most common is an xpub transcribed incorrectly in Session 1. Neither is recoverable by proceeding.

### Why the device display matters

The address must be read from the **hardware device's own screen**, not from the coordinator. A compromised computer can show the client any address it likes. The hardware device's screen is the only display in the room whose output the computer cannot forge, which is the entire purpose of a hardware signer.

Teach the client this explicitly. It is the habit that protects them every time they receive funds for the rest of the wallet's life.

### Record and close (20 min)

Into the session log and, later, the recovery package:

- The full descriptor, including its checksum
    
- All three master fingerprints
    
- The derivation path
    
- The first receive address, as confirmed on all four displays
    
- Which physical device corresponds to which key position and where it lives
    

Have the client save the descriptor to a location they control — a text file, a printed sheet, and eventually every backup location. Then send the log for countersignature.

Still no funds. Say it again.

## Session 3 — Test spend across every path

60 minutes plus confirmation waits. A 2-of-3 has three valid signing pairs, and a setup where only one has ever been exercised is a setup with two untested recovery paths.

### Fund with a test amount

The client sends a small amount — enough to spend meaningfully after fees, trivial to lose. Roughly 50,000 to 100,000 sats works.

The client sends it to the address confirmed on all four displays in Session 2. Watch the transaction confirm in the coordinator. Do not proceed until it has at least one confirmation.

### Exercise every combination

For a 2-of-3, three spends. Each uses a different pair and each must succeed independently.

|   |   |   |
|---|---|---|
  
|Spend|Signers|Proves|
|1|Key 1 + Key 2|The everyday path|
|2|Key 1 + Key 3|Recovery if key 2 is lost|
|3|Key 2 + Key 3|Recovery if key 1 is lost — including the case where key 1 was the one at home during the fire|

The third row is the one people skip, and it is the most important. Key 1 is usually the convenient device kept at home, which is also the one most likely to be destroyed or stolen. A wallet where the two remote keys have never signed together is a wallet whose actual disaster path is untested.

For each spend, the client:

1. Constructs an unsigned PSBT in the coordinator, sending back to a fresh address of the same wallet
    
2. Transfers it to the first signer by microSD or QR
    
3. **Verifies the destination address and amount on the device's own screen** before approving
    
4. Transfers the partially signed PSBT to the second signer
    
5. Verifies again on that device's screen
    
6. Finalizes and broadcasts from the coordinator
    
7. Confirms the transaction appears and confirms
    

Make step 3 and step 5 a spoken ritual. "Read me the address on the device screen." Every time. The habit you build here is the one that defends against a compromised computer later, and it only becomes automatic through repetition.

### Air-gap discipline

If using microSD, the card moves **only** between the coordinator machine and the signers, never to any other computer, phone or cloud location. If using QR, nothing else is in frame.

After the final spend, the client wipes and reformats both cards on camera.

### What failure tells you

|   |   |
|---|---|
 
|Symptom|Likely cause|
|A device refuses to sign|It does not have the descriptor imported, or has the wrong derivation|
|Signature produced but the transaction is rejected|Wrong derivation path on that key|
|Device shows an unexpected change address|Descriptor missing the change branch — check the `<0;1>` path component|
|One pair works, another does not|That key is not actually part of the wallet; return to Session 2 verification|

Any failure returns you to Session 2, not forward to Session 4. Diagnose it fully before moving on — a partially working multisig is more dangerous than an obviously broken one, because it will hold funds for years before revealing the defect.

### Close

Record in the log: all three transaction IDs, which keys signed each, and the client's confirmation that they verified addresses on-device each time.

Still no real funds. Session 4 comes first.

## Session 4 — Recovery rehearsal

90 minutes. The session almost every setup skips, and the only one that proves the backups are real rather than assumed.

### What is actually being tested

Everything so far has tested the wallet as it currently exists, with three working devices. Session 4 tests the scenario that actually happens: **a device is gone and someone has to rebuild from the metal plate.**

Until a backup has been read off the metal and used to reconstruct a working key, it is a stack of stamped letters that nobody has ever confirmed is correct. Verification inside the device at generation time proves the client copied it correctly; it does not prove the plate is legible, complete, or that the client can perform the restore under pressure.

### The wipe and restore

Pick one device — by preference the DIY signer or the least expensive, so the client is less anxious about it.

1. **Client confirms the metal backup for that key is physically in hand.** Not in the safe deposit box. In their hand, in the room.
    
2. **Client factory-resets the device on camera.** The device confirms it has been wiped.
    
3. **Client verifies the wipe** — the device no longer knows the wallet, and any attempt to sign fails.
    
4. **Client restores from the metal plate alone**, reading the words off the metal rather than from memory or any other copy. Camera discipline applies exactly as in Session 1: device angled away, you confirm you are not looking.
    
5. **Client re-imports the descriptor** and asks the device to display the first receive address.
    
6. **The address must match** the value recorded in Session 2.
    

A match proves the backup is correct, legible and sufficient. A mismatch means the backup is wrong, and you have just discovered it with 50,000 test sats at risk rather than the client's life savings.

### Then sign with it

Restoring is not enough. Run one more spend using the restored device plus one other, and confirm it broadcasts. A key that derives the right address but cannot sign has a problem you want to find now.

### The heir rehearsal

If there is a designated heir or co-signer who is not the client, bring them into this session and have **them** perform a signing operation, with the client watching and you guiding.

This is uncomfortable and it is the highest-value thirty minutes in the entire engagement. The heir discovers what they do not understand while there is still someone available to explain it. Every inheritance failure you will read about comes down to a document that was never rehearsed by the person who would need it.

If the heir cannot be present, record their required steps as a written walkthrough with screenshots from the test environment and include it in the recovery package.

### Restore the design

At the end of the session:

- Every device is back in its designated location or on its way there
    
- The wiped-and-restored device holds the same key it held before
    
- All three metal backups are confirmed present and returning to their separate locations
    
- The client confirms by message when each is in place
    

### Now funds can move

Only after Session 4 succeeds does the client move real value into the wallet, and they should do it in stages: a meaningful but survivable amount first, confirm it appears and can be spent, then the balance.

Sweep the test sats out as part of the final spend, or leave them — they cost less than the accounting.

### Annual re-rehearsal

Book the first anniversary before you end the call. A multisig that is never exercised decays: firmware ages, coordinator software changes its import format, metal plates corrode in a damp basement, and the client forgets the procedure. An annual repeat of Session 4 catches all of it, and it is the natural anchor for a retainer relationship.

## The recovery package

Written for one reader: a person who has just lost someone, has no technical background, and is holding this document because they have to. Every choice below follows from that.

Delivered in both languages, printed, with a copy stored at each key location and one with the client's attorney.

### Writing standard

- No jargon without a plain-language definition beside it on first use
    
- Short numbered steps, one action per step
    
- Photographs of each physical item so the reader can identify what they are looking for
    
- No links as the only source of anything — websites disappear, and this document may be opened in fifteen years
    
- Written assuming the reader will need help: it should tell them **what kind** of help and how to verify that the helper is legitimate
    

### Contents

**1. What this is.** One page, no jargon. "These funds are protected by three keys. Any two of them can access the money. Here is where they are and how to use them."

**2. The inventory.** Every key: which device, where the device is, where its metal backup is, who has access to that location, and a photograph of each.

**3. The descriptor.** Printed in full, with its checksum, and a plain-language explanation that this string is required and that the seed phrases alone are not enough. State it more than once. This is the single most common cause of a failed inheritance recovery.

**4. The passphrase**, if one exists. Where it is, how to find it, and an explicit statement that without it the funds cannot be recovered.

**5. Step-by-step recovery.** Numbered, with screenshots from the test environment. Two paths: recovery with the devices intact, and recovery from metal backups when a device is gone.

**6. Verification steps.** How the reader confirms they have done it correctly _before_ moving anything — the same address-matching check from Session 2, written for a non-technical reader.

**7. Who to call.** Your contact details, the attorney's, and — importantly — a statement of **what nobody will ever legitimately ask for**: nobody will ask them to type the seed words into a website, send them by email or message, or read them over the phone. Anyone doing so is stealing.

**8. Dated verification record.** A page listing each annual rehearsal, with the date and what was confirmed. This tells a future reader that the setup was working as of a known date, and by whom.

### The fraud warning is not optional

A grieving heir searching for help with a Bitcoin wallet is among the most targeted people on the internet. Put the warning early, repeat it at the end, and make it concrete:

> Nobody — not your bank, not a support service, not a person who contacts you — will ever need the words on the metal plates. If anyone asks for them, by any method, for any reason, they are attempting to steal these funds. There are no exceptions to this rule.

### What the package must not contain

- Seed words, in any form, in any language, partial or complete
    
- The passphrase itself, as opposed to instructions for finding it
    
- Total balance or holdings — the document will be read by people you did not choose, and a figure turns it into a target
    
- Anything that would let a reader who possesses only the document move funds
    

The package should be safe to lose. If losing it creates a security problem, it contains something it should not.

### Your obligation

You hold a copy of the descriptor and the session logs, and nothing else. State in the package that you can help reconstruct the wallet's structure but cannot access the funds, and that if you are unreachable the descriptor plus any two backups is sufficient for any competent Bitcoin professional to complete the recovery.

A recovery plan that depends on you being alive is not a recovery plan.

## Sign-off, terms and re-verification

### The session log

One page per session, countersigned by the client within 48 hours. It is your liability record, the heir's provenance trail, and the reference for every future engagement with this wallet.

Each page records: date, participants, devices verified and their results, actions performed by the client, public values exchanged, anything that failed and how it was resolved, and an explicit line confirming that no key material was disclosed to the consultant.

That last line matters more than it looks. It is the client's own signed statement of the custody boundary, which is the record you want if anyone ever asks what your role was.

### Contract terms that must be present

|   |   |
|---|---|
 
|Clause|Why|
|No custody|Explicit: consultant never receives, holds, stores or has access to any private key, seed or passphrase|
|Client responsibility|Client generates, records, stores and secures all key material; consultant advises and verifies only|
|Limitation of liability|Capped at fees paid. Non-negotiable for this work.|
|No investment or tax advice|You design infrastructure; you do not advise on holdings, tax or estate law|
|Attorney coordination|Inheritance work requires the client's own attorney; you coordinate, you do not replace|
|Scope|The four sessions, the descriptor, the recovery package. Anything else is a separate engagement.|
|Termination|What happens to the session logs and descriptor copy if either party ends the relationship|
|Death or incapacity|What happens to your records. Clients rarely ask; the ones who do are your best clients.|

Have a lawyer review this before the first engagement. I am not one, and the difference between a good and a bad limitation clause is the difference between a bad month and a bad decade.

### Insurance

Professional liability (errors and omissions) before you run a single ceremony. You are advising on the structure protecting someone's savings, and a design error — a derivation mistake, a backup instruction that turns out to be wrong — is a real exposure even with perfect custody hygiene.

### Abort conditions, consolidated

Stop and reschedule, at any point, if:

- Key material is exposed to the camera, to a screen, or to any networked device
    
- A device fails authenticity verification
    
- Anyone is present who is not a designated key holder
    
- The client is fatigued, distracted, intoxicated, or under time pressure
    
- Any verification value fails to match
    
- The client asks you to hold, photograph, store or receive key material — decline and restate the boundary
    
- You are not certain. Rescheduling costs an hour. Proceeding uncertainly can cost everything.
    

### The annual re-verification

Booked before the engagement ends, delivered as a retainer.

|   |   |
|---|---|
 
|Check|Why it decays|
|Wipe-and-restore on one device, rotating|Metal plates corrode; client procedure is forgotten|
|Signing test across every pair|Firmware updates change signing behaviour|
|Firmware currency on all three|Security fixes accumulate|
|Coordinator compatibility|Import formats and descriptor handling change between versions|
|Descriptor still present at every location|Copies go missing quietly|
|Key locations still valid|People move, banks close, relationships change|
|Heir walkthrough refresh|The heir forgets, or the designated heir has changed|

Price it as a fixed annual engagement. It is the recurring revenue that makes the practice viable, and it is genuinely the service the client most needs — a multisig that is never exercised is a multisig quietly rotting.

### One closing discipline

Rehearse this entire protocol on signet, end to end, at least three times before running it for a paying client. Play both roles. Time each session. Find the places where your explanation is unclear and the places where you reach for a step you have not written down.

The third rehearsal should be smooth. If it is not, run a fourth. The first client should never be the first time.