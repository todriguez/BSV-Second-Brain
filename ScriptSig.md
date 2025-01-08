## Unlock Script (scriptSig)

### Overview

In the context of [[Bitcoin Script]] and the [[UTXO Model]], the **unlock script**, commonly referred to as `scriptSig`, is the part of a [[Bitcoin Transaction]] that provides the necessary data to satisfy the conditions set by a corresponding [[Lock Script (scriptPubKey)]]. It serves as the "key" required to unlock the value stored in a UTXO, enabling it to be spent in a new transaction.

---

### Characteristics of Unlock Scripts

1. **Purpose**:
   - The unlock script provides the inputs needed to make the conditions defined in the lock script evaluate to `true`.

2. **Not Always a Signature**:
   - While digital signatures are the most common data type included in an unlock script (as in [[Pay-to-PubKey-Hash (P2PKH)]] transactions), they are not mandatory. Other data types can also fulfill the lock script's requirements.
   - Examples of non-signature unlock data:
     - **Preimages** for hash-based conditions.
     - **Boolean values** for simple checks.
     - **Complex scripts** for multi-signature transactions or custom smart contracts.

3. **Execution in the Bitcoin Virtual Machine (BVM)**:
   - When a transaction is validated, the unlock script is concatenated with the corresponding lock script and executed in the [[Bitcoin Virtual Machine (BVM)]].
   - The transaction is valid if the combined scripts evaluate to `true`.

---

### Common Use Cases

1. **P2PKH Transactions**:
   - Unlock script contains:
     - A **digital signature** created with the private key.
     - The corresponding **public key** to prove ownership.

   Example:
   ```
   <signature> <public_key>
   ```
2. **Multi-Signature Transactions**:
    
    - Unlock script provides multiple signatures required to satisfy a multi-signature lock script (e.g., [[Pay-to-MultiSig (P2MS)]]).
    - Example:
  ```
<signature1> <signature2>
```
        
3. **Custom Smart Contracts**:
    
    - Unlock scripts can include data or scripts that fulfill specific predicates in advanced use cases.
4. **Hash-Based Locks**:
    
    - Provides a preimage to unlock UTXOs secured by hash-based conditions.
    - Example:
```
<preimage>
```

---
### Flexibility in Unlock Scripts

The `scriptSig` allows for a wide range of spending conditions, supporting:

- **Programmability**: Enables the creation of sophisticated [[Smart Contract]].
- **Adaptability**: Unlock scripts can adapt to various use cases, from simple payments to complex conditions.

---

### Tags

#BitcoinScript #UnlockScript #scriptSig #UTXO #BSV #Blockchain #DigitalSignatures #SmartContracts

---

### See Also

- [[Bitcoin Script]]
- [[Lock Script (scriptPubKey)]]
- [[UTXO Model]]
- [[Bitcoin Virtual Machine (BVM)]]
- [[Pay-to-PubKey-Hash (P2PKH)]]
- [[Pay-to-MultiSig (P2MS)]]
- [[Smart Contract]]

Copy code