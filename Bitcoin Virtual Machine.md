The **Bitcoin Virtual Machine (BVM)** is the execution environment for [[Bitcoin Script]] on the [[BSV Blockchain]] blockchain. It is a stack-based system designed to evaluate scripts embedded in transactions. Unlike traditional virtual machines, the BVM operates with deterministic, minimalistic principles, ensuring secure and efficient transaction validation.

---

## Overview

The BVM processes [[locking scripts]] (also known as `scriptPubKey`) and [[unlocking scripts]] (also known as `scriptSig`) associated with [[UTXO]]. It evaluates whether the unlocking script satisfies the conditions of the locking script, allowing the UTXO to be spent.

### Key Characteristics
1. **Stack-Based**: Operates using two stacks:
   - **Main Stack**: Stores operands and intermediate results.
   - **Alt Stack**: Provides auxiliary storage for temporary values.
2. **[[Deterministic]]**: Ensures that every valid script evaluates the same way across all nodes, maintaining consensus.
3. **Turing-Incomplete**: Lacks explicit looping constructs, avoiding infinite loops and enabling bounded execution. Loops can be unrolled across transactions using techniques like [[OP_PUSHTX]].

---

## Execution Flow

1. **Input Preparation**:
   - The unlockScript (`scriptSig`) is placed onto the stack.
   - The lockScript (`scriptPubKey`) is appended and executed.

2. **Stack-Based Execution**:
   - Operations are executed sequentially, manipulating the stack.
   - Operands are pushed onto the stack, and opcodes define operations to perform (e.g., addition, hashing).

3. **Validation**:
   - The script must evaluate to `true` to unlock the UTXO.
   - If the script fails or produces an invalid result, the transaction is deemed invalid.

---

## Full Opcode Set

In [[BSV Blockchain]], all Bitcoin Script opcodes are fully enabled, allowing for a wide range of functionality. Key categories of opcodes include:

### Arithmetic
- **Example**: [[OP_ADD]], [[OP_SUB]], [[OP_MUL]]
- **Purpose**: Perform basic arithmetic operations on stack values.

### Logical
- **Example**: [[OP_EQUAL]], [[OP_NOT]], [[OP_BOOLAND]]
- **Purpose**: Compare stack values or evaluate boolean conditions.

### Cryptographic
- **Example**: [[OP_SHA256]], [[OP_CHECKSIG]], [[OP_CHECKMULTISIG]]
- **Purpose**: Perform hashing and signature verification.

### Stack Management
- **Example**: [[OP_DUP]], [[OP_SWAP]], [[OP_DROP]]
- **Purpose**: Manipulate the order and content of the stack.

### Flow Control
- **Example**: [[OP_IF]], [[OP_ELSE]], [[OP_ENDIF]]
- **Purpose**: Enable conditional execution paths within a script.

### Data Handling
- **Example**: [[OP_PUSHDATA]], [[OP_CAT]], [[OP_SPLIT]]
- **Purpose**: Manage and manipulate data pushed onto the stack.

---

## Advanced Features in BSV

### 1. **Unbounded Scripting**
- The BVM supports larger scripts and data payloads, unlocking advanced use cases.
- Enhanced opcode limits allow for more complex and expressive smart contracts.

### 2. **Full Opcode Enablement**
- BSV restores previously disabled opcodes, including:
  - [[OP_CAT]] (concatenation of data).
  - [[OP_SPLIT]] (splitting data into parts).
  - [[OP_PUSHTX]] (enabling advanced transaction preimage handling).

### 3. **Extended Script Size and Stack Limits**
- Increased script size and stack depth allow for richer functionality and scalability.

---

## Advantages of the BVM

### 1. **Efficiency**
- Lightweight and deterministic, avoiding overhead common in account-based systems.
- Minimal resource usage ensures cost-effective transactions.

### 2. **Security**
- Lack of looping constructs prevents infinite execution.
- Deterministic execution eliminates ambiguity in transaction validation.

### 3. **Flexibility**
- Supports advanced smart contract use cases, such as:
  - [[Multi-Signature Transactions]]
  - [[Time-Locked Contracts]]
  - Iterative computation via [[OP_PUSHTX]]

---

## Practical Applications

1. **[[Micropayments]]**:
   - Enables efficient processing of high-frequency, low-value payments.

2. **[[Smart Contract]]**:
   - Complex business logic is implemented securely using advanced scripts.

3. **Tokenized Assets**:
   - Facilitates [[token]] issuance and management on the BSV ledger.

4. **Data Integrity**:
   - Use cryptographic functions to verify and store immutable data on-chain.

---

## Key Considerations

1. **Turing Incompleteness**:
   - While lacking native loops, unrolling loops across transactions using [[OP_PUSHTX]] enables iterative computations without risking infinite execution.

2. **Economic Constraints**:
   - Execution of complex scripts is limited by [[transaction fees]], aligning incentives with resource usage.

3. **Backward Compatibility**:
   - The BVM adheres to the original [[Bitcoin Whitepaper]] principles while enabling enhanced functionality.

---

## Tags

#BitcoinVirtualMachine #BVM #BitcoinScript #BSV #SmartContracts #UTXOModel #Cryptography #StackOperations #TransactionValidation #AdvancedOpcodes

---

## See Also

- [[Bitcoin Script]]
- [[UTXO Model]]
- [[OP_PUSHTX]]
- [[BSV Blockchain]]
- [[Smart Contract]]
- [[OP_CAT]]
- [[OP_CHECKSIG]]
- [[Bitcoin Whitepaper]]
