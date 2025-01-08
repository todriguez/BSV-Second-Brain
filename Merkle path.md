# merkle_path

The **Merkle Path** is a fundamental concept in cryptographic systems, particularly in blockchain protocols. With the introduction of the **BSV Unified Merkle Path (BUMP)**, BSV has standardized and optimized the structure and functionality of Merkle proofs. This article explores the Merkle Path and how the BUMP specification enhances its utility.

---

## What is a Merkle Path?

A **Merkle Path**, also referred to as a **Merkle Proof**, is a sequence of hashes that proves the inclusion of a specific data point (a *leaf node*) in a [[Merkle Tree]]. It enables verification of data integrity without requiring access to the entire dataset. This is achieved by providing the hashed pathway from the leaf node to the root of the Merkle Tree.

### Key Features:
- **Data Integrity**: A Merkle Path isolates and verifies data changes at the bit level.
- **Efficiency**: Minimal data is required for verification, reducing computational overhead.
- **Scalability**: Ideal for large datasets, as only a subset of the data is needed.

---

## How Does a Merkle Path Work?

1. **Start at the Leaf Node**: Each piece of data is hashed to form a leaf node.
2. **Pairing and Hashing**: The leaf node is paired with its sibling, and the pair is hashed together.
3. **Iterate**: This process repeats, combining hashes at each tree level until reaching the root hash.
4. **Provide Proof**: The Merkle Path is the sequence of hashes required to compute the root from the original data point.

### Example Use Case in BSV:
- Verifying the inclusion of a transaction in a block without downloading the entire block.

---

## BSV Unified Merkle Path (BUMP)

The **BSV Unified Merkle Path (BUMP)**, specified under [[BRC-74]], extends and consolidates prior Merkle proof formats, offering improvements in efficiency, compatibility, and scalability. 

### Key Features:
1. **Block Height Encoding**: Encodes the block height (1-9 bytes) for fast lookups.
2. **Compound Paths**: Allows multiple paths within a block to be represented in a single proof.
3. **Size Optimization**: Omits unnecessary data, reducing overall proof size.
4. **Binary and JSON Formats**: Supports both binary and JSON encoding for flexibility.

---

## How BUMP Works

### Binary Encoding:
Encodes the block height and tree height at the global level, followed by only the relevant hashes required for calculating the root hash.

| Field            | Description                                        | Size       |
|------------------|----------------------------------------------------|------------|
| **Block Height** | Block containing the transactions.                | 1-9 bytes  |
| **Tree Height**  | Height of the Merkle Tree (max: 64 levels).        | 1 byte     |
| **Number of Leaves** | Count of leaves at each level.                 | 1-9 bytes  |
| **Leaf Data**    | Contains offsets, flags, and hashes.               | Variable   |

### JSON Encoding:
Encodes paths in hierarchical arrays, starting at the lowest level. Each path specifies offsets, hashes, and flags to indicate txids or duplicates.

---

## Visualization of BUMP

A Merkle proof in BUMP format shows:
1. The **block height**.
2. The **leaf hashes** at each level of the tree.
3. The **flags** to indicate whether to duplicate or append hashes.


#### Example JSON:
```json
{
  "blockHeight": 813706,
  "path": [
    [
      { "offset": 3048, "hash": "304e737fdfcb017a..." },
      { "offset": 3049, "txid": true, "hash": "d888711d588021e5..." },
      { "offset": 3050, "txid": true, "hash": "98c9c5dd79a18f40..." },
      { "offset": 3051, "duplicate": true }
    ],
    [
      { "offset": 1524, "hash": "811ae75c80fecd27..." },
      { "offset": 1525, "hash": "82520a4501a06061..." }
    ]
  ]
}

```

## Calculating the Merkle Root

To verify a transaction’s inclusion:

1. Start with the transaction’s hash.
2. Iterate through the Merkle Path, hashing the working hash with sibling hashes.
3. Compare the final computed root with the block’s Merkle Root.

---

## Combining Multiple BUMP Proofs

Proofs from the same block can be combined to reduce redundancy:

1. Ensure the **blockHeight** and **root hash** match.
2. Merge paths, avoiding duplicate entries.
3. Maintain flags to distinguish relevant txids.

---

## Tags

#BSV #MerklePath #BUMP #TechnicalDocumentation



