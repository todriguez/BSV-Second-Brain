# Input

An **Input** in BSV represents the mechanism through which unspent transaction outputs ([[UTXO|UTXOs]]) are consumed to create new outputs in a [[Bitcoin_Transaction|transaction]]. Each input specifies a previously unspent output that it seeks to spend, proving ownership and satisfying the conditions defined by the locking script (commonly referred to as [[scriptPubKey|lockScript]]) in that UTXO.

## Structure of an Input

A transaction input consists of the following components:

### 1. **Outpoint**
   - The outpoint identifies the UTXO being spent. It includes:
     - **Transaction ID (TXID)**: A unique identifier of the transaction that created the UTXO.
     - **Output Index**: The position of the UTXO within the referenced transaction.

### 2. **Unlocking Script**
   - The unlocking script (also referred to as [[scriptSig|unlockScript]]) provides the data required to satisfy the locking script of the referenced UTXO. This can include:
     - **Digital Signatures**: Created using the private key corresponding to the public key in the locking script.
     - **Public Keys**: Required to verify the digital signature.
     - **Other Data**: Depending on the locking script, additional data might be included (e.g., in [[Pay_to_Script_Hash|P2SH]] transactions).

### 3. **Sequence Number**
   - The sequence number is used for transaction-level features, such as [[nSequence]]-based updates in [[Payment Channel|payment channels]]. 

## Validation of Inputs

For an input to be valid, it must satisfy the locking script of the referenced UTXO. This process involves the following steps:

1. **Retrieve the UTXO**:
   - Nodes retrieve the UTXO specified by the input's outpoint from the [[UTXO set|UTXO set]].

2. **Execute the Scripts**:
   - The unlocking script and locking script are concatenated and executed in the Bitcoin [[Script|script]] engine. If the execution results in a `true` value, the input is considered valid.

3. **Verify Ownership**:
   - The input must prove ownership by providing the correct private key-derived signature to satisfy the locking conditions.

## Use Cases of Inputs

Inputs enable various functionalities in BSV, including:

### 1. **Spending Funds**
   - Inputs allow users to spend their UTXOs by referencing them in new transactions.

### 2. **Multi-Signature Transactions**
   - In [[Multisig|multi-signature]] transactions, the input unlocking script provides multiple signatures to satisfy the conditions defined in the UTXO's locking script.

### 3. **Payment Channels**
   - Inputs are used in incrementally updated transactions to manage off-chain payments within [[Payment Channel|payment channels]].

### 4. **Advanced Scripts**
   - Complex scripts like [[Pay_to_R_Puzzle_Hash|P2R]] and [[Pay_to_False_Return|P2FR]] often rely on inputs to carry specific data for execution.

## Importance of Inputs in Bitcoin's Model

Inputs are fundamental to the [[UTXO|UTXO model]] employed by BSV. They ensure:

- **Immutability**: Inputs link back to specific UTXOs, creating a verifiable chain of custody.
- **Scalability**: By allowing SPV nodes to verify transactions using [[Merkle_Proof|Merkle proofs]], inputs reduce the need for full blockchain validation.
- **Flexibility**: Inputs enable [[Smart Contract|smart contract]] functionality by embedding data in unlocking scripts.

## Tags for Obsidian

- [[Input]]
- [[UTXO]]
- [[Bitcoin_Transaction]]
- [[scriptPubKey]]
- [[scriptSig]]
- [[Unlocking_Script]]
- [[Locking_Script]]
- [[nSequence]]
- [[Payment Channel]]
- [[Replace-by-Fee]]
- [[UTXO set]]
- [[Script]]
- [[Multisig]]
- [[Smart Contract]]
- [[Merkle_Proof]]


