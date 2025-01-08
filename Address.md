An **address** is an identifier comprising 26–35 alphanumeric characters. These addresses represent the [[HASH160]] of a [[public key]], produced through the combined use of [[SHA-256]] and [[RIPEMD160]], and are used in [[Pay-to-Public-Key-Hash (P2PKH)|P2PKH]] outputs to facilitate [[Bitcoin Payment|BSV payments]]. BSV addresses commonly begin with the number `1` (e.g., `1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2`).

---

## Structure of a BSV Address

BSV addresses are created using [[Base58Check encoding|Base58Check Encoding]], which includes the following components:

1. **Version Prefix**: Indicates the address type (e.g., `0x00` for mainnet P2PKH addresses).  
2. **Payload**: The [[HASH160]] of the public key, derived by hashing the [[public key]] first with [[SHA-256]] and then with [[RIPEMD160]].  
3. **Checksum**: A 4-byte value appended to the end of the address to ensure integrity, calculated using the first 4 bytes of a double [[SHA-256]] hash of the version and payload.

This structure ensures data integrity, reduces the likelihood of errors due to mistyped addresses, and makes addresses compatible with various systems.

---

## Privacy Concerns

### Address Reuse
Reusing the same address for multiple transactions compromises privacy by making it easy to trace funds and link transactions to a common owner. [[Address Reuse|Address reuse]] is strongly discouraged, as emphasized in **Section 10: Privacy** of the [[Bitcoin Whitepaper|Bitcoin Whitepaper]], which states:

> *"As an additional [[Firewall (Identity)|firewall]], a new key pair should be used for each transaction to keep them from being linked to a common owner."*

To maintain privacy, users should generate a new address for each payment.

---

## Offline Address Creation

BSV addresses can be generated offline without requiring interaction with the BSV network. This capability is particularly useful for:

- **Secure Environments**: Ensures sensitive operations are conducted offline, reducing attack vectors.  
- **E-commerce**: Allows pre-generating unique addresses for customers using a "pay with BSV" option.  
- **[[HD Wallets]]**: Derives unlimited addresses from a master public key without exposing private keys.

Offline generation enhances security and supports diverse use cases.

---

## Case Sensitivity and Validation

BSV addresses are case-sensitive and must be copied exactly to ensure validity. Errors in transcription, including capitalization, will result in invalid addresses. The checksum feature significantly reduces the probability of an undetected error to approximately 1 in 4.29 billion (`1 in 2^32`).

### Address Validation
Address validation should be performed using tools or libraries that adhere to the [[Base58Check encoding]] specification. This process ensures that the address is syntactically correct and matches the checksum.

---

## Proving Ownership with an Address

BSV wallets provide functionality to sign messages using the private key associated with an address. This capability can be used to:

- **Prove Ownership**: Demonstrate control over a specific address.  
- **Sign Contracts**: Cryptographically finalize agreements.  

Signed messages can serve as evidence in various contexts, ensuring authenticity and verifiability.

---

## Misconceptions

### Address Balances
BSV addresses do not hold balances. Instead, funds are tracked as [[UTXO|UTXOs]] associated with the address. Misinterpreting "address balances" can lead to errors, such as loss of funds when change is sent to a new address.

### "From" Addresses
BSV transactions do not specify a "from" address. Instead, they unlock UTXOs and create new ones. Address-based tracking of origins is a flawed abstraction introduced by some wallet interfaces.

---

## Testnet Addresses

Addresses on the BSV [[Testnet]] use a different version prefix, resulting in distinct identifiers from mainnet addresses. This ensures testnet transactions remain isolated from mainnet.

---

## See Also

- [[Technical Background of Bitcoin Addresses]]  
- [[Elliptic Curve Digital Signature Algorithm (ECDSA)]]  
- [[Base58Check encoding]]  
- [[HASH160]]  
- [[SHA-256]]  
- [[RIPEMD160]]  
- [[Private Key]]  
- [[HD Wallets]]  
- [[Address Reuse]]  
- [[Bitcoin Payment]]  

---

## Tags:
#BSV #Addresses #P2PKH #Base58Check #HASH160 #SHA256 #RIPEMD160 #Privacy #UTXO #Cryptography




