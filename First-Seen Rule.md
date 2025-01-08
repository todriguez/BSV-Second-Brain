# First-Seen Rule

The **First-Seen Rule** is a fundamental principle in the [[Bitcoin Protocol]] that governs the acceptance of transactions by nodes in the network. It ensures that once a transaction is broadcast and validated, it is the only version of that transaction recognized as valid. This mechanism plays a critical role in maintaining the integrity, reliability, and orderliness of the [[UTXO Model]].

---

## What is the First-Seen Rule?

The First-Seen Rule dictates that:

1. **A transaction with a given [[TXID]]** (transaction identifier) is accepted only once by the network.
2. **Subsequent transactions** that attempt to spend the same [[UTXO]] (Unspent Transaction Output) are rejected as potential double spends.

This ensures that each UTXO is spent only once and that the network operates in a predictable and consistent manner.

---

## How It Works

1. **Transaction Broadcast**:
   - When a valid transaction is broadcast to the network, it is added to the **mempool** (memory pool) of a node.
   - The transaction locks the referenced UTXOs, preventing them from being spent again.

2. **First-Seen Validation**:
   - Nodes validate the transaction by checking:
     - Its syntax and structure.
     - That it does not conflict with other transactions in the mempool or blockchain.
   - If another transaction with the same inputs is received later, it is discarded as invalid.

3. **Block Inclusion**:
   - Miners build a [[Merkle Tree]] from the ordered transactions of the [[mempool]] to include in a block.
   - The first valid transaction seen by the network is the only one eligible for inclusion.

---

## Importance of the First-Seen Rule

1. **Prevention of Double-Spends**:
   - Ensures that no UTXO is spent more than once.
   - Protects the network from conflicting transactions that could undermine trust.

2. **Orderliness**:
   - Establishes a clear and deterministic process for handling transactions.
   - Avoids ambiguity in which version of a transaction is valid.

3. **Security**:
   - Strengthens the integrity of the blockchain by disallowing conflicting transactions.
   - Works in conjunction with the [[Chain of Digital Signatures]] to provide an unbroken history of ownership.

---

## Interaction with the Honest Chain

The First-Seen Rule complements the concept of the [[Honest Chain]], ensuring that only valid transactions meeting consensus rules are processed. Transactions attempting to bypass the First-Seen Rule, such as double spends or malicious forks, are inherently invalid and excluded from the blockchain.

---

## Economic Implications

1. **Incentivizing Honest Behavior**:
   - Miners are incentivized to process the first valid transaction they receive to maximize efficiency and rewards.

2. **Fairness in Transaction Processing**:
   - Ensures a level playing field by giving priority to the first valid broadcast of a transaction.

3. **Discouraging Fraud**:
   - Reduces the viability of attacks that attempt to replace or overwrite previously seen transactions.

---

## Applications and Use Cases

1. **Payment Channels**:
   - The First-Seen Rule is critical in [[Micropayment Channels]], where the final state of a channel relies on honoring the first valid transaction.

2. **Smart Contracts**:
   - Enforces transaction logic in [[Smart Contract]] by ensuring deterministic behavior.

3. **SPV (Simplified Payment Verification)**:
   - Allows [[Simplified Payment Verification]] wallets to verify transactions securely, knowing that the First-Seen Rule has already filtered out conflicting transactions.

---

## Tags

#FirstSeenRule #BitcoinProtocol #UTXOModel #TransactionValidation #BlockchainIntegrity #DoubleSpendPrevention #HonestChain #Mempool

---

## See Also

- [[Bitcoin Protocol]]
- [[UTXO Model]]
- [[Chain of Digital Signatures]]
- [[Simplified Payment Verification]]
- [[Honest Chain]]
- [[Micropayment Channels]]
- [[Transaction Validation]]
