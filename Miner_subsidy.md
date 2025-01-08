# Miner Subsidy

The **Miner Subsidy** is the reward that miners receive for successfully mining a block on the [[Blockchain]]. It is part of the **[[Coinbase]]** Transaction, which is the first transaction in a block and defines the release of new coins into circulation according to a scheduled protocol.

---

## Issuance of Coins

All [[Satoshis]] in the BSV network were issued in the [[Genesis Block]] by [[Satoshi Nakamoto]]. These coins are not distributed all at once but are gradually released via the **block subsidy**, which ensures a controlled introduction of coins into circulation.

---

## The Subsidy Schedule

The miner subsidy follows a predefined release schedule:

1. **Block Subsidy**: Initially set at 50 Bitcoin per block in the original protocol.  
2. **Halving Schedule**: The subsidy halves approximately every 210,000 blocks (~4 years).  
   - Example: After the first halving, the subsidy dropped to 25, then to 12.5, and now stands at 6.25 Bitcoin per block.

This schedule is not designed to create scarcity but to incentivize miners to contribute computational resources during the network's early stages, providing security and bootstrapping the ecosystem.

---

## Miner Subsidy in the Coinbase Transaction

The miner subsidy forms part of the [[Coinbase]] transaction, which:

1. Includes the block reward, consisting of:  
   - The block subsidy (newly minted satoshis).  
   - [[Transaction Fees]] collected from all transactions included in the block.

2. Ensures that all coins are traceable to their origin in the coinbase transaction. The subsidy is distributed as part of this transaction to reward the miner who successfully creates the block.

---

## Importance of Miner Subsidy

The miner subsidy serves several critical functions:

- **Bootstrapping the Network**:  
  Provides an incentive for miners to contribute computational resources in the network's early stages.

- **Security Through Incentives**:  
  Rewards miners for validating transactions and adding them to the blockchain, maintaining the integrity of the network.

- **Controlled Coin Release**:  
  Introduces coins into circulation at a predictable rate, aligning with the [[Bitcoin Protocol]]'s design.

---

## Transition to Transaction Fees

As the block subsidy decreases due to the [[Halving Schedule]], transaction fees will replace it as the primary incentive for miners. The Bitcoin SV network's scalability ensures high transaction throughput, allowing fees to remain low for users while sustaining miner rewards.

---

## Tags
- [[Miner Subsidy]]
- [[Genesis Block]]
- [[Coinbase Transaction]]
- [[Halving Schedule]]
- [[Transaction Fees]]
- [[Bitcoin Economics]]
