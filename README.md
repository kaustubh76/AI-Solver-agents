# Nimble

Nimble is an AI‐agent‐based solver network that helps users get the best price for swaps and also supports deposits and withdrawals in Morpho vaults. The network is chain‐agnostic and has been demonstrated on [Base](https://base.org/) for this project. The solver agents are built with [Coinbase’s AgentKit](https://github.com/coinbase/agentkit), and the frontend is deployed on OpSec.

## Table of Contents

1. [Overview](#overview)  
2. [Architecture](#architecture)  
   - [High-Level Flow](#high-level-flow)  
   - [Swap Infrastructure](#swap-infrastructure)  
   - [Deposit and Withdraw Infrastructure](#deposit-and-withdraw-infrastructure)
3. [Features](#features)
4. [Usage](#usage)
   - [Swapping Assets](#swapping-assets)
   - [Depositing to Morpho Vaults](#depositing-to-morpho-vaults)
   - [Withdrawing from Morpho Vaults](#withdrawing-from-morpho-vaults)
5. [Project Status](#project-status)

## 1. Overview

Nimble orchestrates a network of AI solver agents to:

- Find optimal swap routes for users across multiple liquidity pools and DEXes.
- Automate yield optimization for deposits and withdrawals in Morpho vaults.

This project consists of:
- Nimble Frontend – A user interface that interacts with the backends (Swap, Deposit, Withdraw).
- Swap Backend – Collects quotes from multiple solver agents and executes swaps at the best price.
- Deposit Backend – Finds the best vault for Morpho deposits, ensures optimal yields, and handles the deposit process.
- Withdraw Backend – Retrieves user funds from Morpho vaults, returning tokens seamlessly.


## 2. Architecture

The Nimble architecture has three major components: Swap Infrastructure, Deposit Infrastructure, and Withdraw Infrastructure. These are orchestrated by the Nimble Frontend.

### 2.1 High-Level Flow


User -> Nimble Frontend -> (Swap Backend | Deposit Backend | Withdraw Backend) -> User

1. User interacts with the Nimble Frontend.  
2. Frontend forwards requests to the appropriate backend.  
3. Backend leverages one or more solver agents (built with Coinbase’s AgentKit) to:
   - Run an auction among solver agents.
   - Retrieve best route (for swaps) or best vault (for deposits).
   - Execute the transaction on-chain.
4. Result is returned to the user (swapped assets or updated vault balance).

![image](https://github.com/user-attachments/assets/1c57f852-00f5-4d46-83b0-42f476013ed5)


### 2.2 Swap Infrastructure

The swap flow is:

1. User approves token spending to the Swap Contract.
2. Solver Agents each propose a quote (e.g., price, route, etc.).
3. Swap Contract runs an auction to pick the best solver agent.
4. Winning Solver Agent executes the swap and sends funds back to the user.

![image](https://github.com/user-attachments/assets/9d1c51fb-bb4d-4adf-9335-5d92bc351458)


### 2.3 Deposit and Withdraw Infrastructure

1. User gives approval to the Deposit Contract or Withdraw Contract.
2. Solver Agents propose yields (for deposits) or methods (for withdrawals).
3. Deposit or Withdraw Contract chooses the best agent based on yield or other optimization criteria.
4. Winning Agent finalizes depositing or withdrawing on behalf of the user.

![image](https://github.com/user-attachments/assets/c60113e2-f9a3-49c1-b5c7-f7287fdc8c0c)




## 3. Features

- Multi-Chain Compatibility: Designed to work on any EVM-compatible chain.
- AgentKit Integration: Leverages [Coinbase’s AgentKit](https://github.com/coinbase/agentkit) to build AI-driven solver agents.
- Optimized Swaps: Runs an auction to always secure the best swap price.
- Morpho Vault Deposits/Withdrawals: Automates yield optimization by selecting the highest-yield vault at deposit time and the appropriate vault for withdrawal.
- End-to-End Operational: Deployed on [Base](https://base.org/) for demonstration, with a functioning frontend on OpSec.

## 4. Usage

### 4.1 Swapping Assets

1. On the Nimble Frontend, connect your wallet (MetaMask or similar).
2. Navigate to the Swap tab.
3. Select tokens to swap.
4. Approve the contract for token spending (if prompted).
5. Click Swap.  
   - Nimble runs an internal auction among solver agents (e.g., agent 1, agent 2, agent 3).
   - The best quote is displayed, and the swap is executed.
6. Receipt of transaction will show up once confirmed.

### 4.2 Depositing to Morpho Vaults

1. Go to the Deposit section in the frontend.
2. Approve the deposit contract (if needed).
3. Enter the amount to deposit.
4. Click Deposit.  
   - The deposit contract finds the best vault (via an auction among the solver agents).
   - Your assets are deposited into the chosen vault for optimal yield.

### 4.3 Withdrawing from Morpho Vaults

1. Navigate to the Withdraw section.
2. Approve if required.
3. Enter the amount (or select “withdraw all”).
4. Click Withdraw.  
   - Nimble chooses the correct vault and handles the withdrawal on your behalf.
   - Funds are returned to your wallet.

## 5. Project Status

- Alpha Release: The core functionality (swap, deposit, withdraw) is operational on Base for demonstration.  
- Next Steps:
  - Audit and security reviews.
  - Expand solver agent strategies for even better yields and swap quotes.
  - Expand to additional chains (e.g., Ethereum mainnet, Polygon, Arbitrum).

---

*Happy Swapping and Yielding!*
