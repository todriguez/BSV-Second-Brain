# [[Consensus Rules]]

**Consensus Rules** are the foundational principles that govern the operation and validation of transactions and blocks on the [[BSV Blockchain]] network. These rules ensure that all participants agree on the state of the blockchain and maintain its integrity.

---

## Immutable Rules: "Set in Stone"

Under the BSV paradigm, consensus rules are **"set in stone"**, adhering to [[Satoshi Nakamoto]]'s original vision for Bitcoin as a stable and scalable protocol. Unlike other blockchain networks, which frequently alter their rules, BSV emphasizes stability, allowing developers and businesses to build with confidence.

- **Chronicle Upgrade**:  
  The upcoming [[Chronicle Upgrade]] will restore the last of the original opcodes and mark the final significant [[Hard Fork]] in the BSV network. After this, the protocol will remain unchanged, with no further alterations to consensus rules.

---

## What Are Consensus Rules?

Consensus rules define the validation criteria for:

1. **Transactions**:  
   Transactions must adhere to specific criteria to be considered valid, such as spending only unspent transaction outputs ([[UTXO]]) and meeting [[Script]] conditions.

2. **Blocks**:  
   Blocks must be validly constructed, include a valid [[Coinbase Transaction]], and adhere to size and timestamp constraints.

3. **Network Behavior**:  
   Nodes must follow rules for propagating and validating transactions and blocks to maintain network integrity.

---

## Hard Forks and Soft Forks

### Hard Forks

A **[[hard fork]]** occurs when changes are made to the consensus rules in a way that makes the new rules incompatible with the old ones. Nodes must upgrade to the new rules to remain part of the same network. 

- In BSV, hard forks have been used sparingly and only for protocol restoration, such as the [[Genesis Upgrade]] and the upcoming [[Chronicle Upgrade]].
- Hard forks on BSV are transparent, planned events designed to restore or complete Satoshi's original design.

### Soft Forks

**[[Soft forks]]** are often described as backward-compatible changes to the consensus rules. However, in reality, they are protocol alterations that tighten existing rules, often introducing subtle complexities or limitations.

- The term "soft fork" is viewed critically in the BSV, as it can obscure the true nature of protocol changes.
- Soft forks lead to centralization by creating dependencies on a subset of miners, developers or nodes.

---

## Core Consensus Rules in BSV

### 1. **Proof of Work**
   - [[Proof of Work]] (PoW) is the mechanism by which miners compete to solve complex mathematical puzzles, earning the right to add a new block to the chain. It ensures energy-backed security and prevents [[Double Spending]].

### 2. **Valid Transactions**
   - Transactions must spend only existing and unspent [[UTXO]]s.
   - Inputs must satisfy [[Script]] conditions (e.g., correct unlocking script).
   - The sum of output values must not exceed the sum of input values, with the difference allocated as [[Miner Fees]].

### 3. **Block Size**
   - There is no fixed block size limit in BSV; miners determine block size policies based on market demands.
   - Larger blocks must still meet technical constraints, such as timely propagation and validation.

### 4. **Block Validity**
   - A block must:
     - Reference the previous block hash.
     - Include a valid [[Coinbase Transaction]].
     - Contain only valid transactions.
     - Have a timestamp greater than the median of the previous 11 blocks.

### 5. **Longest Honest Chain Rule**
   - The chain with the most cumulative proof of work is considered the valid chain. This ensures an objective measure of consensus.

### 6. **First-Seen Rule**
   - While not a strict consensus rule, the **first-seen rule** is an emergent principle based on economic incentives and honest node behavior. Nodes propagate the first valid transaction they see for a given [[UTXO]], rejecting conflicting transactions.

### 7. **Network Protocol**
   - Nodes must follow [[Simplified Payment Verification]] principles, using headers and Merkle proofs for lightweight validation.
   - [[Double-Spend Proofs]] ensure that conflicting transactions are detected and resolved efficiently.

---

## Challenges and Economic Principles

Consensus rules on BSV are designed to align with economic incentives, ensuring that:

- Miners are rewarded for honest behavior through [[Transaction Fees]] and block rewards.
- Users can rely on the network's stability and predictable behavior.

Efficient management of the [[UTXO Set]], propagation of large blocks, and adherence to consensus rules all contribute to a scalable, secure, and reliable blockchain.

---

## Tags

- [[Consensus Rules]]  
- [[BSV Blockchain]]  
- [[Proof of Work]]  
- [[Genesis Upgrade]]  
- [[Chronicle Upgrade]]  
- [[Hard Forks]]  
- [[Soft Forks]]  
- [[UTXO]]  
- [[Script]]  
- [[Double-Spend Proofs]]  
- [[Simplified Payment Verification]]  
