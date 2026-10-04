Connecting hardware wallets directly to your own Electrs server via Sparrow Wallet ensures your transaction data never leaks to third-party public servers. While air-gapped setups are the gold standard for enterprise cold storage, direct USB connections provide excellent security for everyday operations because the private keys never leave the device—all signing happens internally on the hardware wallet itself.

Here is the procedure for connecting your hardware wallet to Sparrow using your node's Electrum server.
### Phase 1: Connect Sparrow to Electrs

Your wallet interface needs to verify transactions against your own full node's copy of the blockchain.

1. Open Sparrow Wallet on your local computer.
2. Navigate to **File > Preferences > Server**.
3. Select the **Private Electrum** tab.
4. Enter the IP address (or Tor `.onion` address) of your node, and set the port to `50001` for TCP or `50002` for SSL.
5. Click **Test Connection**. A green checkmark confirms Sparrow is successfully pulling blockchain data from your personal Electrs instance.
### Phase 2: Device-Specific Preparation

Before Sparrow can read the public keys, each device requires a brief configuration step.

- **Trezor:** Ensure the device is initialized and running the latest firmware. No special configuration is required on the device to allow Sparrow to read it.
- **BitBox02:** The device can only communicate with one software interface at a time. If you have the official BitBoxApp open on your computer, you must close it completely before Sparrow can detect the device.
- **Coldcard:** If you opt to use a USB cable instead of a MicroSD card, you must manually enable the data connection. Navigate to **Settings > Hardware On/Off > USB Port** on the device and turn it on, as it is disabled by default.
### Phase 3: Import the Hardware Keystore

Once the device is prepared, you pull the Extended Public Key (xpub) into Sparrow to monitor balances and generate receiving addresses.

1. Connect the hardware wallet to your computer using a data-capable USB-C cable (power-only charging cables will not allow Sparrow to detect the device).
2. Unlock the hardware wallet by entering your PIN on the device.
3. In Sparrow Wallet, navigate to **File > New Wallet** and give the wallet a descriptive name.
4. Under the **Keystores** section, select **Connected Hardware Wallet**.
5. Click the **Scan** button. Sparrow will automatically detect the connected Trezor, BitBox02, or Coldcard and read its keystore information.
6. Click **Import Keystore**, and then click **Apply**.
7. Sparrow will prompt you to set a password. This password encrypts the wallet data file locally on your computer.
### Phase 4: Address Verification

It is best practice to ensure Sparrow derived the exact same addresses as the hardware wallet.

1. In Sparrow Wallet, click the **Receive** tab on the left-hand menu and locate the first receiving address (index 0).
2. On your hardware wallet, navigate to the address explorer:  
    - **Coldcard:** Go to **Address Explorer** from the main menu.
    - **Trezor/BitBox02:** Initiate a dummy transaction in Sparrow and verify the receive address shown on the device screen matches Sparrow.
3. If the addresses match perfectly, your hardware wallet is successfully synced to your personal node.