# Merkle Root

**Tags**: #Blockchain #MerkleRoot #Cryptography #BlockHeader #SPV #Immutability

The **Merkle Root** is a critical part of blockchain technology and derives from the structure of a [[Merkle Tree]]. In many blockchain protocols—particularly [[Bitcoin]]—the Merkle Root is included in the [[Block header]] and serves as a compact summary of all transactions within a block.

## Position in the Block Header

Inside a [[Block header]], the Merkle Root is stored alongside other fields like the [previous block hash](Previous Block Hash) and the [timestamp](Timestamp). Because the block header is hashed to produce a unique block identifier, any change to the Merkle Root (and thus the transactions) will produce a completely different block header hash, invalidating that block for the entire [[Blockchain]].

## Role in Immutability

By design, if any single transaction in a block is modified—even by a tiny amount—the Merkle Root changes, causing the corresponding [[Block header]] hash to change. This disrupts the [chain of headers](Chain of Headers), since each block header references the [[Hash function|hash]] of the previous block’s header. This “chaining” enforces [[Immutability]]: altering transactions in one block would require recalculating every subsequent block header, making tampering computationally impractical.

## Simplicity of SPV

[[Simplified Payment Verification]] (Simple Payment Verification) takes advantage of the Merkle Root without needing full transaction data. Light clients only need to download and validate the chain of [[Block header|block headers]], verifying that a specific transaction is included in a block by using the Merkle Tree structure. This approach drastically reduces the amount of data a user must store and verify while still maintaining strong security guarantees.

## Chain of Headers

Blocks link together via their headers, forming the [[Chain of Headers]]. Each block header contains the [Merkle Root](Merkle Root), [previous header hash](Previous Block Hash), [nonce](Nonce), and other relevant information. This linked structure ensures that the [[Blockchain]] remains resistant to tampering and censorship, as altering one block would necessitate recalculating all subsequent blocks’ headers.

For more on related concepts, see:
- [[Merkle Tree]]
- [[Blockchain]]
- [[Hash function]]
- [[Cryptography]]
- [[Block header]]
- [[Simplified Payment Verification]]
