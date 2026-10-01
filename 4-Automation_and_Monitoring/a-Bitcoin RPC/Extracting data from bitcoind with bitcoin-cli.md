# Extracting data from bitcoind with bitcoin-cli

· @Manuel Duenas

`bitcoin-cli` is a thin JSON-RPC client. Everything it returns comes from one of four stores inside the running daemon, and knowing which store a command reads tells you in advance whether it will work on a pruned node, whether it needs an optional index, and why it is slow. This tutorial covers block data, peer and network state, and fee estimation, with working commands against Bitcoin Core 29.x and later.

## How bitcoin-cli reaches the daemon

`bitcoin-cli` holds no state of its own. It serialises your command into a JSON-RPC request, sends it over HTTP to `bitcoind`, and prints what comes back. Every quirk in this tutorial comes from what the daemon has in memory or on disk at the moment you ask.

![](file:///Users/manuel/Library/Application%20Support/LibreOffice/4/user/temp/lu22649f332kn.tmp/lu22649f3334x_tmp_e4a2e3e3.png)  
  

The practical consequence: before running an unfamiliar command, ask which store it reads. A pruned node has deleted old block files, so `getblock` on an old height fails while `gettxout` still works. A node without `txindex` cannot find an arbitrary transaction by txid, but can always answer about unspent outputs.

### Authentication

Two options, and the first is better for a single-machine setup.

**Cookie authentication** is automatic. On start, `bitcoind` writes a `.cookie` file into the data directory, and `bitcoin-cli` reads it if it has filesystem access. Nothing to configure.

`rpcauth` is for remote or multi-user access. Never put a plaintext `rpcpassword` in `bitcoin.conf` — generate a salted hash instead:

```
python3 ./share/rpcauth/rpcauth.py myuser
```

That prints an `rpcauth=` line for `bitcoin.conf` and the generated password once. Then:

```
bitcoin-cli -rpcuser=myuser -rpcpassword=... getblockcount
```

Better still, keep the password out of your shell history and process list:

```
bitcoin-cli -stdinrpcpass getblockcount
```

For a remote node, prefer an SSH tunnel or Tailscale over exposing the RPC port. `rpcbind` and `rpcallowip` open a port that has no business facing a network.

### Invocation basics

|   |   |
|---|---|
 
|Flag|Use|
|`-getinfo`|One-shot summary: chain, blocks, connections, difficulty, balance|
|`-named`|Pass arguments by name instead of position|
|`-rpcwait`|Block until the daemon is ready — essential in startup scripts|
|`-conf=`, `-datadir=`|Point at a non-default config or data directory|
|`-regtest`, `-signet`, `-testnet4`|Target a test network|
|`-rpcclienttimeout=0`|Disable the client timeout for long calls like `gettxoutsetinfo`|

Named arguments are worth the habit, because positional ones silently mean different things across versions:

```
bitcoin-cli -named getblock blockhash=000000...e4f verbosity=2
```

### Discovering commands

```
bitcoin-cli help                    # every command, grouped by category
```

`help <command>` is authoritative for the version you are running and includes a worked example at the bottom. When this tutorial and your local `help` disagree, your local `help` is right.

## Block data

### Where the chain stands

```
bitcoin-cli getblockchaininfo
```

The fields that matter operationally:

|   |   |
|---|---|
 
|Field|Meaning|
|`blocks`|Validated block height|
|`headers`|Headers known. If this exceeds `blocks` by a lot, you are still syncing bodies|
|`bestblockhash`|Tip hash|
|`verificationprogress`|0 to 1. Monitor this during IBD rather than `blocks`|
|`initialblockdownload`|Boolean. The honest answer to "is it synced"|
|`pruned`, `pruneheight`|Whether old blocks are gone and from which height data survives|
|`size_on_disk`|Bytes, useful for capacity alerting|
|`warnings`|An array since v29. Non-empty means read it.|

Quick one-liners:

```
bitcoin-cli getblockcount          # tip height
```

Soft-fork and deployment status moved out of `getblockchaininfo` into its own call:

```
bitcoin-cli getdeploymentinfo
```

### Fetching a block

Blocks are addressed by hash, so height lookups are two steps:

```
HASH=$(bitcoin-cli getblockhash 900000)
```

`getblock` takes a verbosity argument, and choosing the right one is the difference between a fast call and megabytes of JSON:

|   |   |   |
|---|---|---|
  
|Verbosity|Returns|Use when|
|`0`|Raw serialised block as hex|Feeding another tool, or parsing yourself|
|`1` _(default)_|Block header fields plus an array of txids|You want structure, not transaction contents|
|`2`|Every transaction decoded in full|You need outputs, scripts, amounts|
|`3`|As 2, plus `prevout` for each input|You need input values — the only way to compute fees without extra lookups|

Verbosity 3 is underused and solves a real problem. A transaction's inputs reference previous outputs by txid and index, not by amount, so computing a fee normally means fetching every parent. Verbosity 3 has the daemon do that for you from its own UTXO knowledge.

```
bitcoin-cli getblock $HASH 3 | jq '.tx[1].fee'
```

For the header alone, which is cheap and works on pruned nodes at any height:

```
bitcoin-cli getblockheader $HASH
```

### Block statistics without parsing

`getblockstats` computes aggregates server-side and accepts a height directly, no hash lookup needed:

```
bitcoin-cli getblockstats 900000
```

It returns fee and size distributions for the block: `avgfee`, `avgfeerate`, `minfeerate`, `maxfeerate`, `medianfee`, `totalfee`, `subsidy`, `total_out`, `total_size`, `total_weight`, `txs`, `utxo_increase`, `ins`, `outs`, and `feerate_percentiles` — an array of the 10th, 25th, 50th, 75th and 90th percentile feerates in sat/vB.

Request only what you need and the call gets substantially faster:

```
bitcoin-cli getblockstats 900000 '["height","avgfeerate","feerate_percentiles","txs"]'
```

This is the right tool for fee history. Walking a range of blocks with `getblockstats` is far cheaper than fetching each block at verbosity 2 and summing.

### Chain tips and reorgs

```
bitcoin-cli getchaintips
```

Returns every known branch head. The `status` field is what you read:

|   |   |
|---|---|
 
|Status|Meaning|
|`active`|Your current chain. Exactly one.|
|`valid-fork`|A valid branch, not the most work — evidence of a past reorg|
|`valid-headers`|Headers validated, block bodies not downloaded|
|`headers-only`|Headers received, not fully validated|
|`invalid`|Branch contains a block your node rejected|

A growing count of `valid-fork` entries with high `branchlen` is worth investigating. An `invalid` tip with significant length means your node disagreed with part of the network, which deserves immediate attention.

### Long-range statistics

```
bitcoin-cli getchaintxstats 2016
```

Transaction count and rate over a window of blocks, defaulting to roughly one month. Useful for capacity reporting without computing it yourself.

## Transactions inside blocks

### The txindex question

By default `bitcoind` keeps no index from txid to block. It can answer "is this output unspent" from the chainstate, but not "show me transaction X" for an arbitrary historical txid.

Three ways around it:

**Give the block hash.** If you already know where the transaction lives, no index is needed:

```
bitcoin-cli getrawtransaction <txid> true <blockhash>
```

**Enable the index.** Add `txindex=1` to `bitcoin.conf` and restart. The node builds the index on first start after the change, which takes hours and adds tens of gigabytes. Incompatible with pruning.

**Query the mempool.** Unconfirmed transactions are always retrievable regardless of indexes.

For consulting work, enable `txindex` on any node a client will query interactively. The disk cost is small against the frustration of commands that fail unpredictably.

### Fetching a transaction

```
bitcoin-cli getrawtransaction <txid>          # hex
```

Verbosity `2` is the one to reach for. It adds a `fee` field and a `prevout` object on each input carrying the spent output's value and scriptPubKey — so you can compute effective feerate without a second round of lookups.

```
bitcoin-cli getrawtransaction <txid> 2 | jq '{fee: .fee, vsize: .vsize, feerate: (.fee / .vsize * 1e8)}'
```

That last expression yields sat/vB, since `fee` is reported in BTC.

### Decoding without a node lookup

```
bitcoin-cli decoderawtransaction <hex>
```

Purely local parsing of a hex string you already have — no index, no chain access. Useful for inspecting a PSBT's finalised output or a transaction someone sent you before broadcasting.

Related decoders:

```
bitcoin-cli decodescript <hex>       # interpret a scriptPubKey or redeemScript
```

`analyzepsbt` is the one worth remembering during a multisig session: it tells you exactly which inputs still need signatures and what the next step is.

### Checking an unspent output

```
bitcoin-cli gettxout <txid> <vout>
```

Reads the chainstate directly, so it works on a pruned node with no index. Returns `null` if the output has been spent or never existed — which makes it a fast spent/unspent test.

```
bitcoin-cli gettxout <txid> 0 true    # include mempool spends
```

With `true`, an output spent by an unconfirmed transaction also returns `null`. Choose based on whether you care about confirmed state or current state.

### Scanning for outputs by descriptor

```
bitcoin-cli scantxoutset start '["addr(bc1q...)"]'
```

Sweeps the entire UTXO set for outputs matching a descriptor. No wallet, no index, no rescan — it reads chainstate directly and takes a minute or two.

This is genuinely useful in a recovery scenario: given a descriptor and nothing else, it finds the current balance without importing anything.

```
bitcoin-cli scantxoutset start '["wsh(sortedmulti(2,[aaaaaaaa/48h/0h/0h/2h]xpub.../0/*,...))"]'
```

Note the limitation: it finds **unspent** outputs only. For transaction history you need a wallet rescan or an external indexer like Electrs or Fulcrum.

### Finding transactions by block range

With `blockfilterindex=1` enabled:

```
bitcoin-cli scanblocks start '["addr(bc1q...)"]' 880000 900000
```

Uses compact block filters to identify which blocks in a range could contain matches, far faster than fetching every block. Returns candidate block hashes; fetch those blocks to confirm. This is how you reconstruct history on a node without `txindex`.

## Peer and network information

### The peer list

```
bitcoin-cli getpeerinfo
```

One object per connection. The fields worth knowing:

|   |   |
|---|---|
 
|Field|What it tells you|
|`id`|Internal peer number, used by `disconnectnode`|
|`addr`|Peer address and port|
|`network`|`ipv4`, `ipv6`, `onion`, `i2p`, `cjdns`, `not_publicly_routable`|
|`connection_type`|How the connection came about — see below|
|`inbound`|True if they connected to you|
|`subver`|Their user agent string, e.g. `/Satoshi:29.0.0/`|
|`startingheight`|Their height when the connection opened|
|`synced_headers`, `synced_blocks`|How far along they are now|
|`pingtime`, `minping`|Current and best round-trip in seconds|
|`bytessent`, `bytesrecv`|Traffic with this peer|
|`conntime`|Unix timestamp of connection start|
|`relaytxes`|Whether they want transaction relay|
|`transport_protocol_type`|`v1` or `v2` — BIP324 encrypted transport|
|`bip152_hb_to`, `bip152_hb_from`|High-bandwidth compact block relay|

`connection_type` is the field most people miss, and it explains your node's behaviour:

|   |   |
|---|---|
 
|Type|Meaning|
|`outbound-full-relay`|A normal outbound peer. Your node maintains 8 of these.|
|`block-relay-only`|Blocks but no transaction relay — a partition-resistance measure, 2 by default|
|`inbound`|They found you|
|`manual`|Added via `addnode` or `connect`|
|`feeler`|A brief test connection to validate an address, then dropped|
|`addr-fetch`|A one-shot connection to collect addresses|

If you see few or no `inbound` peers, your node is not reachable from outside — check port forwarding or Tor configuration. If `outbound-full-relay` is below 8, your node is struggling to find peers.

### Network configuration

```
bitcoin-cli getnetworkinfo
```

|   |   |
|---|---|
 
|Field|Use|
|`version`, `subversion`|Your node's version|
|`protocolversion`|P2P protocol version|
|`connections`, `connections_in`, `connections_out`|The counts at a glance|
|`networks`|Per-network: whether reachable, proxy in use, `proxy_randomize_credentials`|
|`localaddresses`|What your node believes its reachable addresses are|
|`relayfee`|Minimum feerate for relay, in BTC/kvB|
|`incrementalfee`|Minimum feerate bump for RBF|
|`localrelay`|Whether you relay transactions at all|
|`warnings`|Read it|

The `networks` array is the fast way to confirm Tor is actually working. A node you believe is Tor-only but shows `ipv4` as reachable is leaking.

```
bitcoin-cli getnetworkinfo | jq '.networks[] | {name, reachable, proxy}'
```

### Bandwidth

```
bitcoin-cli getnettotals
```

Cumulative `totalbytesrecv` and `totalbytessent` since start, plus an `uploadtarget` object showing whether a `-maxuploadtarget` limit is configured, how much of the cycle remains, and whether the target has been reached. Worth alerting on if the client pays for bandwidth.

### The address manager

Your node keeps a database of addresses it has learned, separate from its current connections.

```
bitcoin-cli getnodeaddresses 50            # 50 known addresses
```

`getaddrmaninfo` reports `new` and `tried` counts per network. A `tried` table that stays near zero means your node has rarely succeeded in connecting outward — usually a firewall or proxy problem.

### Managing connections

```
bitcoin-cli addnode "203.0.113.5:8333" add        # persistent
```

Connecting to a specific peer — a client's other node, a known-good relay — is a common diagnostic step. Use `onetry` first to see whether the connection is even possible before making it persistent.

### Bans

```
bitcoin-cli setban "203.0.113.0/24" add 86400     # one day
```

Bans survive restarts in `banlist.json`. Note that bans are for abusive behaviour; a peer disconnecting often is not misbehaving, and banning normal peers makes your node worse at finding connections.

### Latency check

```
bitcoin-cli ping
```

Queues a ping to every peer. It returns immediately and does not report results — read them from `pingtime` in `getpeerinfo` a few seconds later.

## Mempool and fee estimation

### Mempool state

```
bitcoin-cli getmempoolinfo
```

|   |   |
|---|---|
 
|Field|Meaning|
|`loaded`|Mempool restored from disk after restart. False briefly at startup.|
|`size`|Transaction count|
|`bytes`|Total virtual size|
|`usage`|Actual memory used — larger than `bytes`, this is what counts against the limit|
|`maxmempool`|The configured ceiling, 300 MB by default|
|`mempoolminfee`|Current minimum to enter **this** mempool. Rises above `minrelaytxfee` when full.|
|`minrelaytxfee`|The configured floor|
|`incrementalrelayfee`|Minimum feerate increase for an RBF replacement|
|`total_fee`|Sum of all fees waiting|
|`unbroadcastcount`|Your own transactions not yet confirmed as relayed|

`mempoolminfee` exceeding `minrelaytxfee` is the signal that the mempool is full and low-feerate transactions are being evicted. Any transaction below `mempoolminfee` will be rejected outright by your node — a common cause of a client's "my transaction disappeared".

### Listing the mempool

```
bitcoin-cli getrawmempool                 # array of txids
```

The verbose form on a busy mempool returns a very large object. Prefer `getmempoolentry` for a specific transaction:

```
bitcoin-cli getmempoolentry <txid>
```

|   |   |
|---|---|
 
|Field|Meaning|
|`vsize`, `weight`|Size for fee purposes|
|`time`|When it entered your mempool|
|`fees.base`|Its own fee|
|`fees.modified`|After any local prioritisation|
|`fees.ancestor`|Its fee plus all unconfirmed ancestors — what miners actually evaluate|
|`fees.descendant`|Its fee plus unconfirmed descendants|
|`depends`, `spentby`|Unconfirmed parents and children|
|`bip125-replaceable`|Whether it signals RBF|

The ancestor fields are what matter for a stuck transaction. A low-fee parent with a high-fee child (CPFP) is evaluated on the package feerate, so `fees.ancestor / ancestor vsize` is the number that predicts confirmation — not the transaction's own feerate.

```
bitcoin-cli getmempoolancestors <txid> true
```

### Fee estimation

```
bitcoin-cli estimatesmartfee 6
```

Returns `feerate` in **BTC per kvB** and the `blocks` target actually used. Convert to sat/vB by multiplying by 100,000:

```
bitcoin-cli estimatesmartfee 6 | jq '.feerate * 100000'
```

Two modes:

|   |   |
|---|---|
 
|Mode|Behaviour|
|`CONSERVATIVE` _(default)_|Uses a longer history window. Higher estimate, more resilient if the mempool is rising. Right for transactions you cannot easily replace.|
|`ECONOMICAL`|Shorter window, more responsive to a currently quiet mempool. Lower estimate. Right for RBF-signalling transactions you can bump.|

```
bitcoin-cli estimatesmartfee 1 ECONOMICAL
```

A practical fee table for a client:

```
for t in 1 2 3 6 12 24 144 1008; do
```

### The estimator's limitations

Worth understanding before you trust it in a client script.

**It needs history.** Estimates are built from observed confirmation times of transactions your node saw enter the mempool and then get mined. A node freshly synced, or one restarted after days offline, has no basis for an estimate and returns an `errors` array instead of a `feerate`. Always check for `feerate` before using the result.

**It is backward-looking.** It describes what feerate recently worked, not what will work. In a sharp fee spike it lags.

**Short targets can fail.** Asking for `1` often returns a result for `2` — which is why the response includes the `blocks` field. Read it rather than assuming you got what you asked for.

For current conditions rather than historical estimates, read the mempool directly: `getmempoolinfo` for `mempoolminfee`, or the `feerate_percentiles` from `getblockstats` on the last few blocks to see what has actually been confirming.

### Testing before broadcast

```
bitcoin-cli testmempoolaccept '["<raw hex>"]'
```

Runs full validation without broadcasting. Returns `allowed`, plus `reject-reason` if not, and `vsize` and `fees.base` if accepted. Run this before every programmatic broadcast — it catches fee-too-low, non-standard scripts and missing inputs cheaply.

```
bitcoin-cli submitpackage '["<parent hex>","<child hex>"]'
```

Submits a parent and its CPFP child together, so a parent below `mempoolminfee` can still enter on the package's combined feerate.

## Practical recipes

Everything below assumes `jq`. Install it before anything else; `bitcoin-cli` without `jq` is a toy.

### A readable peer table

```
bitcoin-cli getpeerinfo | jq -r '
```

### Peers grouped by network and direction

```
bitcoin-cli getpeerinfo | jq -r '
```

### Slowest peers

```
bitcoin-cli getpeerinfo | jq -r '
```

### Which Core versions your peers run

```
bitcoin-cli getpeerinfo | jq -r '.[].subver' | sort | uniq -c | sort -rn
```

A useful proxy for how quickly the network adopts releases, and a good talking point with clients deciding when to upgrade.

### Fee history over the last N blocks

```
TIP=$(bitcoin-cli getblockcount)
```

This tells you what actually confirmed, which is more honest than any estimate.

### Mempool feerate histogram

```
bitcoin-cli getrawmempool true | jq -r '
```

Slow on a full mempool — it pulls the whole verbose structure. Run it occasionally rather than in a tight loop.

### Block interval, last 20 blocks

```
TIP=$(bitcoin-cli getblockcount)
```

### A one-line health check

```
bitcoin-cli -getinfo
```

For scripting, a fuller version:

```
bitcoin-cli getblockchaininfo | jq -r '
```

That trio is the basis of a client status page or a cron-driven alert.

### Alerting on tip staleness

```
AGE=$(( $(date +%s) - $(bitcoin-cli getblockheader $(bitcoin-cli getbestblockhash) | jq .time) ))
```

Blocks are irregular, so an hour is normal-ish and two hours is worth a look. Alert on sustained staleness rather than a single long gap.

### Waiting for a new block in a script

```
bitcoin-cli waitfornewblock 600
```

Blocks until the condition is met or the timeout expires — far better than polling `getblockcount` in a loop.

## Errors and gotchas

### Error codes you will meet

|   |   |   |
|---|---|---|
  
|Error|Cause|Fix|
|`error code: -28` — loading block index|Daemon still starting|Wait, or use `-rpcwait`|
|`Could not connect to the server`|Daemon not running, or wrong port or datadir|Check `systemctl status bitcoind`; confirm `-datadir`|
|`Authorization failed: Incorrect rpcuser or rpcpassword`|Cookie unreadable or credentials wrong|Check permissions on `.cookie`, or your `rpcauth` line|
|`No such mempool or blockchain transaction`|No `txindex`, and the tx is confirmed and not in mempool|Supply the block hash, or enable `txindex=1`|
|`Block not available (pruned data)`|Block older than `pruneheight`|Unavoidable without a full resync|
|`Method not found`|Command removed, renamed, or needs an index|Check `bitcoin-cli help` for your version|
|`Insufficient funds` from `fundrawtransaction`|Wallet balance or feerate issue|Check `getbalances` and current `mempoolminfee`|
|`-32603` on `gettxoutsetinfo`|Client timed out, not a server error|Run with `-rpcclienttimeout=0`|

### Units, which cause most mistakes

|   |   |
|---|---|
 
|Context|Unit|
|`estimatesmartfee.feerate`|BTC/kvB — multiply by 100,000 for sat/vB|
|`getnetworkinfo.relayfee`|BTC/kvB|
|`getmempoolinfo.mempoolminfee`|BTC/kvB|
|`getmempoolentry.fees.*`|BTC|
|`getrawtransaction` verbosity 2, `fee`|BTC|
|`getblockstats` feerates|**sat/vB**|
|`getblockstats` fee totals|**satoshis**|

`getblockstats` is the odd one out, and mixing it with the others is the single most common unit bug. Convert everything to sat/vB at the edge of your script and work in one unit internally.

### Floating point

`bitcoin-cli` returns BTC amounts as JSON numbers, and `jq` parses them as doubles. For display that is fine; for accounting it is not.

```
bitcoin-cli getmempoolentry <txid> | jq '.fees.base * 100000000'
```

That can produce `12344.999999999998`. Round explicitly, or use `jq`'s `tostring` on the raw value and handle the decimal yourself. Better still, prefer commands that already return integer satoshis — `getblockstats` does.

### Pruning

On a pruned node:

- `getblock` and `getblockstats` fail below `pruneheight`
    
- `getblockheader` works at **any** height — headers are never pruned
    
- `gettxout` and `scantxoutset` work normally — chainstate is complete
    
- `txindex`, `coinstatsindex` and `blockfilterindex` are all incompatible
    

Check before assuming:

```
bitcoin-cli getblockchaininfo | jq '{pruned, pruneheight}'
```

### Rate and load

RPC calls are served by a small thread pool, default 4. A loop firing hundreds of calls will queue and can make the node appear unresponsive to other clients.

- Raise `rpcthreads` and `rpcworkqueue` in `bitcoin.conf` for monitoring workloads
    
- Prefer one call returning many objects over many calls returning one
    
- `gettxoutsetinfo` scans the entire UTXO set and takes minutes — never put it in a frequent cron. With `coinstatsindex=1` it becomes fast.
    
- `getrawmempool true` on a full mempool returns tens of megabytes
    

### Shell quoting

Array and object arguments must survive the shell. Single-quote the whole JSON:

```
bitcoin-cli getblockstats 900000 '["avgfeerate","txs"]'
```

For anything with nested quotes, use a heredoc or a file rather than fighting the escaping:

```
bitcoin-cli -named createrawtransaction inputs="$(cat inputs.json)" outputs="$(cat outputs.json)"
```

### Version drift

Field names and defaults change between major releases. `warnings` became an array in v29; soft-fork status moved to `getdeploymentinfo`; `getblock` gained verbosity 3.

If you write scripts a client will run for years, pin the version you tested against, check `getnetworkinfo.version` at startup, and read the release notes before upgrading a client's node. A monitoring script that silently returns nothing after an upgrade is worse than one that fails loudly.