# [[Transaction Pre-Image]]

The **Transaction Pre-Image** is the serialized datagram of a [[Bitcoin Transaction]] used in the signature generation process. This datagram is hashed and signed to produce a [[Digital Signature]], ensuring the transaction's integrity and validity. The exact structure of the pre-image determines the data included in the signature, controlled by [[Sighash Flags]].

---

## Structure of the Transaction Pre-Image

The transaction pre-image consists of several serialized fields that capture the essence of a transaction. Each field plays a critical role in defining the transaction's state and behavior.

| **Field**       | **Name**         | **Description**                                                                                                                                             | **Length and Format**                     |
|------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| 1               | `nVersion`       | The version of the protocol defining this transaction.                                                                                                      | 4 bytes, little-endian integer            |
| 2               | `hashPrevouts`   | SHA256 hash of all concatenated input source details (TXIDs and vouts). If [[SIGHASH_ANYONECANPAY]] is used, this is a 32-byte null string.                  | 32 bytes, hash string                     |
| 3               | `hashSequence`   | SHA256 hash of all concatenated `nSequence` values. If [[SIGHASH_ANYONECANPAY]] is used, this is a 32-byte null string.                                      | 32 bytes, hash string                     |
| 4               | `outpoint`       | The outpoint for the input being signed, consisting of TXID (32 bytes) and vout (4 bytes).                                                                   | 36 bytes (32 + 4 bytes)                   |
| 5               | `scriptLen`      | The length of the locking script being validated.                                                                                                           | Variable-length integer (VarInt)          |
| 6               | `scriptPubKey`   | The locking script of the UTXO being spent.                                                                                                                 | Script length in bytes                    |
| 7               | `value`          | The value of the UTXO being spent, represented as satoshis.                                                                                                 | 8 bytes, little-endian integer            |
| 8               | `nSequence`      | The sequence value for the input being signed.                                                                                                              | 4 bytes, little-endian integer            |
| 9               | `hashOutputs`    | SHA256 hash of concatenated outputs (if [[SIGHASH_ALL]]), or only the output at the input's index (if [[SIGHASH_SINGLE]]), or a null string (if [[SIGHASH_NONE]]). | 32 bytes, hash string                     |
| 10              | `nLocktime`      | The `nLocktime` value of the transaction.                                                                                                                   | 4 bytes, little-endian integer            |
| 11              | `sighash`        | The [[Sighash Flags]] applied to the signature.                                                                                                             | 4 bytes                                   |

---

## Impact of [[Sighash Flags]] on the Pre-Image

Sighash flags modify the pre-image by zeroing out certain fields depending on the desired behavior:

- **SIGHASH_ALL**: Includes all fields and leaves nothing zeroed.  
- **SIGHASH_NONE**: Excludes all outputs by replacing them with 32 bytes of zeros in the pre-image.  
- **SIGHASH_SINGLE**: Only includes the output at the same index as the input being signed; other outputs are zeroed.  
- **SIGHASH_ANYONECANPAY**: Modifies the `hashPrevouts` and `hashSequence` fields, replacing them with 32 bytes of zeros.  

---

## Signature Generation and Validation

### Key Mathematical Elements

To generate a signature, the following elliptic curve cryptography (ECC) components are used:

- $P = S \cdot G$: Public key $P$ derived from private key $S$ via point multiplication with the generator point $G$.  
  - $S$: Private key, an integer in the range $[0, n)$, where $n$ is the curve order ($FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEBAAEDCE6AF48A03BBFD25E8CD0364141$).  
  - $G$: Generator point on the secp256k1 curve.  

### Signature Calculation

$$
s = k^{-1} \cdot (H(m) + S \cdot r) \mod n
$$

- $H(m)$: Double SHA256 hash of the transaction pre-image.  
- $r$: $x$-coordinate of $R = k \cdot G$.  
- $k$: Ephemeral key (randomly generated per signature).  

### Signature Format

The signature is represented in [[DER Format]], consisting of:

| **Field**         | **Length**       | **Description**                                                                                                                                                   |
|--------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sequence ID       | 1 byte           | `0x30`, indicating the start of the DER sequence.                                                                                                                 |
| Sequence Length   | 1 byte           | Total length of the signature sequence.                                                                                                                           |
| Integer ID (r)    | 1 byte           | `0x02`, indicating the start of the \( r \)-value.                                                                                                                |
| r Length          | 1 byte           | Length of the \( r \)-value (32 or 33 bytes).                                                                                                                     |
| r Value           | Variable         | \( r \)-value (big-endian integer, padded if negative).                                                                                                           |
| Integer ID (s)    | 1 byte           | `0x02`, indicating the start of the \( s \)-value.                                                                                                                |
| s Length          | 1 byte           | Length of the \( s \)-value (32 or 33 bytes).                                                                                                                     |
| s Value           | Variable         | \( s \)-value (big-endian integer, padded if negative).                                                                                                           |
| Sighash Flag      | 1 byte           | Sighash type (e.g., `0x41` for [[SIGHASH_ALL]]).                                                                                                                  |

---

## Advanced Applications

### OP_PUSH_TX and Recursive Functions
Using [[OP_PUSH_TX]], scripts can extract and reference specific fields from the transaction pre-image:
- Enforce conditions such as `value` or `nLocktime` from prior transactions.  
- Implement recursive logic in conjunction with an adjunct agent to prepare pre-images.  

### [[sCrypt]] and ScriptContext
In [[sCrypt]], the pre-image is represented as the **ScriptContext**, allowing fine-grained control over transaction validation and enabling advanced [[Smart Contract]].

---

## Tags

- [[Transaction Pre-Image]]  
- [[Bitcoin Transactions]]  
- [[Digital Signatures]]  
- [[Sighash Flags]]  
- [[OP_PUSH_TX]]  
- [[Elliptic Curve Cryptography]]  
- [[UTXO]]  
- [[Smart Contract]]  
