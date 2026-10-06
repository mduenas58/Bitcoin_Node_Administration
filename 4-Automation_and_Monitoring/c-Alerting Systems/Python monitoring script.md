Below is a complete Python monitoring script that watches a Bitcoin Core node and an LND node, and sends alerts via Telegram and email if the node goes offline or a channel is force‑closed. It builds directly on the health‑check and channel‑balance scripts from the previous answer.

---

## Architecture Overview

| Component | Purpose | API / Library |
|-----------|---------|---------------|
| **Bitcoin Core health** | Detect if the node is unreachable | JSON‑RPC via `python-bitcoinrpc` |
| **LND health** | Detect if LND is unreachable | gRPC `GetInfo` |
| **Force‑close detection** | React to channel closure events | gRPC `SubscribeChannelEvents` |
| **Telegram alert** | Push notification | Telegram Bot API (`requests`) |
| **Email alert** | Fallback / permanent record | `smtplib` + `email.mime` |
| **Scheduler** | Periodic health checks | `threading.Timer` |
| **Event listener** | Persistent channel event stream | Separate thread with reconnection |

---

## Prerequisites

```bash
pip install python-bitcoinrpc grpcio grpcio-tools requests
```

You also need:
- A compiled `lightning_pb2.py` / `lightning_pb2_grpc.py` from LND’s `lightning.proto` (see the previous answer for compilation steps).
- A Telegram bot token and a chat ID (create a bot with @BotFather, then get your chat ID via `https://api.telegram.org/bot<TOKEN>/getUpdates`).
- An SMTP server (e.g. Gmail, SendGrid) with credentials.
- Bitcoin Core `bitcoin.conf` must have `server=1` and RPC credentials set.
- LND must be running with the REST/gRPC interface enabled and the admin macaroon available.

---

## Full Monitoring Script (`node_monitor.py`)

```python
#!/usr/bin/env python3
"""
Bitcoin + LND monitoring script.
Alerts via Telegram and email when:
  • Bitcoin Core or LND becomes unreachable
  • A Lightning channel is force‑closed (local, remote, or breach)
"""

import codecs
import grpc
import logging
import os
import smtplib
import threading
import time
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from pathlib import Path

import requests
from bitcoinrpc.authproxy import AuthServiceProxy, JSONRPCException

# Generated gRPC modules (see previous answer for compilation)
import lightning_pb2 as lnrpc
import lightning_pb2_grpc as lightningstub

# ──────────────────────────────────────────────────────────────
# 1. CONFIGURATION
# ──────────────────────────────────────────────────────────────

# ---------- Bitcoin Core RPC ----------
BTC_RPC_USER = "your_rpc_user"
BTC_RPC_PASSWORD = "your_rpc_password"
BTC_RPC_HOST = "127.0.0.1"
BTC_RPC_PORT = 8332

# ---------- LND gRPC ----------
LND_GRPC_HOST = "localhost:10009"
LND_MACAROON_PATH = Path.home() / ".lnd/data/chain/bitcoin/mainnet/admin.macaroon"
LND_TLS_PATH = Path.home() / ".lnd/tls.cert"

# ---------- Telegram ----------
TELEGRAM_BOT_TOKEN = "YOUR_BOT_TOKEN"
TELEGRAM_CHAT_ID = "YOUR_CHAT_ID"

# ---------- Email (SMTP) ----------
SMTP_SERVER = "smtp.gmail.com"
SMTP_PORT = 587
SMTP_USER = "your_email@gmail.com"
SMTP_PASSWORD = "your_app_password"          # use an app password, not your login password
ALERT_RECIPIENT = "alerts@example.com"

# ---------- Monitoring interval (seconds) ----------
HEALTH_CHECK_INTERVAL = 60

# ──────────────────────────────────────────────────────────────
# 2. LOGGING
# ──────────────────────────────────────────────────────────────
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s",
    handlers=[
        logging.FileHandler("node_monitor.log"),
        logging.StreamHandler()
    ]
)
log = logging.getLogger(__name__)

# ──────────────────────────────────────────────────────────────
# 3. ALERTING FUNCTIONS
# ──────────────────────────────────────────────────────────────

def send_telegram_alert(message: str) -> None:
    """Send a message via the Telegram Bot API."""
    url = f"https://api.telegram.org/bot{TELEGRAM_BOT_TOKEN}/sendMessage"
    payload = {
        "chat_id": TELEGRAM_CHAT_ID,
        "text": message,
        "parse_mode": "Markdown"
    }
    try:
        resp = requests.post(url, json=payload, timeout=10)
        resp.raise_for_status()
        log.info("Telegram alert sent.")
    except Exception as e:
        log.error(f"Telegram alert failed: {e}")

def send_email_alert(subject: str, body: str) -> None:
    """Send an email alert via SMTP with TLS."""
    msg = MIMEMultipart()
    msg["From"] = SMTP_USER
    msg["To"] = ALERT_RECIPIENT
    msg["Subject"] = subject
    msg.attach(MIMEText(body, "plain"))

    try:
        with smtplib.SMTP(SMTP_SERVER, SMTP_PORT, timeout=15) as server:
            server.starttls()
            server.login(SMTP_USER, SMTP_PASSWORD)
            server.send_message(msg)
        log.info("Email alert sent.")
    except Exception as e:
        log.error(f"Email alert failed: {e}")

def alert(subject: str, body: str) -> None:
    """Fire both Telegram and email alerts."""
    full = f"*{subject}*\n\n{body}"
    send_telegram_alert(full)
    send_email_alert(subject, body)

# ──────────────────────────────────────────────────────────────
# 4. BITCOIN CORE HEALTH CHECK
# ──────────────────────────────────────────────────────────────

def check_bitcoin_core() -> bool:
    """
    Return True if Bitcoin Core responds to getblockchaininfo.
    On failure, send an alert and return False.
    """
    try:
        rpc = AuthServiceProxy(
            f"http://{BTC_RPC_USER}:{BTC_RPC_PASSWORD}@{BTC_RPC_HOST}:{BTC_RPC_PORT}",
            timeout=10
        )
        info = rpc.getblockchaininfo()
        log.info(
            f"Bitcoin Core OK — height {info['blocks']}, "
            f"headers {info['headers']}, chain {info['chain']}"
        )
        return True
    except (JSONRPCException, ConnectionRefusedError, OSError, Exception) as e:
        log.error(f"Bitcoin Core unreachable: {e}")
        alert(
            "🚨 Bitcoin Core Node Offline",
            f"Node at {BTC_RPC_HOST}:{BTC_RPC_PORT} did not respond.\nError: {e}"
        )
        return False

# ──────────────────────────────────────────────────────────────
# 5. LND HEALTH CHECK
# ──────────────────────────────────────────────────────────────

def _build_lnd_credentials():
    """Build composite gRPC credentials for LND."""
    macaroon = codecs.encode(open(LND_MACAROON_PATH, "rb").read(), "hex")

    def metadata_callback(context, callback):
        callback([("macaroon", macaroon)], None)

    auth_creds = grpc.metadata_call_credentials(metadata_callback)

    os.environ["GRPC_SSL_CIPHER_SUITES"] = "HIGH+ECDSA"
    cert = open(LND_TLS_PATH, "rb").read()
    ssl_creds = grpc.ssl_channel_credentials(cert)

    return grpc.composite_channel_credentials(ssl_creds, auth_creds)

def check_lnd_health() -> bool:
    """
    Return True if LND responds to GetInfo.
    On failure, send an alert and return False.
    """
    try:
        creds = _build_lnd_credentials()
        channel = grpc.secure_channel(LND_GRPC_HOST, creds)
        stub = lightningstub.LightningStub(channel)

        resp = stub.GetInfo(lnrpc.GetInfoRequest(), timeout=10)
        log.info(
            f"LND OK — version {resp.version}, "
            f"block height {resp.block_height}, "
            f"synced_to_chain={resp.synced_to_chain}"
        )
        return True
    except Exception as e:
        log.error(f"LND unreachable: {e}")
        alert(
            "🚨 LND Node Offline",
            f"LND at {LND_GRPC_HOST} did not respond.\nError: {e}"
        )
        return False

# ──────────────────────────────────────────────────────────────
# 6. FORCE‑CLOSE DETECTION (channel event stream)
# ──────────────────────────────────────────────────────────────

# Enum values from lightning.proto (ChannelCloseSummary.CloseType)
CLOSE_TYPE_COOPERATIVE = 0
CLOSE_TYPE_LOCAL_FORCE = 1
CLOSE_TYPE_REMOTE_FORCE = 2
CLOSE_TYPE_BREACH = 3

def _is_force_close(close_type: int) -> bool:
    """True for local force, remote force, or breach close."""
    return close_type in (
        CLOSE_TYPE_LOCAL_FORCE,
        CLOSE_TYPE_REMOTE_FORCE,
        CLOSE_TYPE_BREACH,
    )

def channel_event_listener():
    """
    Long‑running thread that subscribes to LND channel events.
    Alerts on any force‑close event.
    Reconnects automatically if the stream drops.
    """
    while True:
        try:
            log.info("Starting LND channel event subscription…")
            creds = _build_lnd_credentials()
            channel = grpc.secure_channel(LND_GRPC_HOST, creds)
            stub = lightningstub.LightningStub(channel)

            stream = stub.SubscribeChannelEvents(
                lnrpc.ChannelEventSubscription()
            )

            for event in stream:
                if event.HasField("closed_channel"):
                    cc = event.closed_channel
                    close_type = cc.close_type
                    chan_point = cc.channel_point

                    if _is_force_close(close_type):
                        type_name = {
                            CLOSE_TYPE_LOCAL_FORCE: "LOCAL_FORCE_CLOSE",
                            CLOSE_TYPE_REMOTE_FORCE: "REMOTE_FORCE_CLOSE",
                            CLOSE_TYPE_BREACH: "BREACH_CLOSE",
                        }.get(close_type, f"UNKNOWN({close_type})")

                        log.warning(
                            f"Force‑close detected: {chan_point} "
                            f"type={type_name}"
                        )
                        alert(
                            f"⚠️ Force‑Close Detected ({type_name})",
                            f"Channel: {chan_point}\n"
                            f"Close type: {type_name}\n"
                            f"Capacity (sats): {cc.capacity}\n"
                            f"Settled balance: {cc.settled_balance}"
                        )
                    else:
                        log.info(
                            f"Cooperative close: {chan_point} "
                            f"type={close_type}"
                        )
        except Exception as e:
            log.error(f"Channel event stream error: {e}. Reconnecting in 10s…")
            time.sleep(10)

# ──────────────────────────────────────────────────────────────
# 7. SCHEDULER
# ──────────────────────────────────────────────────────────────

def health_check_loop():
    """Periodically check Bitcoin Core and LND health."""
    while True:
        check_bitcoin_core()
        check_lnd_health()
        time.sleep(HEALTH_CHECK_INTERVAL)

# ──────────────────────────────────────────────────────────────
# 8. MAIN
# ──────────────────────────────────────────────────────────────

if __name__ == "__main__":
    log.info("Starting Bitcoin / LND node monitor…")

    # Start the channel‑event listener in a daemon thread
    event_thread = threading.Thread(target=channel_event_listener, daemon=True)
    event_thread.start()

    # Run the health‑check loop in the main thread
    try:
        health_check_loop()
    except KeyboardInterrupt:
        log.info("Monitor stopped by user.")
```

---

## How the Monitoring Logic Works

### Node Offline Detection

| Node | Method | Timeout | Alert Condition |
|------|--------|---------|-----------------|
| Bitcoin Core | `getblockchaininfo` via JSON‑RPC | 10 s | Any exception (connection refused, timeout, RPC error) |
| LND | `GetInfo` via gRPC | 10 s | Any gRPC exception |

Both checks run every `HEALTH_CHECK_INTERVAL` seconds. If either call fails, the script immediately fires a Telegram message and an email with the error details.

### Force‑Close Detection

The script subscribes to LND’s `SubscribeChannelEvents` server‑streaming RPC. Each event can carry a `closed_channel` field, which is a `ChannelCloseSummary`. The `close_type` enum tells you how the channel closed:

| Enum value | Meaning | Alert? |
|------------|---------|--------|
| `COOPERATIVE_CLOSE` (0) | Both parties agreed | No |
| `LOCAL_FORCE_CLOSE` (1) | Your node force‑closed | Yes |
| `REMOTE_FORCE_CLOSE` (2) | Peer force‑closed | Yes |
| `BREACH_CLOSE` (3) | Peer broadcast an old state | Yes |

When a force‑close event arrives, the script sends a detailed alert containing the channel point, close type, capacity, and settled balance. The listener runs in a daemon thread and automatically reconnects if the gRPC stream drops.

### Alert Delivery

- **Telegram**: Uses the raw Bot API via `requests`. The message is sent with Markdown formatting, so it renders nicely in the Telegram app.
- **Email**: Uses `smtplib` with STARTTLS on port 587. The script expects an app password (for Gmail, generate one in your Google Account security settings). The email body is plain text, making it easy to parse in a mail client or log aggregator.

Both alert functions are wrapped in try/except blocks so that a failure in one channel does not prevent the other from firing.

---

## Deployment Tips

1. **Run as a systemd service** so the monitor restarts automatically after a reboot or crash.
   ```ini
   [Unit]
   Description=Bitcoin/LND Node Monitor
   After=network.target

   [Service]
   ExecStart=/usr/bin/python3 /opt/node_monitor.py
   WorkingDirectory=/opt
   Restart=always
   RestartSec=15
   User=bitcoin

   [Install]
   WantedBy=multi-user.target
   ```

2. **Secure your credentials.** Move the configuration block into environment variables or a separate `config.py` that is not committed to version control.

3. **Test the alerts** before relying on them. You can temporarily call `alert("Test", "This is a test alert")` at startup to verify both Telegram and email delivery.

4. **Adjust the health‑check interval** based on your tolerance for downtime. A 60‑second interval is a good balance between responsiveness and resource usage.

5. **Extend for multiple nodes** by wrapping the health‑check functions in a loop over a list of node configurations, and prefixing each alert with the node’s name or alias.

This script gives you a lightweight, dependency‑light monitoring solution that covers the two most critical failure modes for a Bitcoin/Lightning node: the node going offline and a channel being force‑closed.