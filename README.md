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

2. Find the **`Boundless Prover`** template. Click **Clone**, then give it a name you like (e.g. `Boundless Prover Personal`).

   ![Clone Template](https://github.com/user-attachments/assets/3c9aa89e-33e2-4b92-a92e-d2e15ea09679)

3. In the Docker settings, paste the following:

> [!WARNING]
> Replace the placeholder values below with your actual values from the prerequisites step:

   ```bash
   -e PRIVATE_KEY=your_private_key_here \
   -e RPC_URL=https://eth-sepolia.g.alchemy.com/v2/your-api-key-here \
   -e NETWORK=eth-sepolia \
   -p 8082:8082 \
   --shm-size=30g
   ```

   Then hit **Save**.

   ![Docker Settings](https://github.com/user-attachments/assets/5d72d55e-b7c5-4fda-a976-7f3bcc6c59b7)

4. Under **Disk Space**, set it to at least `50` GB.

5. Launch a machine using your new template.

   ![Select Template](https://github.com/user-attachments/assets/31ab3b50-1908-4425-b660-7072eb936b64)

## Step 2: Stake 10 USDC

> [!NOTE]
> *You can skip this step if you’ve already staked from this wallet.*

Once your pod is running:

1. SSH into the container.
2. Run the staking command:

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

```
http://localhost:8082
```

You should see the Boundless broker UI showing your prover’s status.
