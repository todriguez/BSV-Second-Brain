A **block** is one of the two fundamental network events in the Bitcoin system (the other being transactions). Blocks serve as containers that batch and organize [[Bitcoin Transactions]], securing them into the blockchain through [[Proof of Work]].

---

### Structure of a Block

A Bitcoin block consists of three main components:
1. **Header**: 80 bytes of metadata describing the block.
2. **Transaction Count**: A variable-length integer (varInt) specifying the number of transactions in the block.
3. **Transactions**: A sequence of raw, serialized transactions included in the block.

#### 1. **Block Header**
The block header contains crucial metadata required for validation and chaining blocks:
- **Version** (4 bytes): Specifies the software version and any protocol upgrades.
- **Previous Block Hash** (32 bytes): Links the block to the hash of the preceding block, forming the blockchain.
- **Merkle Root** (32 bytes): Represents the root of a Merkle tree summarizing all transactions in the block, ensuring data integrity.
- **Timestamp** (4 bytes): The time the block was mined, as defined by the miner.
- **Difficulty Target (Bits)** (4 bytes): Encodes the target difficulty for the block.
- **Nonce** (4 bytes): A value adjusted during mining to produce a hash below the difficulty target.

#### 2. **[[Transaction Count]]**
A [[VarInt]] specifies how many transactions are included in the block. This dynamic field ensures efficiency regardless of the number of transactions.

#### 3. **Transactions**
The serialized transactions are included after the header and transaction count. Each transaction follows the [[Bitcoin Transaction Format]], and their sequence determines the order of execution within the block.

---

### Block Size and Propagation

#### 1. **Size Limits**
- [[BSV Blockchain]] allows for unbounded block sizes, enabling scalability by including millions of transactions in a single block.
- [[BTC]] enforces a 4 MB weight limit (with SegWit) as a soft cap.
- [[BCH]] permits blocks up to 32 MB.

Large blocks facilitate mass adoption and enterprise-grade applications, but they require advanced [[Propagation]] strategies.

#### 2. **Propagation**
Once mined, a block is propagated across the network using a peer-to-peer (P2P) protocol:
- Nodes validate the block before relaying it to peers.
- [[Propagation]] time depends on block size, network bandwidth, and node connectivity.
- [[Compact Blocks]] optimize propagation by transmitting only the block header and short transaction IDs, reducing redundant data transmission.

---

### Block Assembly and Mining

Blocks are assembled by [[Bitcoin Nodes]] (miners) through the following steps:
1. **Transaction Selection**: The miner collects unconfirmed transactions.
2. **Merkle Tree Construction**: Transactions are hashed into a binary tree, generating the Merkle root for inclusion in the block header.
3. **Block Header Creation**: The miner constructs the 80-byte header with metadata and prepares it for hashing.
4. **Proof of Work**: The miner repeatedly hashes the header with different nonce values until the resulting hash is below the difficulty target.
5. **Block Broadcasting**: Once mined, the block is broadcast to the network for validation.

---

### Validation of a Block

Nodes validate blocks before adding them to their local copy of the blockchain:
1. **Header Validation**:
   - Verify the hash of the block header meets the target difficulty.
   - Check the timestamp is reasonable (not too far in the future).
   - Ensure the previous block hash matches the latest known block.
2. **Transaction Validation**:
   - Verify all included transactions are valid and follow the [[UTXO Model]].
   - Ensure no double-spending occurs.
3. **Size and Structure**:
   - Confirm the block adheres to size and structure rules.
4. **Merkle Root**:
   - Validate the Merkle root matches the transactions in the block.

If the block passes all checks, it is appended to the node’s local blockchain and propagated to peers.

---

### Importance of Blocks

#### 1. **Security**
Blocks secure transactions through [[Proof of Work]], ensuring tamper resistance and immutability. Each block is cryptographically linked to the previous one, making unauthorized alterations computationally infeasible.

#### 2. **Batching**
By batching transactions, blocks reduce network overhead and provide a unified structure for propagating and validating transaction data.

#### 3. **Consensus**
Blocks enforce [[Consensus Rules]] by providing a record of accepted transactions and resolving conflicts such as competing chains.

---

### Advanced Features

- **[[Genesis Block]]**: The first block in the Bitcoin blockchain, hardcoded into all node implementations.
- **[[Orphan Blocks]]**: Blocks that are valid but excluded from the main chain due to competing forks.
- **[[Coinbase Transaction]]**: The first transaction in every block, rewarding miners with the block subsidy and transaction fees.

---

### Tags
#Bitcoin #Blockchain #BlockStructure #Consensus #ProofOfWork #Transactions #UTXO

---

### See Also
- [[Bitcoin Transactions]]
- [[UTXO Model]]
- [[Merkle Tree]]
- [[Consensus Rules]]
- [[Proof of Work]]
- [[Genesis Block]]
