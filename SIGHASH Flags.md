# SIGHASH Flags

## Overview

**SIGHASH Flags** are used in Bitcoin transactions to define which parts of the transaction are signed and locked by the signature. They provide flexibility in transaction construction, enabling advanced use cases like [[Smart Contract]], payment channels, and atomic swaps. Each flag specifies the components of the transaction that must remain immutable while leaving other parts open to modification.

### SIGHASH Flags
- **SIGHASH_ALL**: Commits to all inputs and outputs, ensuring the entire transaction is immutable.
- **SIGHASH_NONE**: Commits to all inputs but allows outputs to remain mutable, useful for "blank check" scenarios.
- **SIGHASH_SINGLE**: Commits to a single output corresponding to the input being signed, leaving other outputs mutable.
- **SIGHASH_ANYONECANPAY**: Restricts the commitment to a single input, allowing others to add inputs and outputs.

---

## SIGHASH FORKID

The **FORKID** is an additional component introduced during the [[Bitcoin Cash (BCH)]] fork and subsequently adopted by [[BSV Blockchain]] to enhance security:
- It modifies the signature hash algorithm to prevent replay attacks across chains.
- The FORKID is added to the SIGHASH flag during hashing, creating a unique identifier for each chain.

**Example**:
- Without FORKID: `0x01` (SIGHASH_ALL)
- With FORKID: `0x41` (SIGHASH_ALL | FORKID)

---

## Signature Hash Calculation

### Steps
1. Serialize the transaction, excluding specific parts based on the SIGHASH flag.
2. Append the SIGHASH flag to the serialized data.
3. Perform a double [[SHA-256]] hash of the result.
4. Use the private key to sign the hash, producing the final signature.

### Zero Bytes Under Different Flags
- **SIGHASH_SINGLE**: If no corresponding output exists for the signed input, zero bytes are included in the hash to prevent misuse.
- **SIGHASH_NONE**: Outputs are excluded entirely from the hash, leaving them mutable.

---

## Functional Overview of SIGHASH Flags

| **Flag**                           | **Value (w/ FORKID)** | **Functionality**                                                        |
| ---------------------------------- | --------------------- | ------------------------------------------------------------------------ |
| **SIGHASH_ALL**                    | `0x41`                | Signs all inputs and outputs, making the transaction immutable.          |
| **SIGHASH_NONE**                   | `0x42`                | Signs all inputs but allows outputs to remain mutable.                   |
| **SIGHASH_SINGLE**                 | `0x43`                | Signs all inputs and the output corresponding to the input being signed. |
| **SIGHASH_ALL ANYONECANPAY**       | `0xC1`                | Signs its own input and all outputs.                                     |
| **SIGHASH_NONE<br>ANYONECANPAY**   | `0xC2`                | Signs its own input, leaving outputs mutable.                            |
| **SIGHASH_SINGLE<br>ANYONECANPAY** | `0xC3`                | Signs its own input and the output with the same index.                  |

---

## Use Cases

### 1. **Crowdfunding**
Using **SIGHASH_ALL | ANYONECANPAY**, multiple contributors can add their inputs to a transaction while preserving a fixed output structure.

### 2. **Blank Check**
Using **SIGHASH_NONE**, a transaction allows the recipient to define outputs, creating a flexible "blank check" mechanism.

### 3. **Partial Payments**
**SIGHASH_SINGLE** ensures an input corresponds to a specific output, enabling use cases like escrow or splitting payments.

### 4. **Collaborative Funding**
**SIGHASH_ANYONECANPAY** enables multiple parties to contribute inputs to a transaction without invalidating existing signatures.

---

## Limitations and Considerations

1. **SIGHASH_SINGLE Edge Case**:
   - If there is no corresponding output, the transaction may fail unless zero bytes are explicitly included.
2. **Replay Protection**:
   - Transactions without the FORKID may be replayed on other chains, exposing vulnerabilities.
3. **Complexity**:
   - Misuse of SIGHASH flags can introduce unintended mutability, leading to potential vulnerabilities.

---

## Benefits of SIGHASH Flags

1. **Flexibility**: Supports dynamic transaction structures for advanced use cases.
2. **Security**: Explicitly defines which parts of the transaction are mutable and immutable.
3. **Efficiency**: Reduces computational overhead by allowing partial validation where appropriate.
4. **Replay Protection**: Ensures chain-specific signatures with the FORKID.

---

## Examples of SIGHASH Functionality

### Standard Transaction
- **Flag**: SIGHASH_ALL
- Ensures the entire transaction, including inputs and outputs, is immutable.

### Modular Transactions
- **Flag**: SIGHASH_SINGLE | ANYONECANPAY
- Allows multiple modular transactions to be combined into a single larger transaction.

### Multi-Party Collaboration
- **Flag**: SIGHASH_ANYONECANPAY
- Enables multiple participants to sign only their inputs, allowing others to add theirs independently.

---

## Tags

#SIGHASH #BitcoinScript #DigitalSignatures #UTXO #Transactions #FORKID #Security #SmartContracts #PaymentChannels

---

## See Also

- [[Bitcoin Transactions]]
- [[Digital Signatures]]
- [[Bitcoin Script]]
- [[SHA-256]]
- [[Smart Contract]]
- [[Payment Channels]]
- [[FORKID]]
