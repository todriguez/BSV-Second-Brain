**Bitcoin Transactions** are the fundamental building blocks of the Bitcoin system, representing the primary network events that transfer value and data across the blockchain. Originally specified in the [[Bitcoin Whitepaper]] and early codebase by [[Satoshi Nakamoto]], Bitcoin transactions are structured to ensure traceability, transparency, and cryptographic security.

---

## Original Transaction Format

### 1. **Components of a Transaction**
Bitcoin transactions, as originally specified, consist of:
- **Inputs**: Reference outputs from previous transactions, providing the source of funds.
- **Outputs**: Specify the destination(s) for the funds, including:
  - The amount to be transferred (in [[Satoshis]]).
  - A lockScript ([[scriptPubKey]]) that defines the conditions for spending the funds.
- **Transaction Data**:
  - **Version**: Indicates the transaction's format and compatibility.
  - **Locktime**: Optional field for time-locked transactions.
  - **Signatures**: Generated using private keys generally serving as the unlockScript ([[scriptSig]]) for each input.

### 2. **Standardization and Predictability**
- The original transaction format provides a **fixed, standardized structure**, essential for building interoperable systems and applications.
- The [[UTXO]] model ensures that inputs can be cryptographically verified, creating an immutable chain of ownership.

---

## Bitcoin Transactions Across Implementations

### 1. **BSV: Faithful to the Original Protocol**
- [[BSV Blockchain]] most closely adheres to the original transaction format.
- **Difference**: 
  - The only significant deviation is the inclusion of the `FORKID` in the sighash flag for [[Replay Protection]], ensuring compatibility within environments that diverged during the blockchain splits.
- **Significance**:
  - By maintaining compatibility with the original format, BSV ensures:
    - Long-term stability for enterprise systems.
    - Interoperability with legacy Bitcoin-based software.

### 2. **BTC: Altered Transaction Structures**
- Bitcoin Core ([[BTC]]) has diverged significantly from the original specification by:
  - Adding Segregated Witness (SegWit), which removes signature data from the main transaction body, creating a separate witness structure.
  - Imposing restrictions like reduced block size and non-standard transaction types, which limit scalability and flexibility.
- These changes impact compatibility and deviate from Bitcoin’s original design as a peer-to-peer electronic cash system.

### 3. **BCH: Partial Adherence**
- Bitcoin Cash ([[BCH]]) attempts to restore some of the original protocol’s principles, such as larger blocks for scalability.
- However, BCH introduced its own variations in transaction formats, including different validation mechanisms and limitations compared to BSV.

---

## Importance of a Set-in-Stone Protocol

### 1. **Data Structure Stability**
- Protocols like Bitcoin are defined by their fixed set of data structures and formats.
- Predictability and stability in transaction formatting are essential for:
  - Long-term projects that involve significant investment.
  - Multi-year adoption timelines for enterprises.

### 2. **Centralization Risks of Protocol Changes**
- Arbitrary changes to protocols create centralization:
  - If a group can unilaterally alter fundamental structures, the system is effectively centralized to that group, regardless of the social consensus they claim to represent.
- A set-in-stone protocol ensures:
  - Miners enforce rules rather than create them.
  - Trustless systems remain trustless.

---

## Transaction Validation and Signature Types

### 1. **SIGHASH Flags and FORKID**
- The [[SIGHASH]] flags appended to transaction signatures define how a transaction's components are hashed during validation.
- **BSV Implementation**:
  - Includes the `FORKID` byte for replay protection without deviating significantly from the original design.
  - Ensures compatibility with other blockchain forks while preserving transaction integrity.

### 2. **Replay Protection**
- Replay protection prevents transactions on one chain (e.g., BCH) from being valid on another (e.g., BSV).
- This mechanism, achieved through the `FORKID`, maintains security in environments with multiple Bitcoin-derived blockchains.

---
# Bitcoin Transaction Datagram

| Field Name           | Description                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| **Version**          | A 4-byte field specifying the transaction format version.                                   |
| **Input Count**      | A variable-length integer indicating the number of inputs.                                  |
| **Inputs**           | A list of inputs, each consisting of:                                                      |
| - **TXID**           |   A 32-byte hash of the transaction containing the output being spent.                      |
| - **VOUT**           |   A 4-byte index identifying the output in the referenced transaction.                      |
| - **Unlock Script**  |   A script (scriptSig) that satisfies the conditions of the referenced output’s lock script.|
| - **Sequence**       |   A 4-byte field, usually `0xFFFFFFFF`, or used for time-locked transactions.               |
| **Output Count**     | A variable-length integer indicating the number of outputs.                                 |
| **Outputs**          | A list of outputs, each consisting of:                                                     |
| - **Value**          |   An 8-byte integer specifying the amount in satoshis.                                      |
| - **Lock Script**    |   A script (scriptPubKey) defining the conditions to spend the output.                      |
| **Locktime**         | A 4-byte field specifying the earliest time the transaction can be added to a block.        |

---

## Notes
1. **Variable-Length Fields**:
   - **Input Count** and **Output Count** are CompactSize integers, which can vary in length depending on the number of inputs or outputs.
   
2. **Scripts**:
   - Unlock scripts ([[scriptSig]]) are included in inputs.
   - Lock scripts ([[scriptPubKey]]) are included in outputs.

3. **Transaction ID (TXID)**:
   - A double SHA-256 hash of the serialized transaction (excluding the [[SIGHASH]] and witness data).

4. **Witness Data (SegWit-specific)**:
   - Present only in [[BTC]] transactions using Segregated Witness, not part of the original or BSV transaction format.

---
## Transaction Scripts: Puzzles and Solutions

Bitcoin’s [[Script Language]] is a stack-based programming language enabling a wide variety of transaction conditions. The **lock script** ([[scriptPubKey]]) in an output defines the "puzzle," while the **unlock script** ([[scriptSig]]) in an input provides the "solution." Some common script types include:

### 1. **Pay to Public Key (P2PK)**
- **ScriptPubKey**: `<pubKey> OP_CHECKSIG`
- **ScriptSig**: `<sig>`
- Validates that the provided signature was created using the private key corresponding to the public key.

**Example Execution Stack**:
- **Initial**: `<sig>` `<pubKey>` `OP_CHECKSIG`  
  _Combined scripts are placed on the stack._
- **Signature Verification**: `true`  
  _The signature is verified, and the transaction is valid._

---

### 2. **Pay to Public Key Hash (P2PKH)**
- **ScriptPubKey**: `OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG`
- **ScriptSig**: `<sig> <pubKey>`
- Requires the redeemer to provide both the public key and a valid signature. The public key hash in the scriptPubKey is verified against the provided public key.

**Example Execution Stack**:
- **Initial**: `<sig>` `<pubKey>`  
  _Combined scripts are placed on the stack._
- **Hash Verification**: `true`  
  _The public key hash matches; stack proceeds._
- **Signature Verification**: `true`  
  _The signature is verified, and the transaction is valid._

---

### 3. **Multisignature Transactions (P2MS)**
- **ScriptPubKey**: `<m> <pubKey1> <pubKey2> ... <pubKeyN> <n> OP_CHECKMULTISIG`
- **ScriptSig**: `<sig1> <sig2> ...`
- Requires `m` valid signatures from a group of `n` public keys to unlock the funds.

**Example Execution Stack**:
- **Initial**: `<sig1>` `<sig2>` `<3>` `<pubKey1>` `<pubKey2>` `<pubKey3>` `<5>` `OP_CHECKMULTISIG`  
  _Combined scripts are placed on the stack._
- **Multisignature Check**: `true`  
  _Enough valid signatures are provided, and the transaction is valid._

---

### 4. **Data Outputs**
- Outputs can have a value of zero and store data instead of transferring value.
- Commonly used in [[Application Layer Protocols]].
- **ScriptPubKey Example**: `OP_RETURN <data>`  
  _Encodes arbitrary data into the blockchain for use in protocols._

---

### Key Notes:
1. **Flexibility**: The [[Bitcoin Script]] language allows for complex financial instruments and custom transaction types.
2. **Determinism**: Each script type ensures clear, verifiable conditions for unlocking outputs.
3. **No Support for P2SH**: In [[BSV Blockchain]], the full scripting language is used natively, removing the need for P2SH encodings.

---

## See Also:
- [[Bitcoin Transactions]]
- [[UTXO Model]]
- [[Bitcoin Script]]
- [[Multisignature Transactions]]
- [[Application Layer Protocols]]
- [[Smart Contract]]
- [[SIGHASH]]
- [[Lock Script]]
- [[Unlock Script]]


## Tags

#Bitcoin #BSV #BitcoinTransactions #UTXO #SIGHASH #ReplayProtection #Blockchain #ProtocolStability #ImmutableLedger

---

## See Also

- [[Bitcoin]]
- [[Bitcoin Whitepaper]]
- [[UTXO Model]]
- [[SIGHASH]]
- [[Replay Protection]]
- [[Chain of Digital Signatures]]


