Below are three Python scripts that interact with the Bitcoin Core and LND (Lightning Network Daemon) APIs. Each script addresses a specific task—node health, channel balances, and missing blocks—and uses either REST or gRPC as appropriate. All examples assume you have a running Bitcoin Core node and an LND node with the necessary macaroon and TLS certificate files.

---

## 1. Node Health Check (LND gRPC)

This script uses LND's gRPC interface to fetch general node information such as sync status, block height, and peer count.

### Prerequisites
- Install the required packages:
  ```bash
  pip install grpcio grpcio-tools googleapis-common-protos
  ```
- Compile the LND proto file (see the official guide). You will need `lightning_pb2.py` and `lightning_pb2_grpc.py`.

### Script (`lnd_node_health.py`)

```python
import codecs
import grpc
import os
from pathlib import Path

# Generated gRPC modules
import lightning_pb2 as lnrpc
import lightning_pb2_grpc as lightningstub

# Configuration
GRPC_HOST = 'localhost:10009'
MACAROON_PATH = Path.home() / '.lnd/data/chain/bitcoin/mainnet/admin.macaroon'
TLS_PATH = Path.home() / '.lnd/tls.cert'

# Macaroon credentials
macaroon = codecs.encode(open(MACAROON_PATH, 'rb').read(), 'hex')

def metadata_callback(context, callback):
    callback([('macaroon', macaroon)], None)

auth_creds = grpc.metadata_call_credentials(metadata_callback)

# SSL credentials
os.environ['GRPC_SSL_CIPHER_SUITES'] = 'HIGH+ECDSA'
cert = open(TLS_PATH, 'rb').read()
ssl_creds = grpc.ssl_channel_credentials(cert)

# Combined credentials
combined_creds = grpc.composite_channel_credentials(ssl_creds, auth_creds)

# Connect and call GetInfo
channel = grpc.secure_channel(GRPC_HOST, combined_creds)
stub = lightningstub.LightningStub(channel)

request = lnrpc.GetInfoRequest()
response = stub.GetInfo(request)

print("=== LND Node Health ===")
print(f"Version       : {response.version}")
print(f"Alias         : {response.alias}")
print(f"Pubkey        : {response.identity_pubkey}")
print(f"Block Height  : {response.block_height}")
print(f"Synced to Chain: {response.synced_to_chain}")
print(f"Synced to Graph: {response.synced_to_graph}")
print(f"Active Channels: {response.num_active_channels}")
print(f"Inactive Channels: {response.num_inactive_channels}")
print(f"Pending Channels: {response.num_pending_channels}")
print(f"Peers         : {response.num_peers}")
```

**How it works**  
- The script loads the admin macaroon and TLS certificate, then builds a secure gRPC channel with composite credentials.  
- It calls `GetInfo`, which returns the node's identity, sync status, channel counts, and more.  
- The output gives a quick snapshot of whether the node is synced and how many channels are active.

---

## 2. Channel Balances (LND REST)

This script uses LND's REST API to retrieve the total local and remote balances across all open channels.

### Prerequisites
- Install `requests`:
  ```bash
  pip install requests
  ```
- Ensure your LND node is configured to expose the REST interface (usually on port `8080`).

### Script (`lnd_channel_balance.py`)

```python
import requests
import codecs
from pathlib import Path

# Configuration
REST_HOST = 'https://localhost:8080'
MACAROON_PATH = Path.home() / '.lnd/data/chain/bitcoin/mainnet/admin.macaroon'
TLS_CERT_PATH = Path.home() / '.lnd/tls.cert'

# Read macaroon and encode as hex
macaroon = codecs.encode(open(MACAROON_PATH, 'rb').read(), 'hex').decode()

headers = {
    'Grpc-Metadata-macaroon': macaroon,
    'Content-Type': 'application/json'
}

# Disable SSL verification for self-signed cert (or pass verify=TLS_CERT_PATH)
response = requests.get(
    f'{REST_HOST}/v1/balance/channels',
    headers=headers,
    verify=False
)

if response.status_code == 200:
    data = response.json()
    print("=== Channel Balances (sats) ===")
    print(f"Local Balance        : {data.get('local_balance', {}).get('sat', 0)}")
    print(f"Remote Balance       : {data.get('remote_balance', {}).get('sat', 0)}")
    print(f"Pending Open Local   : {data.get('pending_open_local_balance', {}).get('sat', 0)}")
    print(f"Pending Open Remote  : {data.get('pending_open_remote_balance', {}).get('sat', 0)}")
    print(f"Unsettled Local      : {data.get('unsettled_local_balance', {}).get('sat', 0)}")
    print(f"Unsettled Remote     : {data.get('unsettled_remote_balance', {}).get('sat', 0)}")
else:
    print(f"Error {response.status_code}: {response.text}")
```

**How it works**  
- The REST endpoint `/v1/balance/channels` returns a `ChannelBalanceResponse` with fields for local, remote, pending, and unsettled balances.  
- The script sends the macaroon as a hex-encoded header (`Grpc-Metadata-macaroon`) and parses the JSON response.  
- Balances are given in satoshis under the `sat` sub-field.

---

## 3. Missing Blocks Check (Bitcoin Core RPC + LND GetBlock)

This script checks whether the local Bitcoin Core node has all blocks up to the current best height, and optionally verifies that LND can retrieve a specific block.

### Prerequisites
- Install `python-bitcoinrpc`:
  ```bash
  pip install python-bitcoinrpc
  ```
- For the LND part, ensure the gRPC modules for `chainrpc/chainkit.proto` are compiled (similar to the first script).

### Script (`check_missing_blocks.py`)

```python
from bitcoinrpc.authproxy import AuthServiceProxy, JSONRPCException
import codecs, grpc, os
from pathlib import Path

# ---------- Bitcoin Core RPC ----------
RPC_USER = 'your_rpc_user'
RPC_PASSWORD = 'your_rpc_password'
RPC_HOST = '127.0.0.1'
RPC_PORT = 8332

rpc_connection = AuthServiceProxy(
    f"http://{RPC_USER}:{RPC_PASSWORD}@{RPC_HOST}:{RPC_PORT}"
)

info = rpc_connection.getblockchaininfo()
local_height = info['blocks']
best_hash = info['bestblockhash']

print("=== Bitcoin Core Blockchain Info ===")
print(f"Chain                : {info['chain']}")
print(f"Blocks               : {local_height}")
print(f"Headers              : {info['headers']}")
print(f"Best Block Hash      : {best_hash}")
print(f"Verification Progress: {info['verificationprogress']:.4%}")

# Check for missing blocks by comparing blocks vs headers
if info['blocks'] < info['headers']:
    missing = info['headers'] - info['blocks']
    print(f"\n⚠️  Missing {missing} block(s) — node is still syncing.")
else:
    print("\n✅ All blocks are present up to the current header height.")

# ---------- LND GetBlock (optional) ----------
# Compile chainkit_pb2.py and chainkit_pb2_grpc.py from chainrpc/chainkit.proto first.
try:
    import chainkit_pb2 as chainrpc
    import chainkit_pb2_grpc as chainkitstub

    GRPC_HOST = 'localhost:10009'
    MACAROON_PATH = Path.home() / '.lnd/data/chain/bitcoin/mainnet/admin.macaroon'
    TLS_PATH = Path.home() / '.lnd/tls.cert'

    macaroon = codecs.encode(open(MACAROON_PATH, 'rb').read(), 'hex')

    def metadata_callback(context, callback):
        callback([('macaroon', macaroon)], None)

    auth_creds = grpc.metadata_call_credentials(metadata_callback)
    os.environ['GRPC_SSL_CIPHER_SUITES'] = 'HIGH+ECDSA'
    cert = open(TLS_PATH, 'rb').read()
    ssl_creds = grpc.ssl_channel_credentials(cert)
    combined_creds = grpc.composite_channel_credentials(ssl_creds, auth_creds)

    channel = grpc.secure_channel(GRPC_HOST, combined_creds)
    stub = chainkitstub.ChainKitStub(channel)

    # Request the block by its hash (bytes)
    block_hash_bytes = bytes.fromhex(best_hash)
    request = chainrpc.GetBlockRequest(block_hash=block_hash_bytes)
    response = stub.GetBlock(request)

    print(f"\n=== LND GetBlock ===")
    print(f"Raw block size: {len(response.raw_block)} bytes")
except ImportError:
    print("\n(LND GetBlock skipped — chainkit gRPC modules not compiled.)")
except Exception as e:
    print(f"\nLND GetBlock error: {e}")
```

**How it works**  
- The Bitcoin Core part uses `getblockchaininfo` to compare the `blocks` field with `headers`. If `blocks < headers`, the node is still downloading blocks, indicating missing data.  
- The LND part calls the `GetBlock` gRPC method from the ChainKit subserver. It passes the best block hash and prints the size of the returned raw block.  
- If the chainkit proto modules are not compiled, the script gracefully skips that section.

---

## Summary of API Endpoints Used

| Task | API | Method / Endpoint | Notes |
|------|-----|-------------------|-------|
| Node Health | LND gRPC | `GetInfo` | Returns sync status, channel counts, peers |
| Channel Balances | LND REST | `GET /v1/balance/channels` | Returns local/remote/pending balances |
| Missing Blocks | Bitcoin Core RPC | `getblockchaininfo` | Compares `blocks` vs `headers` |
| Block Retrieval | LND gRPC | `GetBlock` (ChainKit) | Fetches raw block by hash |

These scripts can be extended with error handling, logging, or scheduling (e.g., via `cron` or `systemd` timers) to build a basic monitoring tool for your Bitcoin and Lightning infrastructure.