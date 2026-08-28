# FINOVA Blockchain Management Committee Recruitment Task


---

## Technical Keywords & Core Concepts

| Category | Key Technologies & Concepts Included |
| :--- | :--- |
| **Blockchain Networks** | Ethereum Layer 2, Arbitrum One, EVM Compatibility |
| **Token Standards** | ERC-20 (Stablecoins), ERC-3643 (Permissioned Tokens), ZK-Identity Credentials |
| **DeFi & Smart Contracts** | Atomic Swaps, Automated Market Makers (AMM), Payment Router Contracts, Liquidity Pools |
| **Infrastructure & Security** | Chainlink Oracles, Proof-of-Work (PoW), SHA-256 Hashing, Single Point of Failure Elimination |
| **Compliance & Off-Chain** | Fiat On/Off-Ramps, KYC Attestation Tokens, SEPA Instant / FedNow Payment Rails, Fallback API Routing |

---

## Task 1: Cross-Border B2B Payments & Settlements (PayX)

### Problem Statement
Traditional cross-border payments rely on the legacy SWIFT network and a chain of correspondent banks. This setup creates **high fees (3–7%)**, **slow settlement times (2–5 business days)**, **lack of real-time tracking**, and **trapped liquidity** in pre-funded Nostro/Vostro bank accounts.

### Solution Overview
**PayX** is a decentralized liquidity and settlement dApp that enables real-time, low-cost cross-border payments using 1:1 fiat-backed stablecoins (USDC/EURC) and Automated Market Maker (AMM) liquidity pools on an Ethereum Layer-2 network.

---

### 1. Complete Architecture & Workflow

#### System Architecture Diagram

```text
+-----------------------------------------------------------------------------------+
|                               OFF-CHAIN ENVIRONMENT                               |
|                                                                                   |
|  [ Sender (USD) ] ---> ( FinTech API / ERP Integration )                          |
|                                     |                                             |
|                                     v                                             |
|                             [ Banking Rail ]                                      |
|                                     | (Fiat Deposit via FedNow / ACH)             |
|                                     v                                             |
|                          [ On-Ramp / Off-Ramp Partner ]                           |
+-------------------------------------|---------------------------------------------+
                                      | ( Mints / Releases USDC )
                                      v
+-----------------------------------------------------------------------------------+
|                               ON-CHAIN ENVIRONMENT                                |
|                                                                                   |
|                           [ PayX Smart Contract ]                                 |
|                                     |                                             |
|                 +-------------------+-------------------+                         |
|                 |                                       |                         |
|                 v                                       v                         |
|      [ Liquidity Pool: USDC/EURC ]               [ Chainlink Oracle ]             |
|                 | (Atomic Swap)                         | (Real-time FX Rates)    |
|                 +-------------------+-------------------+                         |
|                                     |                                             |
|                                     v                                             |
|                       [ Destination Token: EURC ]                                 |
+-------------------------------------|---------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
|                               OFF-CHAIN ENVIRONMENT
