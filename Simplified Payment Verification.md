# Simplified Payment Verification (SPV)

[[Simplified Payment Verification]] is a method by which a user can verify if a particular [[transaction]] is included in a [[block]] without downloading the entire [[blockchain]].

---

## Overview

[[Simplified Payment Verification]] was introduced in the [[Bitcoin Whitepaper]] by [[Satoshi Nakamoto]]. It allows [[wallets]] to verify transactions without needing to secure the entire network. This method strikes a balance between authentication and efficiency, making it suitable for mobile devices or systems with limited storage.

---

## Working of SPV

An [[SPV client]] downloads only the [[Block header]] of the blockchain—significantly smaller than the full ledger. Upon startup, the SPV client sends a list of its [[transaction outputs]] or [[UTXO]] to a [[node]] in the [[BSV Network]] to discover where these transactions are included. The node responds with a list of blocks and a [[Merkle Path]] that cryptographically proves the transaction’s inclusion in a given block.

---

## Merkle Tree and SPV

A [[Merkle Tree]] is the data structure that underpins SPV, allowing transaction hashes to be arranged in a tree form. Each leaf node is a hash of a single transaction. The topmost node, or [[Merkle Root]], summarizes all transaction hashes, enabling an SPV client to verify if a specific transaction is included in a block.

---

## SPV in Peer-to-Peer Payments

**SPV** is crucial for true [[Peer-to-Peer]] exchange. It allows two users to transact directly, facilitating decentralized, privacy-preserving systems. Although called “payment,” all blockchain transactions effectively transfer ownership of at least one [[satoshi]] (or other denominations) from one [[UTXO]] to another.

---

## Example Scenario: Alice Pays Bob

1. **Alice orders coffee** at Bob’s shop.  
2. **Bob provides an invoice** with a [[transaction template]] that includes at least one output to receive payment.  
3. **Alice completes** the transaction template by adding one or more of her [[UTXO]]s in the input, covering Bob’s requested amount.  
4. **Alice returns** the filled transaction to Bob with corresponding [[Merkle Paths]] for those UTXOs (potentially using [[BEEF]] under [[BRC 62]]).  
5. **Bob validates** the transaction against his local chain of [[Block header]]. If valid, he can accept it immediately (0-conf).  
6. **Bob submits** the transaction to an [[Overlay Service]] for [[timestamping]] (and any other checks).  
7. **The Overlay Service** performs similar validation, updates its internal state, and submits the transaction to the [[core node network]].  
8. **Nodes validate** the transaction. If accepted, they add it to a [[Block Template]].  
9. **Bob receives confirmation** once the transaction is accepted and can later retrieve a Merkle Path for the transaction after it’s mined.

Thanks to the [[First-Seen Rule]], any attempt to double-spend the same UTXO later will be rejected by the network.

---

## Infrastructure Requirements

From Bob’s standpoint (and the [[Overlay Service]]), the following are essential:

1. **Block Headers**: ~80 bytes per block → ~4.2 MB/year for ~52,416 blocks/year.  
2. **Transaction Data**: ~400 bytes for a basic [[Pay-to-PubKeyHash (P2PKH)]] transaction, assuming the input’s TX is already mined.  
3. **Merkle Paths**: ~1 KB per path (depending on transaction volume per block).

[[Simplified Payment Verification]] solutions maintain only the necessary subset of the blockchain, linked via [[Block header]] and relevant transactions.

---

## Instant Payments

[[Simplified Payment Verification]] supports **instant payments** ([[0-conf]]) in many situations:

- **Bob checks** the transaction locally via SPV and can trust it for low-value purchases.  
- **For extra security**, Bob may query a node to ensure no conflicting (double-spend) transaction exists.

### Why Bob Can Trust Instant Transactions

Bob receives:
1. **Transaction data**  
2. **Merkle proofs** of the referenced transactions  
3. **Valid digital signatures**  

This combination generally assures Bob of the payment’s legitimacy, akin to signing a receipt in credit card payments. For added confidence, Bob can verify with a [[Node]] to confirm no conflicts.

---

## Locking Scripts and Integrity Checks

SPV’s security also hinges on correct [[lockScript]] and [[unlocking script]] usage:

- **Locking Script**: Details the conditions to spend the UTXO (e.g., `OP_DUP OP_HASH160 <Public Key Hash> OP_EQUALVERIFY OP_CHECKSIG`).  
- **Unlocking Script**: Must fulfill the locking script’s requirements via a valid [[signature]] and [[public key]].

If the locking script doesn’t properly link to a particular user, anyone might spend the UTXO. Script integrity is therefore vital.

---

References: [nChain Article on SPV](https://medium.com/nchain/simplified-payment-verification-48ac60f1b26c)

---

## Tags
- #spv
- #bitcoin
- #p2p
- #blockchain
- #light-clients
- #transactions
- #payment
- #merkle-tree
- #script-validation
- #instant-payments








