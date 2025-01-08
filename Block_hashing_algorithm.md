
---
# Block Hashing Algorithm

The **block hashing algorithm** is a core component of the [[BSV Blockchain]] protocol, ensuring the integrity and security of the blockchain. The hashing process involves double hashing the block header using [[SHA-256]] and adhering to strict difficulty targets as specified by the `nBits` field in the header.

---

## Block Header Overview

The [[block header]] is always **80 [[bytes]]** in size and contains the essential [[metadata]] for the block. This metadata is used as the input to the hashing algorithm, producing a unique identifier for the block (the block hash).

### Block Header Datagram

| Field                 | Description                                                                             | Size     |
| --------------------- | --------------------------------------------------------------------------------------- | -------- |
| **Version**           | Protocol version number indicating rule set for block validation.                       | 4 bytes  |
| **[[PrevBlockHash]]** | [[Hash]] of the previous block in the chain (links blocks together).                    | 32 bytes |
| **MerkleRoot**        | Hash of the root of the Merkle tree containing all transactions in the block.           | 32 bytes |
| **Timestamp**         | Approximate creation time of the block (UNIX timestamp).                                | 4 bytes  |
| **[[nBits]]**         | Encodes the network difficulty target as an exponent and mantissa.                      | 4 bytes  |
| **[[Nonce]]**         | A counter that miners iterate to find a valid block hash meeting the difficulty target. | 4 bytes  |

---

## Double Hashing with [[SHA-256]]

The hashing algorithm uses a **double SHA256 hash**:
1. The block header is serialized and hashed once using SHA256.
2. The output is hashed again with SHA256 to produce the final hash.  
   This double hashing process enhances security against collision attacks.

The final hash output is represented in **Little Endian** format and is used to verify that the block meets the difficulty requirements specified by `nBits`.

---

## Difficulty and `nBits`

The `nBits` field encodes the difficulty target using an **exponent** and **mantissa** in compact form:
- **Mantissa**: Encodes the significant digits of the target.
- **Exponent**: Determines the position of the decimal point, effectively scaling the target.

The difficulty target specifies how many leading zero bits must be present in the resulting hash. For example:
- A low target indicates more leading zeros, making it harder to mine a block.
- A high target makes it easier, adjusting to the network's total hashing power.

---

### Understanding the Number Space

The **output space** of SHA256 spans from:
- **0x000...0** (32 bytes of zeros) to 
- **0xFFF...F** (~\(1.17 \times 10^{77}\)).  

This space is uniformly distributed, meaning most hash outputs statistically fall around the midpoint. The goal of mining is to produce a hash output lower than the difficulty target encoded by `nBits`.

---

### Example: Network Hash Rate and Difficulty

If the network has a **1 Exahash/second** hash rate (1 quintillion hashes per second), with a block interval of 600 seconds (10 minutes):
- Approximately $600 \times 10^{18}$ (600 quintillion) hash attempts are made.
- The target encoded in `nBits` is adjusted to ensure only 1 out of 600 quintillion hashes falls below the target, maintaining a 10-minute block interval.

This adjustment ensures that the difficulty target dynamically aligns with the network's hash rate.

---

## Transactions and Merkle Root

The hashing process for the block header is independent of the number of transactions. The transactions are summarized in the **[[Merkle Root]]**, which is:
1. Constructed by hashing pairs of transaction hashes in a tree structure.
2. Represented as a single 32-byte hash in the block header.

---

## Links Between Blocks

The **PrevBlockHash** field in the block header links the current block to the previous block, forming a continuous, immutable chain of blocks:
- Each block’s hash includes the hash of the previous block.
- This chaining ensures tamper resistance, as altering one block requires recalculating all subsequent block hashes.

---

## Tags
- [[Block Hashing]]
- [[SHA-256]]
- [[Double Hashing]]
- [[Difficulty]]
- [[Block Header]]
- [[nBits]]
- [[Merkle Root]]
- [[Little Endian]]
- [[Mining]]
- [[Blockchain Security]]

---

By design, the block hashing algorithm is efficient, secure, and scales with the network's growth. It ensures that the computational effort required for mining aligns with the economic incentives and security requirements of the BSV blockchain.
