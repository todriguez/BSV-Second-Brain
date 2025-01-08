# TXID (Transaction ID)

The **Transaction ID (TXID)** is a unique identifier for a [[Bitcoin Transactions|Bitcoin transaction]]. It plays a critical role in the [[Chain of Digital Signatures]], serving as the "fingerprint" for each transaction on the blockchain. The TXID is derived from the transaction's raw data and is integral to linking transactions together in a verifiable, cryptographic manner.

---

## How TXID is Generated

1. **Double SHA-256 Hash**:
   - The TXID is computed by applying the [[SHA-256]] hash function twice (double hashing) to the raw, serialized transaction data.
   - This ensures cryptographic integrity and mitigates vulnerabilities to certain types of attacks.

2. **Little-Endian Representation**:
   - The resulting hash is presented in **little-endian** byte order when displayed or stored in Bitcoin's system.
   - Little-endian format means the least significant byte appears first, which is the opposite of standard network byte order.

---

## Role of TXID in the Blockchain

### 1. **Leaf Node in the Merkle Tree**
- Each TXID represents a **leaf node** in the [[Merkle Tree]] of a block.
- Transactions are hashed and combined to form the [[Merkle Root]], anchoring all transactions immutably to a block.

### 2. **Linking Transactions**
- TXIDs are essential for referencing outputs of previous transactions:
  - A [[Transaction Input|transaction input]] uses the TXID and [[VOUT]] pointer to identify which output from a previous transaction is being committed as input.
  - This forms the cryptographic linkage in the [[Chain of Digital Signatures]].

### 3. **Verifiability**
- Each TXID is immutable and unique to its transaction:
  - If even a single byte in the transaction data changes, the TXID will change.
  - This ensures that the transaction data is tamper-proof and verifiable.

---

## Technical Representation

### Raw Data Example:
- Given raw transaction data:
```
0100000001abcdef...
```
- The TXID is calculated as:
$$TXID = SHA256(SHA256(raw\ data))$$

### Little-Endian Conversion:
- Hash (big-endian):  
`1a2b3c4d5e6f7g8h9i0j...`

- TXID (little-endian):  
`j0i9h8g7f6e5d4c3b2a1...`

---

## TXID in the Chain of Digital Signatures

1. **Ownership Validation**:
 - Each TXID acts as a pointer to a specific [[UTXO]] (Unspent Transaction Output) from a previous transaction.
 - This ensures that the referenced funds are valid and unspent.

2. **Integrity of Transactions**:
 - The TXID links new transactions to prior ones, forming an unbroken chain of cryptographic proofs.

3. **Network Efficiency**:
 - Nodes use TXIDs to quickly verify and organize transactions in [[Block]].

---
## Applications and Significance

1. **Transaction Reference**:
 - TXIDs are used in explorers, wallets, and systems to uniquely reference transactions.

2. **Auditability**:
 - They provide a transparent and cryptographically secure method to trace transaction history.

3. **Blockchain Integrity**:
 - TXIDs anchor the chain’s integrity by ensuring every transaction is linked and verifiable.

---

## Tags

#TXID #BitcoinTransactions #MerkleTree #DigitalSignatures #Blockchain #SHA256 #Cryptography #UTXO #BitcoinProtocol

---

## See Also

- [[Bitcoin Transactions]]
- [[VOUT]]
- [[Merkle Tree]]
- [[SHA-256]]
- [[UTXO Model]]
- [[Chain of Digital Signatures]]
- [[Block]]
