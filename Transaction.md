## Overview

A **Bitcoin transaction** consists of a version number, a locktime value, a list of [[Input|inputs]] and a list of [[Outputs|outputs]]. Its primary functionality is to transfer custody of [[Bitcoin|bitcoin]] from one party to another. Beyond this, transactions serve as vehicles for [[Smart Contract|smart contracts]], data recording, attestation, and other secondary functionalities.

### Transaction Lifecycle

A transaction can be created and iterated inside a [[Payment Channel|Payment Channel]] using [[nLockTime]] and [[nSequence]] interlocks or sent directly to the [[Bitcoin Network|Bitcoin Network]] for inscription into a [[Block|block]]. Transactions use [[UTXO|unspent transaction outputs (UTXOs)]] as inputs and distribute their value to new outputs. UTXOs represent the 'coins' in which all bitcoin is stored.

### Transparency and Finality

Transactions are not encrypted, making it possible to view every transaction collected into a block. Once validated by a majority of miners on the network, they are considered settled. When included in a block, miners collaboratively agree on the order in which transactions were seen by the network.

Transactions are uniquely referenced using their [[TXID|TXID]], which is a double [[SHA-256|SHA-256]] hash of the fully serialized transaction.

## Transaction Components

### Inputs

An **input** references an output from a previous transaction. It specifies the source of the funds being spent in the new transaction. Each input includes:

- **Previous TXID:** The [[TXID|TXID]] of the referenced transaction.
- **Index:** Identifies the specific output being referenced.
- **ScriptSig:** The first half of a [[Script|Bitcoin script]] used to unlock the bitcoin held in the referenced output.

#### Input Format
| Field                     | Description                                      | Size                   |
| ------------------------- | ------------------------------------------------ | ---------------------- |
| Previous Transaction Hash | [[TXID]] of the transaction creating the output  | 32 bytes               |
| Previous Txout-Index      | Index of the output (non-negative integer)       | 4 bytes                |
| Txin-Script Length        | Length of the scriptSig                          | [[VarInt]] (1-9 bytes) |
| Txin-Script (ScriptSig)   | [[Script]] solving the output                    | Variable               |
| Sequence No               | Used for payment channels; final when 0xFFFFFFFF | 4 bytes                |


### Outputs

An **output** defines the destination of funds in a transaction. Each output specifies:

- **Value:** The number of [[Satoshis|satoshis]] transferred.
- **ScriptPubKey:** A [[Script|script]] that locks the value, defining how it can be unlocked by future transactions.

#### Output Format
| Field               | Description                                                  | Size                    |
| ------------------- | ------------------------------------------------------------ | ----------------------- |
| Value               | Non-negative integer representing the number of [[Satoshis]] | 8 bytes                 |
| Txout-Script Length | Length of the scriptPubKey                                   | [[VarInt]] (1-9 bytes ) |
| Txout-Script        | [[Script]] defining unlock conditions                        | Variable                |

### Scripts: Locking and Unlocking

- **ScriptPubKey (Locking Script):** Specifies conditions to release the bitcoin.
- **ScriptSig (Unlocking Script):** Provides a valid solution to the locking script, allowing the bitcoin to be spent.

### Transaction Validation

Bitcoin transactions use a [[Forth|Forth-like scripting language]] to verify inputs and outputs. The [[ScriptPubKey]] (locking script) is evaluated with the values left on the stack by the [[ScriptSig]] (unlocking script). If the script returns `true`, the input is authorized.

## Puzzle Types in Bitcoin

Bitcoin's scripting system allows for various types of financial transactions:

- **Pay to Public Key ([[P2PK]]):** Outputs are locked to a public key. The unlocking script provides a signature.
- **Pay to Public Key Hash ([[P2PKH]]):** Outputs are locked to a hash of a public key, requiring both the public key and a signature to unlock.
- **Pay to Script Hash ([[P2SH]]):** Outputs are locked to a hash of a script, enabling complex locking conditions.
- **Pay to Multi-Signature ([[P2MS]]):** Requires multiple parties to sign for the funds to be spent.

## Transaction Serialization

| Field           | Description                       | Size                               |
| --------------- | --------------------------------- | ---------------------------------- |
| Version No      | Currently set to 2                | 4 bytes                            |
| Input Counter   | Number of Inputs                  | [[VarInt]] indicating input count  |
| List of Inputs  | Variable                          | Variable                           |
| Output Counter  | Number of Outputs                 | [[VarInt]] indicating output count |
| List of Outputs | Variable                          | Variable                           |
| nLocktime       | Finalization time or block height | 4 bytes                            |

## Related Concepts
- [[Blockchain]]
- [[Block]]
- [[UTXO]]
- [[TXID]]
- [[Script]]
- [[nLockTime]]
- [[nSequence]]
- [[Payment Channel]]
- [[Transaction_Fees]]

#Tags: #Bitcoin #Transaction #Blockchain #TXID #UTXO #Script #SmartContracts #PaymentChannel #Mining
