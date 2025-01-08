# Elliptic Curve Cryptography (ECC)

Elliptic Curve Cryptography (ECC) is a fundamental cryptographic system used in [[BSV Blockchain]] and many other secure systems. It provides a robust and efficient method for key generation, encryption, and [[digital signatures]], based on the mathematical properties of elliptic curves over finite fields.

---

## Overview

ECC relies on the properties of points on an elliptic curve defined by an equation of the form:

$$ y^2 = x^3 + ax + b $$

Where $a$ and $b$ are constants that determine the specific curve used, and the discriminant must satisfy conditions to ensure the curve is non-singular.

The [[BSV Blockchain]] network uses the **secp256k1** elliptic curve, defined as:

$$ y^2 = x^3 + 7 $$

This curve is chosen for its efficiency and security properties.

---

## Key Concepts

### 1. **The Generator Point ($G$)**
- The generator point $G$ is a predefined point on the elliptic curve.
- All cryptographic operations in ECC start from $G$.
- $G$ has a prime order $n$, meaning $nG = 0$ (the point at infinity).

### 2. **Private Key**
- A private key is a randomly selected integer $k$ in the range $[1, n-1]$.
- It must be kept secret to ensure security.

### 3. **Public Key**
- A public key is derived by multiplying the private key $k$ with the generator point $G$:
  $$ P = kG $$
- The resulting $P$ is a point on the elliptic curve, and it can be shared publicly.

---

## Operations in ECC

### 1. **Point Addition**
- Adding two points $P$ and $Q$ on the curve results in another point $R$:
  $$ R = P + Q $$

### 2. **Scalar Multiplication**
- Multiplying a point $P$ by a scalar $k$ involves repeated point addition:
  $$ Q = kP $$

---

## Why ECC for Bitcoin?

### 1. **Security**
- The difficulty of the **[[Elliptic Curve Discrete Logarithm Problem (ECDLP)]]** underpins ECC's security.
- Given $P$ and $Q = kP$, it is computationally infeasible to determine $k$.

### 2. **Efficiency**
- ECC achieves high levels of security with smaller key sizes compared to other cryptographic systems like [[RSA]].
- For example, a 256-bit ECC key provides comparable security to a 3072-bit RSA key.

### 3. **Compact Transactions**
- Smaller key sizes result in compact transactions, reducing on-chain storage requirements and transaction fees.

---

## Applications in Bitcoin

### 1. **Digital Signatures**
- ECC is used for generating [[ECDSA (Elliptic Curve Digital Signature Algorithm)]] signatures, ensuring the authenticity of transactions.
  - **Signing**: The private key generates a signature.
  - **Verification**: The public key verifies the signature.

### 2. **Key Derivation**
- Public and private keys are derived using the generator point $G$.
- [[Hierarchical Deterministic Wallets (HD Wallets)]] rely on ECC for deriving multiple keys from a single seed.

### 3. **End-to-End Encryption**
- ECC enables secure [[Elliptic Curve Diffie-Hellman (ECDH)]] key exchange for encrypted communication.

---

## ECC in Practice: secp256k1 Parameters

### Curve Definition
- $$ y^2 = x^3 + 7 $$

### Parameters
- Generator Point $G$: Predefined point on the curve.
- Prime Order $n$: The number of points on the curve, including the point at infinity.
- Field Size $p$: 256-bit prime number defining the finite field.

### Example Operations
1. Private Key: $k = 123456789$
2. Public Key: $P = kG$

---

## Tags

#EllipticCurveCryptography #ECC #Cryptography #Bitcoin #BSV #secp256k1 #DigitalSignatures #ECDSA #KeyDerivation #PublicKeyCryptography

---

## See Also

- [[ECDSA]]
- [[Hierarchical Deterministic Wallets]]
- [[Elliptic Curve Diffie-Hellman (ECDH)]]
- [[Bitcoin Script]]
- [[BSV Blockchain]]
- [[Private Key]]
- [[Public Key]]
- [[Generator Point ($G$)]]
