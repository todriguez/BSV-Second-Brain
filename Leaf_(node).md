# Leaf Nodes in a Merkle Tree

In the context of a [[Merkle Tree]] (or binary hash tree), **leaf nodes** represent the cryptographic hashes of raw transaction data, often referred to as [[TXID]]s. Each transaction in a data set corresponds to one leaf node, ensuring a one-to-one relationship between the data set and the leaf nodes at the base of the tree.

## Characteristics of Leaf Nodes in a Merkle Tree

1. **Hashes of Raw Data**:  
   Each leaf node contains the [[SHA-256]] double-hashed value of the raw transaction data (TXID), providing a unique fingerprint for each transaction.

2. **Correspondence to Data Set**:  
   The number of leaf nodes equals the size of the data set, with each transaction producing one leaf node.

3. **Foundation of the Merkle Tree**:  
   Leaf nodes serve as the starting layer for constructing the Merkle tree. These hashes are iteratively paired and hashed to form internal nodes, culminating in the [[Merkle Root]].

4. **Base for Merkle Path Authentication**:  
   Leaf nodes are integral to [[Merkle Path]] authentication, which validates the inclusion of specific transactions in the tree.

## Layers in a Merkle Tree

For a data set of \(n\) transactions, the Merkle tree will have \(\lceil \log_2 n \rceil\) layers, where each layer represents successive levels of hashing:
- The **leaf layer** contains \(n\) leaf nodes, each corresponding to a transaction.
- Higher layers progressively reduce the number of nodes by hashing pairs until the [[Root Node|Merkle Root]] is reached.

If the number of transactions (\(n\)) is not a power of two, the tree is padded by duplicating the last node to ensure all layers have an even number of nodes.

## Merkle Path and Merkle Path Authentication

### Definition of Merkle Path
A **Merkle Path** is the set of sibling hashes required to prove that a particular leaf node is included in the Merkle tree. Each hash in the path is used to reconstruct the tree from the leaf node to the root.

### Authentication Process
Merkle path authentication enables efficient validation of a specific transaction without needing access to the entire data set:
1. **Start with the Leaf Node**:  
   The leaf node representing the transaction (TXID) is the starting point.
   
2. **Combine with Sibling Hashes**:  
   The sibling hashes from the Merkle path are combined with the leaf node's hash and hashed together at each layer.

3. **Reconstruct the Root**:  
   The process continues layer by layer until the root hash is reconstructed.

4. **Validation Against the Root**:  
   If the reconstructed root matches the known [[Merkle Root]], the transaction is confirmed as part of the data set.

### Efficiency of Merkle Path
The Merkle path authentication process is highly efficient, requiring only $$\lceil \log_2 n \rceil$$hashes for verification. This logarithmic complexity makes Merkle trees ideal for systems like [[Simplified Payment Verification]] in [[BSV Blockchain|BSV]].

## Applications in BSV

In the [[BSV Blockchain]] blockchain:
- Each block contains a Merkle tree of transaction hashes (TXIDs) to summarize all included transactions.
- Leaf nodes represent the double SHA-256 hashes of raw transaction data.
- The Merkle Root is stored in the [[Block Header]], providing a cryptographic summary of the block's transactions.
- [[Simplified Payment Verification]] relies on Merkle path authentication to verify transactions efficiently without requiring full blockchain data.

## Tags

- [[Merkle Tree]]
- [[Merkle Path]]
- [[SHA-256]]
- [[BSV Blockchain]]
- [[TXID]]
- [[Block Header]]
- [[Simplified Payment Verification]]
- [[Blockchain Security]]

Leaf nodes are the foundation of a Merkle tree, directly representing the raw transaction data in cryptographic form. They enable scalable and efficient data verification, making them a cornerstone of secure and efficient blockchain technology like Bitcoin SV.
