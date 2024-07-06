# AnonPay_masternode

## Local Wallet Setup
This section guides you through setting up your local or control wallet. If you already have the AnonPay core wallet running, you can skip to the next section.
﻿
### 1. Install and Sync Local Wallet:
- Download the latest AnonPay wallet from [https://github.com/AnonPayOfficial/AnonPay](https://github.com/AnonPayOfficial/AnonPay)
- Create a new directory:
- Windows: `C:\Users\AppData\Roaming\AnonPayCore`
- Linux/MAC: `~/.anonpaycore`
- If you have an existing AnonPay wallet, remove the following folders before using the bootstrap (ensure the wallet is closed before doing this):
- `blocks`
- `chainstate`
- `evodb`
- `llmq`
- Start the wallet and let it finish syncing.
- Encrypt the wallet via **Settings > Encrypt Wallet**.
- Create a new receiving address.
- Backup `wallet.dat` via **File > Backup Wallet**. Store it in multiple locations.
- Dump the private key for the receiving address (this should be printed and stored offline in multiple locations):
- `walletpassphrase yourpassword time_in_seconds`
- `dumpprivkey "your_address"` (replace "your_address" with your actual receiving address)
- Send 1000 ANP to yourself (this is the current collateral amount).
- Wait for 1 confirmation.
- Note: The private key only allows you to restore the matching receiving address. If you set up multiple nodes, you should dump the private key for each collateral receiving address.
﻿
### 2. Build protx command for control wallet
Example protx quick_setup command:
`protx quick_setup "transaction_id" "1" "your_smartnode_server_IP:38096" "fee_address"`
- Structure:
- Transaction ID: In your wallet, go to **Transactions**, right-click the one you sent to yourself earlier, and **Copy Transaction ID**.
- Collateral index: In **Tools > Debug console**, type `smartnode outputs` to check if 1 or 0. Adjust the command if needed.
- Your smartnode server IP and port: Replace the example IP with your Smartnode server IP, keep the port as is.
- Fee address: This is any address in your wallet which contains enough ANP to pay the fee. Use `listaddressbalances` in the Debug console to find an address and replace it in the example command.
- Enter the `protx quick_setup` command in Debug console. This will create a .conf file for that node in the directory from which you ran the wallet. Open it and copy the contents.
﻿
### Finish Smartnode Configuration (VPS):
- Stop the daemon: `~/.anonpay-cli stop`
- Edit the configuration file: `nano ~/.anonpaycore/anonpay.conf`
- Paste the contents from the .conf file made during the protx command, save, and exit.
- Start anonpayd: `~/./anonpayd`
- After two minutes, check status: `~/./anonpay-cli smartnode status`
- You should see: `Ready Ready`
- Your Smartnode is now running!
﻿
