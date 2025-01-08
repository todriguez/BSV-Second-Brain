# Signatures

Signatures are unique markings or methods used to signify consent, approval, or authentication. While traditionally they have been handwritten, the concept of signatures has evolved significantly with the rise of digital technologies.

---

## Types of Signatures

### 1. **Wet Signatures**
A **wet signature** refers to a physical signature created by a person marking a document. It is called "wet" because ink or another medium may still be wet immediately after signing.  
- Commonly used in paper-based agreements, contracts, and legal documents.

### 2. **Electronic Signatures**
An **electronic signature (e-signature)** is a digital representation of a person’s intent to sign a document.  
- Includes typed names, scanned signatures, or even a checkbox in a digital form.  
- Widely used in industries transitioning from paper to digital workflows.

### 3. **Digital Signatures**
**[[Digital signatures]]** are a subset of electronic signatures that use cryptographic methods to secure the authenticity and integrity of a document or message.  
- Created using public and private key pairs, such as in [[ECDSA]].  
- Essential in systems like [[BSV Blockchain]], where they validate transactions and ensure data integrity.

---

## Uses of Signatures

### 1. **Contracts and Agreements**
Signatures are used to signify mutual consent to the terms of a contract or agreement, making it legally binding.

### 2. **Financial Transactions**
Signatures on checks, authorization forms, and digital wallets indicate approval of the associated transaction.

### 3. **Legal Documents**
Wills, deeds, and other legal documents require signatures to confirm authenticity and legal enforcement.

### 4. **Art and Authentication**
Artists sign their work to establish authorship and provenance, while digital systems like [[NFTs]] use digital signatures for authentication.

---

## Signatures in [[Cryptology]]

In cryptology, a **digital signature** serves as proof that a particular action or document was authorized by the signer. Within the [[BSV Blockchain]] system, signatures are indispensable for:
- Verifying transaction authenticity through [[OP_CHECKSIG]] and related opcodes.  
- Ensuring integrity in [[Smart Contract]] and financial transactions.  
- Binding actions to identities in compliance frameworks, such as [[Bitcoin Certified Addresses (BCA)]] systems.

---

## Subset: Digital Signatures in BSV

### Creation Process
Digital signatures in BSV are created using [[Elliptic Curve Cryptography]]:
1. A private key is used to generate a signature for a message (transaction pre-image).  
2. A public key verifies the signature, ensuring only the private key holder could have signed it.

### Functions
- **Accountability:** Ties actions to specific entities.  
- **Compliance:** Ensures transactions meet [[KYC]] and [[AML]] standards.  
- **Security:** Prevents unauthorized modifications to signed data.

### Applications
- Binding conditions in [[Smart Contract]].  
- Validating ownership in [[tokenized assets]] or digital commodities.  
- Ensuring audit trails for regulatory purposes.

---

## Tags
- [[Signatures]]
- [[Digital Signatures]]
- [[Cryptology]]
- [[Smart Contract]]
- [[Compliance]]
- [[BSV Blockchain]]
- [[ECDSA]]
- [[Authentication]]
- [[Financial Transactions]]

---

Signatures, in their various forms, remain a cornerstone of trust, accountability, and authentication in both traditional and digital contexts. The evolution from wet signatures to cryptographic digital signatures exemplifies the ongoing shift toward secure, decentralized, and efficient systems.
