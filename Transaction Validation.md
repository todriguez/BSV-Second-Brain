# Transaction Validation

## Overview

Transaction validation is the process of verifying that a [[Bitcoin Transactions|Bitcoin transaction]] adheres to the consensus rules of the [[BSV Blockchain]] blockchain. It ensures that transactions are consistent, lawful, and eligible for inclusion in a [[Block|block]]. This process is crucial for maintaining the integrity of the blockchain as a [[Chain of Digital Signatures]].

Transaction validation involves multiple steps, from structural verification to the evaluation of [[unlockScript|unlock scripts]] ([[scriptSig]]) against [[lockScript|lock scripts]] ([[scriptPubKey]]). This process is executed by the [[Bitcoin Virtual Machine (BVM)]], which evaluates the conditions (predicates) required to spend a [[UTXO|UTXO]].

---

## Steps in Transaction Validation

### 1. **Structural Verification**
Before execution, the transaction undergoes basic structural checks:
- **Format**: The transaction must conform to the [[Bitcoin Transactions|transaction format]].
- **Syntax**: Inputs, outputs, and metadata are checked for valid syntax.
- **Size**: The transaction must not exceed the maximum allowable size.

### 2. **Consensus Rule Verification**
The transaction is checked against [[Consensus Rules]]:
- **Double-Spend Prevention**: Ensures the [[UTXO|UTXOs]] being spent have not been previously spent.
- **UTXO Availability**: Confirms that the referenced outputs exist and are unspent.
- **Transaction Fees**: Validates that inputs cover outputs and include the required network fee.
- **Signature Validation**: If the [[unlockScript]] includes a signature, it is verified against the specified [[Public Key]].

### 3. **Script Evaluation**
The [[Bitcoin Virtual Machine (BVM)]] processes the [[lockScript]] and [[unlockScript]]:
- **Stack-Based Execution**: The BVM uses a [[Two-Stack Push Down Automaton]] to evaluate scripts.
- **Predicate Resolution**: The [[lockScript]] specifies a predicate (a condition to be met), while the [[unlockScript]] provides data to satisfy that condition.
- **Custom Unlocking Conditions**: [[unlockScript]] can include non-signature data, such as hashes, time locks, or custom values.

---

## The Predicate System

The Bitcoin transaction system operates on a **predicate model**:
- **Lock Script (scriptPubKey)**:
  - Defines the conditions under which the [[UTXO]] can be spent.
  - Examples include:
    - Signature verification.
    - Multi-signature checks.
    - Hash locks or time locks.

- **Unlock Script (scriptSig)**:
  - Supplies the data (witness) needed to satisfy the lock script.
  - Can include:
    - Digital signatures.
    - Pre-images for hash locks.
    - Arbitrary data depending on the locking conditions.

- **Evaluation**:
  - The BVM combines the [[unlockScript]] and [[lockScript]] on a single stack, evaluates the combined script, and checks if the final result is `TRUE`.

---

## Conditions Evaluated

### Common Conditions
1. **Signature Validation**:
   - Verifies that the [[Digital Signature]] matches the [[Public Key]] specified in the [[lockScript]].
   - Ensures the transaction is authorized by the rightful owner.

2. **Time Locks**:
   - Checks if a transaction meets [[nLocktime]] or [[nSequence]] requirements.

3. **Hash Locks**:
   - Verifies that a pre-image provided in the [[unlockScript]] matches the hash specified in the [[lockScript]].

4. **Custom Logic**:
   - User-defined [[Bitcoin Script]] conditions can be implemented, allowing flexible and programmable spending rules.

### Advanced Use Cases
1. **Non-Signature Unlocking**:
   - Unlock scripts may not require a signature.
   - Examples:
     - A hash pre-image for data verification.
     - Specific data for matching against a pattern in the lock script.

2. **Smart Contracts**:
   - Leveraging [[Bitcoin Script]] and high-level languages like [[sCrypt]], complex transaction conditions can be expressed and validated.

---

## Role of the Bitcoin Virtual Machine (BVM)

The [[Bitcoin Virtual Machine (BVM)]] is responsible for evaluating transaction scripts:
- **Execution Environment**:
  - A lightweight and deterministic virtual machine designed for stack-based computation.
- **Efficiency**:
  - The BVM processes transactions quickly and safely, avoiding vulnerabilities like infinite loops.
- **Stack Operations**:
  - Uses a primary and alternate stack for [[Two-Stack Push Down Automaton]] execution.

---

## How BSV Handles Validation

### 1. **Adherence to Original Design**
- [[BSV Blockchain]] restores all original opcodes and script capabilities, enabling rich transaction logic.
- Transactions follow the protocol's intended [[Set-in-Stone]] rules, ensuring reliability and backward compatibility.

### 2. **Replay Protection**
- Transactions include a [[SIGHASH]] flag with a FORKID byte to prevent replay attacks.

### 3. **Immutability with Flexibility**
- Even with immutability, mechanisms like [[Digital Asset Recovery (DAR)]] allow courts to reassign [[UTXO]] lawfully, recording all actions on-chain.

---

## Importance of Transaction Validation

1. **Security**:
   - Prevents unauthorized spending and double-spending attacks.
2. **Integrity**:
   - Ensures the blockchain remains an immutable and reliable record.
3. **Flexibility**:
   - The predicate system supports diverse use cases, from simple payments to complex smart contracts.

---

## Tags

#TransactionValidation #BitcoinScript #BVM #UTXO #DigitalSignatures #ConsensusRules #BSV #PredicateSystem #BlockchainSecurity

---

## See Also

- [[Bitcoin Transactions]]
- [[Bitcoin Virtual Machine (BVM)]]
- [[UTXO Model]]
- [[Lock Script]]
- [[Unlock Script]]
- [[Consensus Rules]]
- [[Digital Asset Recovery (DAR)]]
- [[Set-in-Stone]]
