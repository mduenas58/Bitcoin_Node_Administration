Hardening a Bitcoin node from an OPSEC (Operational Security) perspective is fundamentally about **denying an adversary the information they would need to act against you**—whether that's a remote attacker trying to compromise your node, a surveillance firm mapping your IP to your Bitcoin holdings, or a physical threat actor who knows you hold value. OPSEC is threat-model-driven: you can't defend everything against everyone, so you must first name what you're protecting and from whom, then apply countermeasures accordingly.

Below is a structured breakdown of the key layers.

---

## 1. Network Privacy: Hiding Your Node's Location

The most immediate OPSEC leak from running a node is your **IP address**. Without mitigation, your node advertises your real location to every peer it connects to.

### Route All Traffic Through Tor
- **Bitcoin Core supports Tor natively.** You can run your node as a Tor onion service, meaning inbound connections reach you through a `.onion` address without ever knowing your real IP.
- Starting with Bitcoin Core 22.0, only **Tor v3** hidden services are supported (v2 addresses are ignored).
- The critical configuration distinction: use the `proxy` option to route **all clearnet-bound traffic** through Tor. The `onion` option alone only allows you to reach Tor peers via hidden services—it does **not** proxy your regular traffic.

### Consider a VPN (With Caveats)
- A VPN adds a layer between your ISP and your node, but **a VPN is not privacy by itself**. You're simply shifting trust from your ISP to the VPN provider. Audit any provider's no-logs claims rather than reading their marketing.
- For stronger setups, configure the VPN on your **router** or a dedicated bridge adapter, not just on the node itself. This prevents leaks if the VPN drops.

### Firewall Configuration
- **Block all incoming connections by default.** Only open what you explicitly need.
- For a node that does not accept inbound connections, you need **no open ports at all** on the firewall. Use `ufw` to deny everything and allow only outbound traffic.
- If you do accept inbound connections (to support the network), open **only port 8333/TCP** and nothing else. Place the node in a separate VLAN from your normal LAN devices.

### Disable Incoming Connections (Optional)
- Setting `listen=0` in `bitcoin.conf` disables inbound connections entirely. The node still connects outbound to peers.
- From a pure security standpoint, the risk is roughly the same whether you accept inbound connections or not. However, **disabling inbound connections hides your node from the network's address gossip**, which reduces your exposure to targeted scanning.

---

## 2. System Hardening: Locking Down the Host

### Full Disk Encryption (Table Stakes)
- Full-disk encryption is the **baseline** for any Bitcoin node. It protects against theft, resale, repair-shop access, seized hardware, and any situation where the machine is powered off but still contains sensitive keys, backups, logs, or config files.
- It does **not** protect you while the node is unlocked and running. For that, you need additional layers.
- For higher-threat scenarios, consider hidden volumes or self-destruct mechanisms using tools like VeraCrypt.

### SSH Hardening
- **Disable password authentication entirely.** Use Ed25519 key-based authentication only.
- **Disable root login** via SSH (`PermitRootLogin no`).
- **Change the default SSH port** from 22 to a random high-numbered port. This reduces automated bot attack noise by over 90%.
- **Restrict SSH access to trusted IPs only** at the firewall level. Never expose SSH to the open internet.
- Use **Fail2Ban** to automatically ban IPs that repeatedly fail authentication.

### Systemd Service Hardening
If you run `bitcoind` as a systemd service (recommended), apply sandboxing directives to limit what a compromised daemon can access:
- `NoNewPrivileges=true` — prevents privilege escalation
- `PrivateTmp=true` — isolates temporary files
- `ProtectSystem=strict` and `ProtectHome=true` — makes most of the filesystem read-only
- `MemoryDenyWriteExecute=true` paired with `SystemCallArchitectures=native` — prevents memory-based exploits from circumventing protections
- `PrivateDevices=true` — restricts device access

These settings follow systemd's "strict" security profile and significantly reduce the attack surface if `bitcoind` is compromised.

### Encrypt Sensitive Data at Rest
- Even with full-disk encryption, consider **file-level encryption** (e.g., `gocryptfs`) for especially sensitive files like wallet seeds, LND backups, and configuration files containing API keys. This locks them even while the system is running.
- For Lightning nodes, automate **encrypted backups** of channel states and macaroons using GPG encryption with cloud redundancy.

---

## 3. Operational Practices: The Human Layer

OPSEC is a **habit, not a configuration**. The most sophisticated technical setup fails if you leak information through your behavior.

### Identity Compartmentalization
- **Never broadcast your holdings**, online or in person. Keep your financial identity strictly separated from your social identity.
- Use **pseudonymous identities** for any public Bitcoin activity. Do not link your node's operation to your legal name, home address, or social media accounts.
- **Take deliveries of hardware** (node hardware, wallets, etc.) in ways that do not tag your home address as a target—use a PO box, a locker, or a trusted third party.

### Physical Security Awareness
- A node or mining setup adds a **physical signature**: heat plume, noise profile, power draw that a utility can see. Know what each activity reveals and decide deliberately what to accept.
- Consider **where the node is physically located**. If someone breaks in, can they grab the machine and walk away with your keys? Full-disk encryption helps here, but only if the machine is powered off.

### Update Discipline
- **Regularly update Bitcoin Core, your OS, and all dependencies.** Vulnerabilities are discovered and patched continuously. A recent example: Bitcoin Core 31.1 patched an IP address leak in a privacy feature—operators had to fully shut down their node before installing the new binaries to benefit from the fix.
- When a critical patch drops, **act quickly**. Node managers leaking full-control credentials have been documented; rotate every Lightning macaroon before one leaks.

### Backup Validation
- A backup you haven't **tested** is not a backup. Regularly restore your node's wallet and configuration from backups in a clean environment to verify they actually work.
- Store backups **offline** and **encrypted**. Never leave unencrypted seed phrases or wallet files on a networked machine.

---

## 4. Privacy Within the Node Itself

### Separate Wallets from Node Identity
- Connecting your wallet to your **own node** means you're not divulging your IP address, your Bitcoin addresses, or your balances to a third-party server. But if your wallet software queries a public Electrum server (even over Tor), you're still leaking that information.
- Run a **private Electrum server** (Fulcrum, Electrs) alongside your node so your wallet queries stay local.

### Be Careful with Transaction Broadcasting
- When you broadcast a transaction, the first node to see it can potentially infer that it originated from you. If your node is not configured to accept incoming connections, you may be the **only** node that sees your transaction first—making it easy to link the transaction to your IP.
- Bitcoin Core 31.0 had a privacy feature (`privatebroadcast`) that was found to have an IP leak in certain configurations. The fix in 31.1 required a full shutdown. As a workaround during the vulnerability window, developers recommended disabling `privatebroadcast`, using only v1 transport, or routing all IPv4/IPv6 traffic through Tor.

### Address Reuse and Coin Consolidation
- On-chain privacy is part of node OPSEC. **Address reuse** and **careless coin consolidation** can link your cold storage to your public identity. Tools like CoinJoin exist precisely to break those linkages.

---

## 5. OPSEC Checklist (Quick Reference)

| Layer | Action | Priority |
|---|---|---|
| **Network** | Route all traffic through Tor (`proxy` option, not just `onion`) | Critical |
| **Network** | Firewall: deny all inbound, allow only needed outbound | Critical |
| **Network** | Disable inbound connections if you don't need them (`listen=0`) | Medium |
| **Host** | Full-disk encryption | Critical |
| **Host** | SSH: key-only auth, no root login, non-standard port, IP-restricted | Critical |
| **Host** | Fail2Ban for brute-force protection | High |
| **Host** | Systemd sandboxing (`NoNewPrivileges`, `ProtectSystem`, etc.) | High |
| **Data** | File-level encryption for seeds, backups, API keys | High |
| **Data** | Encrypted, offline, tested backups | Critical |
| **Ops** | Never link financial identity to social identity | Critical |
| **Ops** | Pseudonymous public presence | High |
| **Ops** | Regular updates and prompt patching | Critical |
| **Ops** | Physical security awareness (deliveries, heat/noise, location) | Medium |
| **Privacy** | Run private Electrum server; avoid public wallet queries | High |
| **Privacy** | No address reuse; careful coin consolidation | Medium |

---

## The Core Principle

The dangerous leaks are rarely the obvious ones. OPSEC works through an **aggregation lens**: individually trivial data points—your routines, purchases, online handles, package deliveries, offhand comments—combine into an actionable picture. Your node's IP, your wallet's address queries, your update schedule, and your physical routine each seem harmless alone. Assembled, they answer an adversary's three questions: **what do you have, where is it, and when are you vulnerable**.

Consistency beats intensity. One lapse—a single photo of your seed phrase, one wallet query to a public server, one reused address—can undo years of discipline. Build sustainable habits, revisit your threat model as circumstances change, and treat OPSEC as an ongoing process rather than a one-time configuration.