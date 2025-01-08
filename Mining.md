## Introduction

**Mining** is the process by which nodes in the [[Bitcoin Network]] assemble newly broadcast [[Bitcoin Transactions]] into a data structure called a [[block]]. Nodes then compete to append their block to the public [[Blockchain]] by repeatedly mutating the block's [[Block header]] data structure, usually by incrementing the [[nonce]] field. They then hash the block header in an attempt to find a value that satisfies a difficult [[Proof of Work]].

When a node discovers a valid proof-of-work hash for a block, it broadcasts the block to all other nodes. These nodes validate the block by ensuring that:

1. All [[transactions]] within the block are valid.
2. None of the transactions have already been included in a previous block.

Upon validation, nodes signal acceptance by building upon the block to create the next block in the chain.

Each block is [[timestamped]] and references the hash of the preceding block, forming a backward-reinforcing, [[timechain]] structure — the precursor to the term [[Blockchain]]. This structure ensures that:

- Transactions are computationally and economically impractical to modify, providing [[immutability]].
- An authoritative order of transactions is maintained, protecting users from [[double-spending]] attempts.

The mining process underpins these qualities and is the cornerstone of [[Bitcoin]]'s security and functionality.

---

## Nodes

**Nodes** are entities running software that performs mining functions, enforces the [[Bitcoin Protocol]] rules, and propagates data across the [[P2P Network]]. Nodes can be categorized into:

1. **Mining Nodes:**
    - Assemble [[Block]] and perform [[Proof of Work]] to add blocks to the [[Blockchain]].
    - Author and enforce the Bitcoin [[ledger]].
2. **Non-Mining Nodes:**
    - Run node client software but do not perform mining tasks.
    - Often used for [[block explorers]], [[payment gateways]], and archival purposes.

### Historical Note

The term "miner" and the concept of "mining" are not mentioned in the original [[Bitcoin Whitepaper]]. Instead, these terms describe the activities outlined in Section 5, where [[nodes]] are responsible for the network's operation.

---

## Mempool

Before a transaction is included in the [[Blockchain]], it resides in a miner's **[[mempool]]**.

### Key Characteristics:

- Each miner maintains their own mempool, leading to variations across miners.
- Mempools hold transactions grouped in different ways, including:
    - Transactions ready for the next block.
    - Transactions awaiting specific conditions (e.g., [[nLockTime]] or [[nSequence]]).
    - Transactions deemed invalid.

### Mining Candidate Creation

Miners select transactions from their mempool to create a candidate block:

1. Transactions are hashed into a [[Merkle Tree]] structure, resulting in a [[Merkle Root]].
2. The Merkle Root is included in the [[Block header]], which miners hash in search of a valid [[Proof of Work]].

---

## Hashing

**Hashing** is a cryptographic function that converts input data into a fixed-length [[hash value]] representing the original data.

### Properties of Hashing:

- **One-way Function:** The original input cannot be derived from the hash.
- **Deterministic:** The same input always produces the same output.
- **Sensitive to Input Changes:** Any change, even a single bit, results in a completely different hash.

In Bitcoin, miners hash the 80-byte [[Block header]] using the **[[SHA-256]]** algorithm twice, a process called [[SHA-256d]].

---

## Proof of Work

Bitcoin's [[Proof of Work]] mechanism requires miners to find a valid hash for the [[Block header]].

### Validation Criteria:

- The hash must be less than the [[Target]], a value specified in the block's [[Bits]] field.
- The target adjusts dynamically to ensure an average block creation time of 10 minutes.

### Computational Investment

Due to the vast target space, miners invest heavily in:

- Specialized hardware (e.g., [[ASIC]]).
- Electricity for computational power.

This investment forms the basis of Bitcoin's **proof-of-work** system, making it computationally expensive to attack the network.

---

## Incentives

The first transaction in every block is the **[[Coinbase Transaction]]**, which rewards the miner with:

1. A [[block subsidy]], which halves approximately every four years ([[halving]]).
2. The sum of all [[transaction fees]] within the block.

---

## Competition and Propagation

When a miner finds a valid proof-of-work:

1. They broadcast the block to the network.
2. Competing miners validate the block and, if valid, begin mining on top of it.

### Orphan Blocks

If multiple miners produce valid blocks simultaneously, only one becomes part of the [[longest chain]], while the others are classified as [[Orphan Blocks]].

---

## Pooled Mining

In **[[pooled mining]]**, miners contribute their computational resources to a pool:

- A coordinating node distributes [[block templates]] with unique nonce ranges to participants.
- Participants perform [[Proof of Work]], and rewards are distributed proportionally to their contributions.

This system aligns with [[Nakamoto Consensus]] by allowing hash operators to reallocate their resources if the pool does not align with their profitability or rule-set preferences.

### Stratum Protocol

The **[[Stratum]]** protocol facilitates communication between mining pools and individual miners, enabling efficient coordination.

---

## Related Concepts

- [[Blockchain]]
- [[Proof of Work]]
- [[Merkle Tree]]
- [[Double-Spending]]
- [[Mempool]]
- [[Bitcoin Transactions]]
- [[Timechain]]
- [[Orphan Blocks]]
- [[P2P Network]]

---

#Tags: #Bitcoin #Mining #Nodes #ProofOfWork #Blockchain #Mempool #Hashing #Stratum #DoubleSpending #NakamotoConsensus