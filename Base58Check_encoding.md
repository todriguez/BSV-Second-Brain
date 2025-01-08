**Base58Check** is a modified version of Base58 binary-to-text encoding, specifically designed for encoding Bitcoin-related data. It is used to encode [[Address|Bitcoin addresses]] and other byte arrays in Bitcoin into human-readable, easily typable strings.

---

## Background

The original Bitcoin client source code outlines the rationale behind Base58 encoding:

> "Why base-58 instead of standard base-64 encoding?  
> - Avoid 0OIl characters that look similar in some fonts and could create visually identical account numbers.  
> - A string with non-alphanumeric characters is not as easily accepted as an account number.  
> - E-mail usually won't line-break if there's no punctuation to break at.  
> - Double-clicking selects the whole number as one word if it's all alphanumeric."

---

## Features of Base58Check

1. **Arbitrary Payload Size**: It supports encoding arbitrary-length byte arrays.  
2. **Reduced Ambiguity**: Excludes easily confused characters (`0`, `O`, `I`, `l`).  
3. **Version/Application Byte**: Includes one byte for version or application information.  
4. **Error Detection**: Adds a 4-byte checksum derived from [[SHA-256]] to detect typographical errors.  
5. **Preservation of Leading Zeros**: Encodes leading zero bytes as the character `1`.

---

## Creating a Base58Check String

A Base58Check string is created from a version byte and payload using the following steps:

1. **Concatenate Version Byte and Payload**:  
   Combine the version byte with the payload (byte array).  

   $$ \text{data} = \text{version byte} \| \text{payload bytes} $$

2. **Compute Checksum**:  
   Take the first four bytes of:  
   $$ \text{checksum} = \text{SHA256}(\text{SHA256}(\text{data}))[:4] $$

3. **Concatenate Data and Checksum**:  
   Combine the data from Step 1 with the checksum:  
   $$ \text{final\_data} = \text{data} \| \text{checksum} $$

4. **Convert to Base58**:  
   Treat `final_data` as a single big-endian integer and convert it to Base58 using the Base58 alphabet.

5. **Handle Leading Zeros**:  
   For each leading zero byte in `final_data`, prepend a `1` character to the Base58 result.

The final result is the Base58Check-encoded string.

---

## Encoding a Bitcoin Address

Bitcoin addresses are Base58Check-encoded hashes of [[ECDSA]] public keys:

1. For **Pay-to-PubKey-Hash (P2PKH)**:
   - Payload:  
     $$ \text{RIPEMD160}(\text{SHA256}(\text{ECDSA Public Key})) $$
   - Version Byte: `0x00` (produces addresses beginning with `1`).

2. Address Characteristics:
   - Hash size: 20 bytes.
   - Version byte ensures unique prefixes for different address types.

---

## Encoding a Private Key

Base58Check is also used to encode [[Private Key|private keys]] in the [[Wallet Import Format (WIF)]]. Differences include:

1. **Version Byte**: `0x80` (produces strings beginning with `5H`, `5J`, or `5K` for uncompressed keys).  
2. **Payload Size**: 32 bytes (private key size).  

For compressed public keys, an additional byte (`0x01`) is appended to the payload before encoding.

---

## Base58 Alphabet

The Bitcoin-specific Base58 alphabet excludes ambiguous characters:

| **Value** | **Character** | **Value** | **Character** | **Value** | **Character** | **Value** | **Character** |
|-----------|---------------|-----------|---------------|-----------|---------------|-----------|---------------|
| 0         | 1             | 16        | H             | 32        | Z             | 48        | q             |
| 1         | 2             | 17        | J             | 33        | a             | 49        | r             |
| 2         | 3             | 18        | K             | 34        | b             | 50        | s             |
| 3         | 4             | 19        | L             | 35        | c             | 51        | t             |
| 4         | 5             | 20        | M             | 36        | d             | 52        | u             |
| 5         | 6             | 21        | N             | 37        | e             | 53        | v             |
| 6         | 7             | 22        | P             | 38        | f             | 54        | w             |
| 7         | 8             | 23        | Q             | 39        | g             | 55        | x             |
| 8         | 9             | 24        | R             | 40        | h             | 56        | y             |
| 9         | A             | 25        | S             | 41        | i             | 57        | z             |
| 10        | B             | 26        | T             | 42        | j             |           |               |
| 11        | C             | 27        | U             | 43        | k             |           |               |
| 12        | D             | 28        | V             | 44        | m             |           |               |
| 13        | E             | 29        | W             | 45        | n             |           |               |
| 14        | F             | 30        | X             | 46        | o             |           |               |
| 15        | G             | 31        | Y             | 47        | p             |           |               |

---

## Version Bytes

Some common version bytes and their uses:

| **Version (Decimal)** | **Leading Symbol** | **Use**                         |
|------------------------|--------------------|----------------------------------|
| 0                      | `1`                | Bitcoin pubkey hash             |
| 21                     | `4`                | Bitcoin compact pubkey (proposed)|
| 52                     | `M` or `N`         | Namecoin pubkey hash            |
| 128                    | `5`                | Bitcoin private key (WIF)       |
| 111                    | `m` or `n`         | Bitcoin testnet pubkey hash     |

---

## Considerations

1. **Hash Consistency**: Handle leading or trailing `0x00` bytes properly to avoid address mismatches.
2. **Error Detection**: The checksum allows for detecting, but not correcting, typographical errors.
3. **Versioning**: The version byte ensures compatibility with multiple protocols.

---

## Tags

#Base58Check #Bitcoin #Encoding #Cryptography #BitcoinAddresses #WIF #Checksum

---

## See Also

- [[Address]]
- [[Wallet Import Format]]
- [[ECDSA]]
- [[SHA-256]]
