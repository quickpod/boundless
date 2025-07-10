# 🐝 Quick Start: Boundless Prover on QuickPod
**Last updated:** July 11, 2025
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

2. Search for `boundless` and `Clone` the template
   ![image](https://github.com/user-attachments/assets/d5c18a81-2580-4ebf-b54e-083d217b9881)

4. In the **Docker Options** edit the following

> [!WARNING]
> Replace the placeholder values below with your actual values from the prerequisites step:

   | Placeholder | Replace With |
   | ----------- | ------------ |
   | `YOUR_PRIVATE_KEY_GOES_HERE` | Your actual wallet private key |
   | `YOUR_RPC_URL_HERE` | Your actual  RPC URL |
   | `eth-sepolia` | Your chosen network value (see supported networks table above) |

   Then hit **Save**.

   ![image](https://github.com/user-attachments/assets/33231092-f36c-45b6-9c26-09a59e89dc7a)

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

## FAQ

1. **Where is the `docker-compose.yml` file?**
   This setup does **not** use Docker or `docker-compose`.
   Instead, services are managed using **Supervisor**.
   You can configure which services run by editing:

   ```
   /app/supervisord.conf
   ```

   After making changes, restart all services with:

   ```bash
   supervisorctl restart all
   ```

2. **How do I restart a specific service (like the broker)?**
   Use this command format:

   ```bash
   supervisorctl restart <service-name>
   ```

   For example, to restart the broker service:

   ```bash
   supervisorctl restart broker
   ```

3. **Where can I edit the `broker.toml` configuration?**
   The file is located at:

   ```
   /app/broker.toml
   ```

   You can edit it using a text editor:

   * With **nano** (beginner-friendly):

     ```bash
     nano /app/broker.toml
     ```
   * Or with **vi** (more advanced):

     ```bash
     vi /app/broker.toml
     ```

4. **How can I check logs?**
   Logs for all services are in:

   ```
   /app/logs
   ```

   You can view them using:

   * To view the full log:

     ```bash
     cat /app/logs/<filename>.log
     ```
   * To scroll through:

     ```bash
     less /app/logs/<filename>.log
     ```
   * To follow logs in real time:

     ```bash
     tail -f /app/logs/<filename>.log
     ```

5. **How do I increase the number of `exec_agents`?**
   You can add the following option when starting the container:

   ```bash
   -e AGENTS=<number>
   ```

   By default, it runs with 2 agents. For example, to run 4 agents:

   ```bash
   -e AGENTS=4 ...
   ```

6. **How do I update CPU or memory limits?**
   Currently, there is **no built-in way to limit resource usage**.
   All processes will share the available CPU and memory of the container.

7. **What settings should I use for my GPU?**
Update your docker options with the proper segement size based on the table below:
```
-e SEGMENT_SIZE=16
```

| GPU Memory | Recommended Segment Size | Memory Used | Cycles | Performance | Common GPU Models |
|------------|-------------------------|-------------|---------|-------------|-------------------|
| 1-2GB      | **16**                  | ~512MB      | 65K     | Basic       | GTX 1050, RTX 3050 (4GB) |
| 2-4GB      | **17**                  | ~1GB        | 131K    | Good        | GTX 1060, RTX 3060 Ti |
| 4-6GB      | **18**                  | ~2GB        | 262K    | Better      | GTX 1070, RTX 3060 |
| 6-8GB      | **19**                  | ~4GB        | 524K    | Great       | GTX 1080, RTX 3070 |
| 8-12GB     | **20**                  | ~6GB        | 1M      | Excellent   | RTX 3080, RTX 4070 |
| 12GB+      | **21** (default)        | ~7GB        | 2M      | Maximum     | RTX 3080 Ti, RTX 4080, RTX 4090 |
| 16GB+      | **22**                  | ~12GB       | 4M      | Overkill    | RTX 4090, A100 |
| 24GB+      | **23**                  | ~20GB       | 8M      | Enterprise  | RTX 6000, A100 |

