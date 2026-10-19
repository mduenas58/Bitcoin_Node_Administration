To securely access your home server from outside using Cloudflare while ensuring **only you** can access it, you need to combine two core features: **Cloudflare Tunnel** (which exposes the service without opening ports) and **Cloudflare Access** (which enforces identity verification).

### 🛠️ Step 1: Prerequisites
Before starting, you need to prepare:
*   **A domain name**: You must add it to Cloudflare and change the NS records at your registrar to point to Cloudflare.
*   **Your home server**: Ensure your service is running locally (e.g., `http://localhost:8080`).

### 🔗 Step 2: Create a Tunnel (Establish the Connection)
The purpose of this step is to establish an "outbound" connection from your home server to Cloudflare, thereby bypassing your router's port forwarding restrictions.

1.  Log in to the Cloudflare dashboard and go to **Networking** > **Tunnels**.
2.  Click **Create a tunnel**, select **Cloudflared** as the connector, and give it a name (e.g., `home-server`).
3.  The page will display installation commands for your server's operating system. Copy this command and run it in your home server's terminal. This command will automatically download and install `cloudflared` and connect using the Token in the command.
4.  Once the tunnel status shows as **Healthy**, proceed to the next step.

### 🌐 Step 3: Publish an Application (Configure Routing)
Map your domain to the local service running on your server.

1.  In the tunnel details page, go to the **Routes** tab and click **Add route** > **Published application**.
2.  **Hostname**: Enter a subdomain, for example, `myserver.yourdomain.com`.
3.  **Service URL**: Enter the address where your home server service is actually running locally, for example, `http://localhost:8080` (if the service is on another machine on the LAN, fill in its internal IP).
4.  Save. Now, accessing that domain should open your home server's page, but at this point, **anyone** can access it.

### 🔒 Step 4: Lock Down Access (Critical: Allow Only Yourself)
This is the core step to fulfill your "only me" requirement. You need to use **Cloudflare Access** to add an identity verification gateway in front of the tunnel.

1.  In the Cloudflare dashboard, go to **Zero Trust** > **Access** > **Applications**.
2.  Click **Add an application** and select **Self-hosted**.
3.  **Application domain**: Enter the domain you configured in Step 3 (e.g., `myserver.yourdomain.com`).
4.  **Create a policy**:
    *   **Action**: Select **Allow**.
    *   **Include** (include rule): Select **Emails** and fill in **your own email address** (e.g., `you@example.com`).
    *   **Require** (require rule): Can be left blank, but the Include rule for Emails is sufficient to restrict access to only you.
5.  Save the policy.

### ✅ Final Result
Now, when you (or anyone else) access that domain from the external network, Cloudflare will first intercept the request and require you to enter your email address. Cloudflare will send a one-time login code (OTP) to that email. **Only after entering the correct code can you see your home server's content**. Even if someone else obtains your domain, they will be blocked outside the login page.

### 💡 Security Tips
*   **Keep Token secure**: The Token generated when creating the tunnel is equivalent to the key to your home network; never leak it.
*   **Run as a service**: It's recommended to run `cloudflared` as a system service (e.g., `systemctl`), so it will automatically reconnect after server reboots.
*   **Check for 502 errors**: If the domain shows 502, first verify with `curl http://localhost:port` locally to confirm the service is running, then check whether the "Service URL" in the tunnel configuration is filled in correctly.