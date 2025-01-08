
A **Mining Pool** is a collaborative arrangement where a coordinating [[Node]] partners with multiple hashers to collectively mine blocks on the [[Blockchain]]. This coordination enables individual hashers to contribute their computational resources without needing to operate as a full node, while the mining pool node manages the complex tasks of block assembly and network participation.

---

## How a Mining Pool Works

In a mining pool, the **node** acts as the coordinating entity. The node satisfies the six steps outlined in Section 5 of the [[Bitcoin Whitepaper]], which define a node's responsibilities in the Bitcoin network:

1. Collecting transactions into a block.  
2. Solving the Proof-of-Work for the block.  
3. Broadcasting the block to other nodes.  
4. Accepting valid blocks from peers.  
5. Maintaining a full copy of the blockchain.  
6. Validating all transactions and blocks according to [[Consensus Rules]].

### Service Agreements with Hashers

Mining pools enter agreements with hashers to rent their computational resources (hashpower). Hashers do not need to maintain the full functionality of a node; instead, they rely on the mining pool's node for tasks like:

- Assembling block templates.
- Managing the [[UTXO Set]] and transaction mempool.
- Ensuring compliance with [[Consensus Rules]].

Hashers, in turn, perform Proof-of-Work calculations on the block templates provided by the mining pool node.

---

## Block Templates and Mining Candidates

The mining pool node prepares **block templates**—partially constructed blocks with:

- A header containing the previous block hash.
- A [[Coinbase Transaction]] that includes the miner's subsidy and transaction fees.
- A list of [[Transactions]] from the mempool.

These block templates are distributed to hashers, each with unique parameters (e.g., a portion of the nonce space) to prevent duplication of Proof-of-Work efforts. Hashers then iterate over the nonce or update their candidate templates as new transactions or [[Timestamps]] are received.

---

## Hashers vs. Nodes

It is critical to understand that **not all hashers are nodes**. While hashers contribute computational resources to solve the Proof-of-Work puzzle, only the mining pool's coordinating entity is considered a node. A **node**:

- Participates fully in the Bitcoin network, broadcasting and validating blocks and transactions.
- Maintains the full blockchain.
- Follows all steps of the [[Bitcoin Protocol]].

Hashers rely on the mining pool node for these functions and focus solely on the Proof-of-Work computation.

---

## Importance of Mining Pools

### Efficiency and Coordination

Mining pools optimize the mining process by dividing the computational task across multiple hashers. This reduces duplication of effort and ensures faster block discovery.

### Resource Accessibility

For individual miners, joining a mining pool provides access to the mining rewards without the need to operate a full node or compete against larger-scale operations.

---

## Tags
- [[Mining Pool]]
- [[Node]]
- [[Hashing]]
- [[Proof of Work]]
- [[Block Template]]
- [[Bitcoin Protocol]]
- [[Bitcoin Whitepaper]]
- [[Consensus Rules]]
