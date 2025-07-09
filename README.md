# 🐝 Quick Start: Boundless Prover on QuickPod
**Last updated:** July 9, 2025

---

## What You’ll Need

Before you begin, make sure you have:

* **10 USDC** in your wallet (on the correct network)
* An **RPC URL**, for example:
  `https://eth-sepolia.g.alchemy.com/v2/A1bC23dEfG456hiJkLmnOpQRsTuvWxYz`
* Your **wallet’s private key**, like:
  `5f6a2b8790ac134d47fe28bcad6150eb7f426b8d60a743dc5b0940fbea29c6d1`
* A **NETWORK** value that matches the network you're using (see below)

### Supported Networks

| Network          | `NETWORK` Value |
| ---------------- | --------------- |
| Base Mainnet     | `base`          |
| Base Sepolia     | `base-sepolia`  |
| Ethereum Sepolia | `eth-sepolia`   |

> [!WARNING]
> Make sure your USDC, wallet, and RPC endpoint are all on the **same network**

If you don't know what any of this means, please read the [Account Setup Guide](./ACCOUNT.md) first.

---

## 🚀 Step-by-Step: Launching on QuickPod

### 1. Create Your Pod

1. Go to [QuickPod Templates](https://console.quickpod.io/templates)

2. Click **Create New Template** to create a new template from scratch.

3. Fill in the template details:
   - **Template Type**: Select `GPU`
   - **Template Name**: Give it a name you like (e.g. `Boundless Prover`)
   - **Docker Image Path**: `ghcr.io/quickpod/boundless:latest`
   - **Disk Space**: Set to at least `50` GB

  ![image](https://github.com/user-attachments/assets/1286c59c-a7c9-41e9-b198-015ebfed337a)

4. In the **Docker Options** field, paste the following:

> [!WARNING]
> Replace the placeholder values below with your actual values from the prerequisites step:
   ```bash
   -e PRIVATE_KEY=your_private_key_here -e RPC_URL=https://eth-sepolia.g.alchemy.com/v2/your-api-key-here -e NETWORK=eth-sepolia -p 8082:8082 --shm-size=30g
   ```

   | Placeholder | Replace With |
   | ----------- | ------------ |
   | `your_private_key_here` | Your actual wallet private key |
   | `your-api-key-here` | Your actual Alchemy API key from the RPC URL |
   | `eth-sepolia` | Your chosen network value (see supported networks table above) |

   Then hit **Save**.

   ![image](https://github.com/user-attachments/assets/71382587-32e5-447c-bba2-826a8b40fd59)

5. Launch a machine using your new template.

![image](https://github.com/user-attachments/assets/95bf6229-d841-4bb3-914b-6e5c9b40e6c7)

## Step 2: Stake 10 USDC

> [!NOTE]
> *You can skip this step if you’ve already staked from this wallet.*

Once your pod is running:

1. SSH into the container.
   ![image](https://github.com/user-attachments/assets/806b56b7-4b31-47bb-a2a5-8636897d6156)

3. Run the staking command:

   ```bash
   boundless account deposit-stake 10
   ```

You should see a message confirming the stake was successful.
![stake](https://github.com/user-attachments/assets/38567b4a-2339-44eb-9458-919188224a33)

### Verify Your Stake

You can verify your stake by visiting the appropriate explorer:

| Network Type | Explorer URL |
| ------------ | ------------ |
| **Testnet** | https://explorer.testnet.beboundless.xyz/balances |
| **Mainnet** | https://explorer.beboundless.xyz/balances |

![image](https://github.com/user-attachments/assets/05772bf4-f214-484e-99c9-b2375aa220df)

## Step 3: Restart the Services

> [!NOTE]
> *Skip this if services are already running from a previous stake.*

After staking, restart the services:

```bash
supervisorctl restart all
```

This ensures the prover loads with the updated state.

## Step 4: Check the Broker Logs

Open your browser and go to:

![image](https://github.com/user-attachments/assets/d68041c1-e762-492b-8742-56082158305f)

![image](https://github.com/user-attachments/assets/344a68fb-2e32-484c-8cee-39dc17c42989)


You should see the Boundless broker UI showing your prover’s status.

Other commands:
```bash
# check errors
cat /var/log/supervisor/broker_error.log

# check broker logs
tail -f /var/log/supervisor/broker.log

# check service status
supervisorctl status

# restart all services then check status again
supervisorctl restart all
supervisorctl status
```

