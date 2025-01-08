# R-Puzzles

An **R-Puzzle** is a novel type of script in Bitcoin Script that allows for the spending of a [[UTXO]] using any valid Bitcoin keypair. This can be applied to sign [[Metanet]] node addresses, addresses holding tokens, or even randomly generated keypairs.

---

## Key Components of R-Puzzles

### **k**
In an R-Puzzle, the spending party uses a proof of knowledge of a value **k**. This value:
- Is from the same mathematical set as Bitcoin [[Private Keys]].
- Must be known to the spender.
- Is used to generate **r**, which is the x-coordinate of **k** multiplied by the [[Generator Point|G]]. 

The process involves:
1. Extracting **r** from the [[ECDSA]] signature in the transaction.
2. Comparing **r** against a hash stored in the [[scriptPubKey]].

**k**-chains can be managed using deterministic techniques similar to Bitcoin keychains.

---

## Generating an ECDSA Signature

To generate an [[ECDSA]] signature, the following inputs and steps are used:

### Inputs
1. **k**: A randomly selected value.
2. **Keypair**: Public key **P1 = S1 \cdot G**, where **S1** is the private key.
3. **Message m**: The hash of the transaction or data being signed.

### Method
1. Calculate:
   $$
   R = k \cdot G
   $$
2. Extract:
   $$
   r = \text{x-coordinate of } R
   $$
3. Compute:
   $$
   s = k^{-1} \cdot (H(m) + S_1 \cdot r) \mod n
   $$

The resulting signature is:
$$
\langle r, s \rangle
$$
plus 5 bytes of formatting and a [[SIGHASH]] type.

---

## Signature Structure

| **Data Structure**             | **Length** | **Data (hex)**                                                                                               |
|---------------------------------|------------|-------------------------------------------------------------------------------------------------------------|
| Sequence Identifier             | 1 byte     | `30`                                                                                                        |
| Length of Sequence              | 1 byte     | `46`                                                                                                        |
| Integer Identifier              | 1 byte     | `02`                                                                                                        |
| Byte-length of r                | 1 byte     | `21`                                                                                                        |
| Needed if \( \text{left}(r, 1) > 7f \) | 1 byte     | `00` (optional)                                                                                            |
| r                               | 32 bytes   | Example: `e9d34347e597e8b335745c6f8353580f4cbdb4bcde2794ef7aab915d996642`                                   |
| Integer Identifier              | 1 byte     | `02`                                                                                                        |
| Byte-length of s                | 1 byte     | `21`                                                                                                        |
| Needed if \( \text{left}(s, 1) > 7f \) | 1 byte     | `00` (optional)                                                                                            |
| s                               | 32 bytes   | Example: `df2ccb52c7243c55bde34934bd55efbdac21c74a20bb7b438d1b6de3311f`                                     |
| Sighash Type                    | 1 byte     | `01`                                                                                                        |

**Serialized Example**:
```
3046022100e9d34347e597e8b335745c6f8353580f4cbdb4bcde2794ef7aab915d996642022100df2ccb52c7243c55bde34934bd55efbdac21c74a20bb7b438d1b6de3311f01
```


---

## Extracting **r**

The following script extracts **r** from the signature:

### Script
```
OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP
```


### Step-by-Step Execution

| **Stack**                    | **Script**                                                        | **Description**                                                                                 |
|-------------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `<sig>`                       | `OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP`    | The scriptSig is loaded onto the stack.                                                        |
| `<3 bytes> <sig'>`            | `OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP`                 | The first 3 bytes of the signature are split.                                                  |
| `<sig'>`                      | `OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP`                        | The 3-byte data item is removed.                                                               |
| `<r Length> <sig">`           | `OP_SWAP OP_SPLIT OP_DROP`                                      | The 1-byte r length is split from `sig'`.                                                      |
| `<sig"> <r Length>`           | `OP_SPLIT OP_DROP`                                              | The r length parameter is moved to the top of the stack.                                       |
| `<r> <sig''>`                 | `OP_DROP`                                                       | r is split from `sig"`.                                                                        |
| `<r>`                         | -                                                               | `sig''` is dropped, leaving only `r`.                                                          |

---

## Pay to R-Puzzle Hash (P2RPH)

The script to validate an R-Puzzle is:
```
OP_OVER OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 <Hash(r)> OP_EQUALVERIFY OP_CHECKSIG
```


---

## Security Considerations

### Protecting Private Keys
If the same **k** value is used for multiple signatures, the private key can be derived. Ensure:
1. Unique **k** values are used for each signature.
2. Deterministic **k** values are securely generated.

### Signature Forgeability
Given a signature **\<r, s\>** and a public key **P**, an attacker can create a different message **m'** and compute a new public key **P'** such that:
$$
P' = P + [r^{-1} \cdot (H(m) - H(m'))] \cdot G
$$
To mitigate this:
- Require an additional signature to prove knowledge of the private key corresponding to **P**.

---

## R-Puzzle Use Cases

1. **Delegation of Authority**:
   - Allows a third party to act on behalf of the owner with constraints.
2. **Tokens**:
   - Facilitates token-based systems using advanced scripts.
3. **Multi-Signature Schemes**:
   - Enables flexible multi-sig configurations.

---

## Tags

#RPuzzle #ECDSA #BitcoinScript #BSV #UTXO #DigitalSignatures #PayToRPuzzleHash

---

## See Also

- [[ECDSA]]
- [[UTXO Model]]
- [[Private Key]]
- [[Digital Signatures]]
- [[Bitcoin Script]]
