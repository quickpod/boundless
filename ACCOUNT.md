# Full Setup Guide: Sepolia Testnet USDC Transfers

This guide walks you through everything you need to prepare for testing USDC transfers on the Sepolia network—setting up a wallet, getting Sepolia ETH and USDC, and configuring your RPC endpoint.

> [!NOTE]
> If you're following the **Boundless Prover Quick Start**, you can skip staking here and refer to **Step 2** in the main guide when you're ready.

> [!NOTE]
> **Mainnet support is also available.** You can run the prover on Ethereum or Base Mainnet as well—just note that you’ll need **real USDC** (not test tokens) and actual ETH for gas.


## 1. Register for Alchemy & Get an RPC URL

* Visit [Alchemy](https://dashboard.alchemy.com/signup/) and create a free account. No credit card needed.
* After signing up, create a new **app/project**:

  * Choose a network:

    * **Sepolia (testnet)** – recommended for development
    * **Ethereum Mainnet** or **Base Mainnet** – if you're going live
  * Your app will generate an **RPC URL** like:
    `https://eth-sepolia.g.alchemy.com/v2/your-api-key`
* **Copy** this RPC URL—you’ll need it later to connect to your chosen network.


## 2. Create a Wallet & Get Your Private Key

* You can use wallets like **MetaMask**, **MyEtherWallet**, or **Trust Wallet**:

  * When you create a new wallet, it generates a **public address** and a **private key**.
  * Example with MetaMask:

    * Install the extension
    * Create a wallet and safely store the seed phrase
    * Reveal your private key from Account Settings (for use in development)
* Advanced users can also generate wallets via tools like:

  * [web3.js](https://web3js.readthedocs.io/)
  * [Ethereum Private Key Generator](https://github.com/Ethereum-private-key-generator)

> [!WARNING]
> Never share your private key. Store it offline or in a secure password manager.

## 3. Add the Network to MetaMask

In MetaMask, go to **Settings → Networks → Add Network** and choose:

### For Sepolia (Testnet)

| Field              | Value                                             |
| ------------------ | ------------------------------------------------- |
| Network Name       | Sepolia                                           |
| RPC URL            | `https://rpc.sepolia.org` *(or your Alchemy URL)* |
| Chain ID           | `11155111`                                        |
| Currency Symbol    | `ETH`                                             |
| Block Explorer URL | `https://sepolia.etherscan.io`                    |

### For Mainnet (Optional)

| Field              | Value                         |
| ------------------ | ----------------------------- |
| Network Name       | Ethereum Mainnet or Base      |
| RPC URL            | Use your mainnet Alchemy URL  |
| Chain ID           | `1` (Ethereum), `8453` (Base) |
| Currency Symbol    | `ETH`                         |
| Block Explorer URL | etherscan.io or basescan.org  |


## 4. Get Sepolia ETH from a Faucet

* **Alchemy Faucet:**

  * Log in to [Alchemy's faucet](https://www.alchemy.com/faucets/ethereum-sepolia)
  * Enter your wallet address and pass CAPTCHA
  * Receive up to **0.5 Sepolia ETH per day**
* **Alternative Faucets:**
  Other options include:

  * [QuickNode](https://faucet.quicknode.com/)
  * [sepoliafaucet.com](https://sepoliafaucet.com)

> [!WARNING]
> Some faucets may require at least **0.001 ETH (real ETH) on mainnet** to verify your wallet.

## 5. Get Sepolia USDC (10 USDC)

* **Circle Faucet:**

  * Go to [faucet.circle.com](https://faucet.circle.com)
  * Choose **Ethereum Sepolia**, paste your wallet address, and request tokens
  * You’ll receive **10 USDC every 24 hours**
* **Other Options:**

  * [thirdweb faucet](https://thirdweb.com/faucet) may also provide USDC on EVM-compatible testnets
  * Alternatively, deploy your own USDC mock contract if needed for advanced testing

> [!WARNING]
> **If you're using Mainnet**, you must acquire **real USDC** (e.g., from Coinbase or a DEX). Testnet faucets will not work on mainnet.

## 6. (Optional) Testnet Staking

* Staking isn’t required for basic transfers or faucet usage.
* If you’re using **Boundless Prover**, you’ll stake 10 USDC later in that setup.
* To experiment with staking, look for testnet-compatible staking dApps or deploy one yourself.

---

## 7. Why You Might Need 0.001 Mainnet ETH

Some faucets (like QuickNode) require your wallet to hold a tiny amount of **Ethereum Mainnet ETH** to prove it's not a bot. If needed, transfer or buy 0.001 ETH to meet this requirement.


## Summary Table

| Step             | What to Do                                          | Notes                           |
| ---------------- | --------------------------------------------------- | ------------------------------- |
| Register Alchemy | Create account and project, get your RPC URL        | Sepolia or Mainnet supported    |
| Create Wallet    | Use MetaMask or similar, back up key                | Store securely                  |
| Add Network      | Add Sepolia or Mainnet to wallet                    | Use correct RPC + chain ID      |
| Get Sepolia ETH  | Use faucet (Alchemy or others) to get test ETH      | Some may require mainnet ETH    |
| Get Sepolia USDC | Use Circle faucet for test USDC                     | 10 USDC per 24h                 |
| Use Mainnet USDC | Acquire real USDC for production                    | Faucets do not work for mainnet |
| Staking          | Not needed unless using Boundless Prover or similar | Covered in separate guide       |


You’re now fully equipped to test (or deploy) USDC transfers on Sepolia or Mainnet. When ready, continue to the [Boundless Prover guide](./README.md) to launch your node.
