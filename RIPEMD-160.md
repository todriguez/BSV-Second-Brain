**RIPEMD-160** is a cryptographic hash function used in the [[BSV Blockchain]] system. It was originally designed as part of the RIPE (RACE Integrity Primitives Evaluation) project, aimed at creating secure and efficient cryptographic primitives. RIPEMD-160 is a 160-bit hash function, providing a compact and secure output, which is integral to key operations in Bitcoin SV, such as the `HASH160` function.

---

## Overview of RIPEMD-160

### Key Characteristics
- **Output Size**: 160 bits (20 bytes).
- **Collision Resistance**: Designed to minimize the chances of two different inputs producing the same hash.
- **Preimage Resistance**: It is computationally infeasible to reverse-engineer the input from the hash.
- **Efficiency**: Lightweight and optimized for performance on modern hardware.

### Historical Context
RIPEMD-160 was developed by a team of researchers in the 1990s as part of the European Union's RACE project. While it shares similarities with the [[MD5]] and [[SHA-1]] families of hash functions, RIPEMD-160 was designed with additional robustness against cryptographic vulnerabilities identified in earlier algorithms.

---

## Role in BSV

RIPEMD-160 is a vital component of the `HASH160` function, which combines it with [[SHA-256]]. This dual-hashing mechanism serves two primary purposes in BSV:

1. **Address Generation**: RIPEMD-160 compacts the output of SHA-256 to produce BSV addresses.
2. **Transaction Validation**: The resulting hash is used in locking and unlocking scripts to ensure that funds are only accessible to the intended recipient.

---

## `HASH160` Function in BSV

The `HASH160` function is defined as:
1. **Step 1**: Hash the input (e.g., a public key) using SHA-256.
2. **Step 2**: Hash the SHA-256 output using RIPEMD-160.

This double-hashing provides enhanced security by combining the strengths of both algorithms. The output is a 20-byte value, which is compact and efficient for use in scripts and addresses.

---

## `OP_HASH160` Opcode

The Bitcoin SV scripting language includes the `OP_HASH160` opcode, which implements the `HASH160` function directly in script execution.

### Syntax and Functionality
- **Opcode**: `OP_HASH160`
- **Hexadecimal**: `0xa9`
- **Purpose**: Applies SHA-256 followed by RIPEMD-160 to the top stack element and replaces it with the hash.

### Example: Pay-to-PubKey-Hash (P2PKH) Script
A typical P2PKH script uses `OP_HASH160` as follows:

#### lockScript
```
OP_DUP OP_HASH160 <pubkeyhash> OP_EQUALVERIFY OP_CHECKSIG
```

#### unlockScript

```
<signature> <public key>
```

Steps:

1. `OP_DUP`: Duplicates the public key on the stack.
2. `OP_HASH160`: Applies the `HASH160` function to produce a 20-byte hash.
3. `<pubkeyhash>`: Pushes the expected hash onto the stack.
4. `OP_EQUALVERIFY`: Ensures the calculated and expected hashes match.
5. `OP_CHECKSIG`: Verifies the signature against the public key.

---

## Benefits of RIPEMD-160 in BSV

### Compact Representation

The 160-bit output reduces the size of public key representations, saving storage and bandwidth.

### Enhanced Security

Combining SHA-256 and RIPEMD-160 in `HASH160` offers:

- **Collision Resistance**: Reduces the likelihood of two inputs producing the same hash.
- **Resistance to Preimage Attacks**: Ensures that hash values cannot be reverse-engineered to reveal the input.

### Lightweight Computation

RIPEMD-160 is computationally efficient, making it suitable for blockchain environments where performance and resource efficiency are critical.

---

## Applications in Bitcoin SV

1. **BSV Addresses**: RIPEMD-160 hashes are used to create [[Base58Check]]-encoded addresses, which are human-readable and easy to validate.
2. **Locking and Unlocking Scripts**: RIPEMD-160 ensures secure transaction validation by hashing public keys in scripts.
3. **Data Integrity**: The algorithm is used to provide cryptographic proofs of integrity for public keys and other critical data.

---

## Tags

- [[RIPEMD-160]]
- [[HASH160]]
- [[OP_HASH160]]
- [[SHA-256]]
- [[Bitcoin Script]]
- [[Pay-to-PubKey-Hash]]
- [[Cryptographic Security]]
- [[Base58Check]]
- [[BSV Blockchain]]

