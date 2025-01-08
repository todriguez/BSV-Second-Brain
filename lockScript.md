## Lock Script (scriptPubKey)

### Overview

The **lock script**, commonly referred to as `scriptPubKey`, is a key component of the [[Bitcoin Script]] system within the [[UTXO Model]]. It defines the conditions under which a specific [[UTXO]] (Unspent Transaction Output) can be spent. The lock script acts as a "lock" on the value stored in the UTXO, ensuring it can only be spent by providing the correct "key" through a corresponding [[Unlock Script (scriptSig)]].

---

### Characteristics of Lock Scripts

1. **Purpose**:
   - Establishes the conditions that must be satisfied to unlock the UTXO.
   - Enforces security and ownership by specifying spending requirements.

2. **Programmatic Nature**:
   - The lock script is a small program written in [[Bitcoin Script]], executed by the [[Bitcoin Virtual Machine (BVM)]] during transaction validation.

3. **Flexibility**:
   - Lock scripts can define simple or complex conditions, enabling diverse use cases ranging from basic payments to advanced [[Smart Contract]].

---

### Common Types of Lock Scripts

1. **Pay-to-PubKey-Hash (P2PKH)**:
   - The most common lock script type.
   - Locks the UTXO to a specific Bitcoin address, requiring the spender to provide a valid public key and digital signature.
   - Example:
     ```asm
     OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
     ```

2. **Pay-to-Script-Hash (P2SH)**:
   - Allows more complex scripts to be used while simplifying transaction outputs.
   - Locks the UTXO to a hash of a script, requiring the spender to provide the full script and data to satisfy it.
   - Example:
     ```asm
     OP_HASH160 <scriptHash> OP_EQUAL
     ```

3. **Pay-to-MultiSig (P2MS)**:
   - Requires multiple signatures to unlock the UTXO.
   - Example:
     ```asm
     <m> <pubKey1> <pubKey2> ... <pubKeyN> <n> OP_CHECKMULTISIG
     ```

4. **Custom Scripts**:
   - Enables advanced conditions like time locks, hash locks, or other programmable predicates.

---

### Execution in the Bitcoin Virtual Machine (BVM)

1. **Concatenation**:
   - During transaction validation, the `scriptSig` (unlock script) is concatenated with the `scriptPubKey` (lock script) to form a complete program.

2. **Evaluation**:
   - The BVM executes the combined script.
   - The transaction is valid if the script evaluates to `true`.

3. **Predicate System**:
   - Lock scripts define a predicate (a condition to be satisfied) that the unlock script must resolve.

---

### Advanced Features

1. **Programmability**:
   - Lock scripts can encode complex conditions, enabling use cases like [[Micropayments]], [[Escrow Services]], and multi-party agreements.

2. **Security**:
   - Provides robust mechanisms to prevent unauthorized spending of UTXOs.

3. **Transparency**:
   - Lock scripts are included in transaction outputs, ensuring they are visible and verifiable by all network participants.

---

### Comparison to Unlock Script

| Feature               | Lock Script (scriptPubKey)                | Unlock Script (scriptSig)                |
|-----------------------|------------------------------------------|------------------------------------------|
| **Purpose**           | Defines conditions for spending UTXOs.  | Provides data to satisfy the lock script.|
| **Location**          | Included in transaction outputs.         | Included in transaction inputs.          |
| **Data Type**         | Encodes predicates.                      | Encodes solutions to predicates.         |

---

### Tags

#BitcoinScript #LockScript #scriptPubKey #UTXO #BSV #Blockchain #DigitalSignatures #SmartContracts

---

### See Also

- [[Bitcoin Script]]
- [[Unlock Script (scriptSig)]]
- [[UTXO Model]]
- [[Bitcoin Virtual Machine (BVM)]]
- [[Pay-to-PubKey-Hash (P2PKH)]]
- [[Pay-to-Script-Hash (P2SH)]]
- [[Smart Contract]]
