# AMM

## Technology Stack & Tools

- Solidity (Writing Smart Contract)
- Javascript (React & Testing)
- [Hardhat](https://hardhat.org/) (Development Framework)
- [Ethers.js](https://docs.ethers.io/v5/) (Blockchain Interaction)

## Requirements For Initial Setup

- Install [NodeJS](https://nodejs.org/en/). We recommend using the latest LTS (Long-Term-Support) version, and preferably installing NodeJS via [NVM](https://github.com/nvm-sh/nvm#intro).

## Setting Up

### 1. Clone/Download the Repository

### 2. Install Dependencies:

`npm install`

### 3. Start Hardhat Node:

In your terminal run:
`npx hardhat node`

_As a reminder, do **NOT** use or fund the accounts/keys provided by the hardhat node in a real production setting, they are to be only used in your local testing!_

### 4. Deploy Smart Contract

In a separate terminal run:
`npx hardhat run scripts/deploy.js --network localhost`
