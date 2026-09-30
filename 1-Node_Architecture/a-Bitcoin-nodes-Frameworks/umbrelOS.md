Good instinct — and start with one finding that changes how you'd use it commercially.

## Before you start: the license

umbrelOS is open source but **licensed under PolyForm Noncommercial 1.0.0**, which prohibits commercial use. That's not a footnote for a consultant. Deploying umbrelOS for paying clients is arguably outside the license grant, and you don't want to discover that after building a practice on it.

Verify the current `LICENSE` file yourself before relying on this — licenses change and the stakes are legal rather than technical. But plan on Umbrel being a **reference architecture you learn from**, not a platform you resell. Which is a better use of it anyway.

Compare: RaspiBlitz is MIT, Start9's StartOS is MIT, nix-bitcoin is MIT, MyNode has a paid-tier model. Know each one's terms before you recommend it.

---

# The method: reconnaissance on any appliance distro

This generalizes. You'll do the same thing to StartOS, Citadel and RaspiBlitz, so learn the sequence rather than the Umbrel-specific answers.

The core question at every layer is the same: **what did they build, what did they wrap, and what did they decide for the user?**

### Phase 1 — Boot and process layer

Flash umbrelOS to a spare machine or VM, get SSH access, and start from PID 1:

```bash
# What actually starts at boot
systemctl list-unit-files --state=enabled
systemctl list-units --type=service --state=running

# The process tree tells you the real hierarchy
ps auxf

# What did they write vs what ships with Debian?
dpkg -l | wc -l
ls -la /etc/systemd/system/
```

The units in `/etc/systemd/system/` that aren't Debian packages are Umbrel's actual contribution. On umbrelOS you'll find `umbreld` there. Read it:

```bash
systemctl cat umbreld
journalctl -u umbreld --no-pager | head -100
```

That single service file tells you the working directory, the user it runs as, the restart policy, and the environment — which is most of the architecture in twenty lines.

### Phase 2 — Network layer

```bash
# Every listening socket and its owner
ss -tulpn

# Container networks and addressing scheme
docker network ls
docker network inspect umbrel_main_network

# Packet filtering — where does traffic actually get routed?
nft list ruleset        # or iptables -L -n -v --line-numbers
```

The question you're answering: how does a request to port 80 reach the right app container? Every appliance distro solves this differently, and it's the design decision that most constrains what you can do afterward.

### Phase 3 — Storage layout

```bash
lsblk -f
mount | column -t
df -h

# Partition scheme reveals the update strategy
fdisk -l
```

An A/B partition pair means atomic OTA updates with rollback. A single root means in-place updates. This determines how upgrades fail and how you recover them, which is exactly the kind of thing a client pays you to know.

### Phase 4 — The data directory

```bash
cd /home/umbrel/umbrel
tree -L 2
find . -name "*.yml" -o -name "*.yaml" -o -name ".env" | head -40
cat .env 2>/dev/null
```

### Phase 5 — Source reading

```bash
git clone https://github.com/getumbrel/umbrel
git clone https://github.com/getumbrel/umbrel-apps
git clone https://github.com/getumbrel/umbrel-os
```

Read commits, not just code. `git log --oneline | head -200` on the main repo shows you what they've been fixing, which tells you where the fragile parts are.

---

# What you'll find: umbrelOS architecture

### The layers

**Debian** at the base. Not a custom kernel, not a novel init — a standard Debian system with a purpose-built daemon on top. This is a deliberate choice worth noting: they optimized for maintainability over minimalism.

**`umbreld`** — the central backend daemon, written in TypeScript/Node, running under systemd. It handles user management, app store operations, app lifecycle, file management and system status, and **exposes a type-safe tRPC API to the React frontend**.

This is the single most important thing to understand about the 1.x architecture. In the old 0.5.x design, responsibility was scattered across several components — a Python manager, a Node middleware, a bash event-handler daemon, and a set of shell scripts. All of that collapsed into one daemon. If you learned Umbrel on 0.5.x, your mental model is obsolete.

**Docker** for every application. Each app is a set of containers described by a `docker-compose.yml`, with **images pinned to specific digests** rather than tags — a detail worth stealing, since tag-based pinning is how supply-chain surprises happen.

**React frontend** talking tRPC to `umbreld`.

The honest summary from one analysis: Umbrel wrapped Docker, a reverse proxy and app management into a polished GUI, making it accessible to people who don't know Docker — not technically complex, but very well productized. That's the right read. The value is in the packaging, the app store curation and the UX, not in novel systems engineering.

### The app framework — this is the part worth studying

Apps live at `/home/umbrel/umbrel/app-data/<app-id>/`, with the location exposed to the app as **`APP_DATA_DIR`**, and each app folder contains its `docker-compose.yml` plus its persistent data.

Each app package has two files that matter:

**`umbrel-app.yml`** — the manifest: id, name, version, category, port, dependencies, description, release notes.

**`docker-compose.yml`** — the services, with one structural convention you should notice immediately:

```yaml
services:
  app_proxy:
    environment:
      APP_HOST: $APP_BTC_RPC_EXPLORER_IP
      APP_PORT: $APP_BTC_RPC_EXPLORER_PORT

  web:
    image: getumbrel/btc-rpc-explorer:v2.0.2
    restart: on-failure
    ...
    networks:
      default:
        ipv4_address: $APP_BTC_RPC_EXPLORER_IP
```

**Every app gets an `app_proxy` service it didn't define.** That's `umbreld` injecting an authentication and routing shim in front of the actual application. It's how an app with no login system of its own inherits Umbrel's single sign-on, and how routing happens without each app knowing anything about the hostname or TLS.

That's a genuinely good design pattern and one of the main things worth taking away.

**Service discovery via environment variables.** Apps reach shared infrastructure through injected variables: `$APP_BITCOIN_NODE_IP`, `$APP_BITCOIN_RPC_PORT`, `$APP_BITCOIN_RPC_USER`, `$APP_LIGHTNING_NODE_DATA_DIR`, `$DEVICE_HOSTNAME`, `$DEVICE_DOMAIN_NAME`. Apps can also mount Bitcoin Core's or LND's data directory read-only.

Trace where those variables come from. Look for `exports.sh` in app packages and for the assembly logic in `umbreld` — that's the dependency-injection mechanism, and understanding it is what lets you add your own services to a running system.

**Hook scripts.** Look for a `hooks/` directory in app packages — pre-install, post-install, pre-start, post-start. This is where apps do setup that Compose can't express.

---

# Hands-on deconstruction exercises

Reading gets you 30%. These get you the rest.

### 1. Trace one request end to end

Open the BTC RPC Explorer in a browser. Now find every hop:

```bash
# Where did the TLS terminate?
ss -tulpn | grep :443

# Follow the proxy
docker ps --format '{{.Names}}\t{{.Ports}}'
docker logs <app_proxy_container> --tail 50

# Watch it live
docker exec -it <container> sh -c 'tcpdump -i any -n port 3002' 2>/dev/null
```

Draw the diagram by hand. Browser → what → what → container. If you can't draw it, you don't understand it yet.

### 2. Run an Umbrel app outside Umbrel

Take an app package, resolve every `$VARIABLE` manually, drop the `app_proxy` service, and bring it up with plain `docker compose` on a bare Debian box pointed at your own Bitcoin node.

```bash
cd ~/umbrel/app-data/mempool
cat docker-compose.yml
# now rewrite it with literal values and run it standalone
```

This exercise alone teaches you more about the framework than any amount of source reading, because it forces you to discover every implicit dependency. It's also directly billable later: "migrate my Umbrel to a maintainable setup" is a real client request.

### 3. Break it deliberately

- `docker stop` the Bitcoin container and watch what `umbreld` does
- Corrupt an app's data directory and attempt recovery
- Fill the disk to 100% and observe the failure mode
- Kill `umbreld` mid-app-install and see whether state is left consistent
- Pull the power during an update

Write down each failure signature. **This becomes your troubleshooting playbook**, and it's what separates a consultant from someone who can follow install instructions. Clients don't call you when things work.

### 4. Reproduce the OS build

```bash
git clone https://github.com/getumbrel/umbrel-os
# read the build scripts — what base image, what packages, what's injected
```

Understanding how the image is assembled tells you exactly what's customized versus inherited from Debian, and whether you could build an equivalent yourself.

### 5. Package your own app

Write a manifest and compose file for something not in the store, install it from a custom app repository, and get it working. The app store is just a git repo — you can point Umbrel at your own.

---

# What to steal, what to reject

**Steal:**

- **The `app_proxy` pattern.** Centralized auth and routing injected in front of every service. Reimplement it with Caddy or Traefik plus forward-auth for your own stack.
- **Digest-pinned images.** No surprise updates.
- **Manifest + compose separation.** Metadata apart from runtime definition.
- **Environment-variable service discovery.** Simple, debuggable, no service mesh.
- **`APP_DATA_DIR` convention.** One variable, and suddenly the whole installation is relocatable to an encrypted external drive — which is exactly how you'd build a portable client deployment.

**Reject:**

- **Monolithic daemon control.** `umbreld` owning everything makes it a single point of failure and makes anything outside the model awkward. For client work, plain systemd units and Compose files are more debuggable and don't depend on a vendor's daemon staying alive.
- **The abstraction over Docker.** Great for users, bad for operators. When something breaks, you're debugging two layers instead of one.
- **Opaque updates.** You want clients on infrastructure where you control update timing.
- **The license**, for commercial work.

---

# Comparison for your consulting toolkit

||umbrelOS|StartOS (Start9)|RaspiBlitz|MyNode|nix-bitcoin|
|---|---|---|---|---|---|
|Base|Debian|Debian|Raspberry Pi OS|Debian|NixOS|
|Orchestration|Docker + `umbreld`|Docker + `startd`|Bare systemd + bash|Docker/systemd|Nix derivations|
|Config model|Compose + manifest|Service packages (`s9pk`)|Bash scripts|Mixed|Declarative Nix|
|License|PolyForm Noncommercial|MIT|MIT|Freemium|MIT|
|Reproducible|No|Partially|No|No|**Yes**|
|Best for|Consumer UX|Privacy-focused users|Learning the plumbing|Turnkey|**Professional deployments**|

Two of these deserve extra attention for your purposes.

**RaspiBlitz** is the best teacher. It's mostly bash on bare systemd with almost no abstraction, so reading it shows you what every other framework is hiding. If you want to understand what installing a Lightning node actually involves, read `raspiblitz/home.admin/`.

**nix-bitcoin** is the one to take seriously for client work. Declarative, reproducible, auditable, MIT-licensed, with hardening and secret management built in. A client deployment defined in a Nix file that you can rebuild identically on new hardware is a genuinely superior product to a stack of Compose files — and almost nobody in the consulting market offers it. Steep learning curve, real differentiator.

---

# The deliverable

Give yourself a week per framework and produce, for each:

1. An architecture diagram you drew by hand
2. A failure catalogue — what breaks, what the symptom looks like, how to recover
3. A migration path off it onto your own stack
4. The license terms and what they permit
5. A one-page client-facing comparison: when you'd recommend each, and when you wouldn't

That last document is a sales asset. A client deciding between Umbrel and a custom build wants exactly that page, and being the person who can write it honestly — including "here's when you should just use Umbrel and not hire me" — is worth more than any install you'll ever perform.

---

Want me to sketch the reference architecture for your own deployment stack — the thing you'd actually ship to clients, borrowing the `app_proxy` pattern but built on plain systemd or Nix?