# AMM — Automated Market Maker DApp

A full-stack decentralized exchange built around a Uniswap-style **Automated Market Maker (AMM)**. Users can swap between two ERC-20 tokens, provide liquidity to earn pool shares, withdraw their liquidity, and view price/trade history — all backed by smart contracts running on a local Ethereum (Hardhat) network.

The AMM uses the **constant-product formula** (`x * y = k`) to price trades: the product of the two token reserves is held constant, so swapping one token for the other moves the price along the curve automatically, with no order book or counterparty.

## Features

- **Swap** — trade Circa Coin (CRCA) ↔ USD Token (USD) at the price set by the pool
- **Deposit** — add liquidity to the pool and receive proportional LP shares
- **Withdraw** — burn shares to remove your liquidity from the pool
- **Charts** — view swap history and price movement over time
- **MetaMask integration** — connect a wallet, sign transactions, and track balances

## Technology Stack & Tools

- **Solidity** `0.8.9` — smart contracts
- **[Hardhat](https://hardhat.org/)** — development, testing & deployment framework
- **[Ethers.js v5](https://docs.ethers.io/v5/)** — blockchain interaction
- **React 18** — frontend UI
- **Redux Toolkit** + **redux-thunk** — application state management
- **React-Bootstrap** — UI components and styling
- **[ApexCharts](https://apexcharts.com/)** — price & history charts

## Project Structure

```
contracts/        Solidity smart contracts
  ├─ AMM.sol      Core market maker: liquidity, swaps, shares
  └─ Token.sol    Minimal ERC-20 token used for the two pool assets
scripts/
  ├─ deploy.js    Deploys the two tokens and the AMM contract
  └─ seed.js      Funds accounts, adds liquidity, and runs sample swaps
test/             Hardhat/Mocha tests for the AMM and Token contracts
src/
  ├─ components/  React UI (Swap, Deposit, Withdraw, Charts, Navigation…)
  ├─ store/       Redux store, reducers, selectors, and contract interactions
  ├─ abis/        Compiled contract ABIs consumed by the frontend
  └─ config.json  Per-network contract addresses (31337 = Hardhat local)
```

### Smart Contracts

- **`Token.sol`** — a minimal ERC-20 implementation (`transfer`, `approve`, `transferFrom`, allowances). Two instances are deployed as the tradable assets: **CRCA** (Circa Coin) and **USD** Token.
- **`AMM.sol`** — the market maker. It holds the two-token liquidity pool and exposes:
  - `addLiquidity` / `removeLiquidity` — deposit or withdraw liquidity in exchange for pool shares
  - `swapToken1` / `swapToken2` — swap one token for the other along the constant-product curve
  - `calculateToken1Deposit` / `calculateToken2Deposit` — compute the matching deposit amount
  - `calculateToken1Swap` / `calculateToken2Swap` — quote the output of a swap
  - emits a `Swap` event used to build the trade history charts

## Requirements For Initial Setup

- Install [NodeJS](https://nodejs.org/en/). We recommend using the latest LTS (Long-Term-Support) version, and preferably installing NodeJS via [NVM](https://github.com/nvm-sh/nvm#intro).
- A browser wallet such as [MetaMask](https://metamask.io/) to interact with the frontend.

## Setting Up

### 1. Clone/Download the Repository

### 2. Install Dependencies

```
npm install
```

### 3. Start a Hardhat Node

In a terminal, run:

```
npx hardhat node
```

_As a reminder, do **NOT** use or fund the accounts/keys provided by the Hardhat node in a real production setting — they are for local testing only._

### 4. Deploy the Smart Contracts

In a separate terminal, run:

```
npx hardhat run scripts/deploy.js --network localhost
```

This deploys the two tokens and the AMM. Make sure the deployed addresses match those in `src/config.json` for chain id `31337` (the default Hardhat addresses already match a fresh node).

### 5. Seed the Exchange (optional but recommended)

Populate the pool with liquidity and a few sample swaps so the UI and charts have data:

```
npx hardhat run scripts/seed.js --network localhost
```

### 6. Start the Frontend

```
npm start
```

This launches the React app at [http://localhost:3000](http://localhost:3000). Connect MetaMask to the **Localhost 8545** network (chain id `31337`) and import one of the Hardhat test accounts to start swapping and providing liquidity.

## Running Tests

Run the contract test suite with Hardhat:

```
npx hardhat test
```
