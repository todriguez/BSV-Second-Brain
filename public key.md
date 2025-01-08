# Public Key

A **Public Key** is a cryptographic value derived from a corresponding [[Private Key]] that enables secure communication, authentication, and digital signatures in modern cryptography. Public keys are a central component of [[Public Key Cryptography]] (PKC), allowing for asymmetric encryption and signature verification.

---

## Public Key in General

1. **Purpose**:
   - Public keys are shared openly to enable encrypted communication and identity verification.
   - They are mathematically related to private keys, forming a key pair.

2. **Asymmetric Encryption**:
   - A message encrypted with a public key can only be decrypted by its corresponding private key.
   - Conversely, a digital signature created with a private key can be verified using the corresponding public key.

3. **Mathematical Foundation**:
   - Public keys are derived using computationally secure mathematical functions, ensuring the infeasibility of deriving the private key from the public key.

---

## Public Key in Elliptic Curve Cryptography (ECC)

In [[Elliptic Curve Cryptography (ECC)]], a public key is a point on the elliptic curve derived from a private key, which is a scalar value. ECC provides stronger security per bit compared to traditional cryptography (e.g., RSA) due to the hardness of the [[Elliptic Curve Discrete Logarithm Problem]].

### Public Key Derivation in ECC

1. **Elliptic Curve Equation**:
   $$ y^2 = x^3 + ax + b \pmod{p} $$
   - Where $( a, b \in \mathbb{Z}_p )$ define the curve parameters, and $( p )$ is a prime number.

2. **Public Key Formula**:
   $$ Q = k \cdot G $$
   - $Q $: Public key (a point on the curve).
   - $k$: Private key (a scalar).
   - $G$: Generator point (defined by the curve parameters).
   - $( \cdot )$: Scalar multiplication operation.

3. **Key Properties**:
   - $Q$ is a point on the curve, represented as $(x, y)$.
   - Scalar multiplication ensures that the public key cannot feasibly be used to deduce $k$.

---

## Public Key in secp256k1

The **secp256k1** curve is the elliptic curve used in [[Bitcoin]] and [[BSV Blockchain]] for public key cryptography. It is defined by specific parameters optimized for cryptographic efficiency.

### secp256k1 Parameters

1. **Curve Equation**:
   $$ y^2 = x^3 + 7 \pmod{p} $$
  - $( p = 2^{256} - 2^{32} - 977 )$: A prime number defining the finite field.

2. **Generator Point**:
   $$ G = (x_G, y_G) $$
   $( x_G = 55066263022277343669578718895168534326250603453777594175500187360389116729240 )$
   $( y_G = 32670510020758816978083085130507043184471273380659243275938904335757337482424 )$

3. **Order of $G$**:
   $$ n = 2^{256} - 432420386565659656852420866394968145599 $$
   - Defines the number of points on the curve.

4. **Cofactor**:
   $$ h = 1 $$

### Public Key Derivation in secp256k1

Given a private key $k$, the public key is:
$$ Q = k \cdot G $$

### Compact Representation

1. **Uncompressed Format**:
   -  $Q = (x, y)$
   - Represented as a 65-byte value: $( 0x04 \| x \| y )$

2. **Compressed Format**:
   - Uses only  $x$ and the parity of  $y$.
   - Represented as a 33-byte value: $( 0x02 \| x )$ if $y$ is even or $( 0x03 \| x )$ if  $y$ is odd.

---

## Applications of Public Keys

1. **Digital Signatures**:
   - Verifying the authenticity of a [[Transaction]] in Bitcoin using [[ECDSA]].

2. **Encryption**:
   - Enabling secure message exchange in communication protocols.

3. **Address Generation**:
   - Public keys are hashed to generate Bitcoin addresses for receiving payments.

4. **Identity Verification**:
   - Proving ownership of the corresponding private key without exposing it.

---

## Tags

#PublicKey #Cryptography #EllipticCurveCryptography #secp256k1 #Bitcoin #BSV #ECDSA #DigitalSignatures

---

## See Also

- [[Private Key]]
- [[Elliptic Curve Cryptography (ECC)]]
- [[secp256k1]]
- [[Digital Signatures]]
- [[ECDSA]]
- [[Address]]
