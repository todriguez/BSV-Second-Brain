## SIGHASH: Signature Hash Types in Bitcoin Transactions

**SIGHASH** refers to the signature hash types used in [[Bitcoin]] transactions to define how a digital signature commits to specific parts of the transaction. These flags enable [[flexibility]] in transaction construction by allowing certain components to be mutable while locking others in place.

SIGHASH plays a critical role in transaction validation, ensuring the [[cryptographic integrity]] of signed data while supporting advanced use cases like [[micropayments]], [[payment channels]], and [[smart contracts]].

---

### Overview of SIGHASH

Each signature in a Bitcoin transaction is appended with a **SIGHASH flag**, determining how the [[Transaction ID (TXID)|transaction hash]] is calculated for validation. The hash is then signed using the [[ECDSA]] private key, and this signature ensures transaction authenticity.

SIGHASH types fall into two main categories:
1. **Base Flags**: Define which parts of the transaction are hashed.
2. **Modifier Flags**: Adjust the behavior of the base flags, e.g., restricting commitment to specific inputs or outputs.

---

### Base SIGHASH Flags

| **Flag**            | **Description**                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------|
| **SIGHASH_ALL**     | Default type. Commits to all inputs and outputs, ensuring the entire transaction is immutable.                    |
| **SIGHASH_NONE**    | Commits to all inputs but excludes outputs, allowing them to remain mutable. Useful for "blank checks."           |
| **SIGHASH_SINGLE**  | Commits to a single input and the corresponding output, leaving other outputs mutable. Ideal for partial payments. |

---

### Modifier Flags

| **Modifier**             | **Description**                                                                                             |
|--------------------------|-------------------------------------------------------------------------------------------------------------|
| **SIGHASH_ANYONECANPAY** | Restricts the signature to the signed input only, enabling other parties to add inputs and outputs.          |

Modifier flags can be combined with base flags using bitwise operations. For example:
- **SIGHASH_SINGLE | SIGHASH_ANYONECANPAY**: Signs a single input and the corresponding output, allowing other inputs and outputs to be mutable.

---

### SIGHASH and Transaction Validation

The SIGHASH flag determines how the transaction's [[double SHA-256|double-hashed]] message is constructed for validation. Steps include:
1. **Transaction Serialization**:
   - Components like inputs, outputs, and metadata are serialized.
   - Specific fields are omitted or altered based on the SIGHASH type.
2. **Hash Calculation**:
   - A double SHA-256 hash of the serialized data is computed.
3. **Signature Verification**:
   - The hash is validated against the signature using the provided public key.

---

### Use Cases for SIGHASH Types

#### 1. **SIGHASH_ALL**
- **Use Case**: Standard payments where all transaction details are immutable.
- **Benefit**: Ensures the transaction cannot be altered after signing.

#### 2. **SIGHASH_NONE**
- **Use Case**: Creating "blank checks" where outputs can be added later.
- **Benefit**: Enables flexibility in output definition.

#### 3. **SIGHASH_SINGLE**
- **Use Case**: Splitting payments or managing escrow agreements.
- **Benefit**: Commits to a specific input-output pair, leaving others mutable.

#### 4. **SIGHASH_ANYONECANPAY**
- **Use Case**: Collaborative funding or payment channels.
- **Benefit**: Allows additional parties to contribute inputs.

---

### SIGHASH and Replay Protection

In the [[BSV Blockchain]] network, the **FORKID** is included in the SIGHASH flag to prevent replay attacks across different blockchain forks. This ensures that signatures are unique to the BSV chain.

The FORKID modifies the hashing algorithm by appending an additional byte to the SIGHASH value. This change prevents transactions valid on one chain (e.g., BCH) from being valid on another (e.g., BSV).

---

### Importance of SIGHASH in BSV

1. **Flexibility**:
   - SIGHASH flags support complex transaction structures, such as [[atomic swaps]], [[payment channels]], and advanced [[smart contracts]].

2. **Security**:
   - By precisely defining which parts of a transaction are signed, SIGHASH reduces the risk of unintended mutability or malicious modification.

3. **Scalability**:
   - SIGHASH types enable efficient transaction aggregation in high-throughput systems like the BSV network.

4. **Interoperability**:
   - Adherence to original [[Bitcoin protocol]] rules ensures compatibility with legacy systems while supporting modern applications.

---

### Example: Using SIGHASH_SINGLE

Consider a payment scenario where a transaction has three inputs and three outputs. Using **SIGHASH_SINGLE**, the signature for each input commits only to the corresponding output:
- **Input 0** → **Output 0**
- **Input 1** → **Output 1**
- **Input 2** → **Output 2**

This configuration is useful for splitting payments or handling escrow, where specific inputs are tied to predefined outputs.

---

### Limitations and Considerations

1. **Edge Cases**:
   - With **SIGHASH_SINGLE**, if the corresponding output does not exist, the transaction becomes invalid unless special handling (e.g., zero bytes) is implemented.

2. **Complexity**:
   - Improper use of SIGHASH flags can lead to transaction malleability or unintended consequences.

3. **Compatibility**:
   - Variations in SIGHASH implementations across forks (e.g., BTC, BCH) may impact cross-chain compatibility.

---

### Conclusion

SIGHASH is a cornerstone of Bitcoin’s [[UTXO Model]], enabling secure, flexible, and scalable transaction validation. By allowing developers to fine-tune transaction behavior, SIGHASH flags empower advanced use cases while preserving the integrity of the blockchain. The BSV network’s commitment to the original Bitcoin protocol ensures robust support for SIGHASH functionality, making it ideal for enterprise-grade applications.

---

### Tags

#Bitcoin #BSV #SIGHASH #Transactions #SignatureValidation #UTXO #ReplayProtection #Blockchain #SmartContracts #Micropayments

---

### See Also

- [[Bitcoin Transactions]]
- [[SIGHASH Flags]]
- [[UTXO Model]]
- [[Replay Protection]]
- [[Double SHA-256]]
