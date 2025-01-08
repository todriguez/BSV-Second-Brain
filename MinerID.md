# MinerId

**MinerId** is a protocol that allows a Miner to embed information in the [[Coinbase|coinbase transaction]] of each block they win. This process links blocks produced by a specific node to a pseudonymous identity, which the Miner may optionally associate with a real-world identity.

---

## Description

Currently, Bitcoin Miners can embed identity data on the Bitcoin ledger by inserting information into malleable input fields of the [[Coinbase|coinbase]] transaction in blocks they mine. However, this data can be trivially forged or spoofed.

The MinerId protocol solves this by *cryptographically* associating a block with a specific Miner’s pseudo-identity. A **MinerId** is simply an ECDSA public key from a keypair. This key signs the Miner’s [[Metadata|metadata]] placed in a [[False_Return|False Return]] output of the coinbase transaction within a block.

Using ECDSA signatures (instead of arbitrary unsigned data) provides non-repudiation, binding the Miner’s identity to mined blocks in a reliable way. While MinerId is a helpful infrastructure tool for the Bitcoin SV network, **it is not mandatory**. It’s a voluntary public key infrastructure that Miners can adopt to secure additional services and enhance trust around the ledger.

---

## Definitions

- **MinerId**  
  An ECDSA public key (based on [[Secp256k1|secp256k1]] parameters) used by the Miner to identify themselves.

- **VcTx (Validity Check Transaction)**  
  A transaction that determines the validity of the MinerId based on whether it remains unspent (valid) or spent (invalid/revoked). Using a VcTx allows a Miner to revoke a compromised MinerId key at any time, without needing to wait until they mine another block. By contrast, using the coinbase document alone would force the Miner to wait until they solve new [[Proof of Work|proof of work]] to revoke or update their MinerId.

- **Coinbase Document**  
  A structured data packet in the `OP_RETURN` (provably unspendable) output of the Miner’s [[Coinbase|coinbase transaction]]. All identity data for the Miner is stored here.

---

## Security

Ideally, the MinerId (and by extension, the coinbase transaction) should be specific to the block in which it appears. A direct one-to-one binding between the block and the MinerId signature prevents reuse of a Miner’s identity data in an unrelated block.  

However, making the MinerId entirely block-specific could introduce a chicken-and-egg dilemma: The block header cannot be finalized and signed by the MinerId key until the coinbase transaction is known, and vice versa.  

By including the block height in the coinbase document, replay attacks become as difficult as forking the chain (see [[Re-org|Re-org]]). This high cost disincentivizes maliciously reusing a valid MinerId in another block, such as an empty block that could harm the Miner’s reputation.

---

## Examples

**MinerId** has been supported by TAAL mining ltd. since December 20, 2019. See the following coinbase transactions:

- [TX 17a8b9994f1e89855b34660ea1d17061ae65833f1ded395c4c6a72d2d98832a6](https://whatsonchain.com/tx/17a8b9994f1e89855b34660ea1d17061ae65833f1ded395c4c6a72d2d98832a6)  
- [TX d898e7f3c198cefccf99e6ec982786f25af62aa86d6bc56c66a611660bf04942](https://whatsonchain.com/tx/d898e7f3c198cefccf99e6ec982786f25af62aa86d6bc56c66a611660bf04942)

---

## See Also

- [Medium.com blog post](https://medium.com/@jadwahab/6578046ac88)

---

## Tags
- #bsv  
- #bitcoin  
- #minerid  
- #security  
- #infrastructure  
- #proof-of-work  
