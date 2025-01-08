https://arxiv.org/abs/2311.15842

# Bitcoin-Certified Addresses (BCA)

Bitcoin-Certified Addresses (BCA) leverage the computational power of the [[BSV Network]] to bind [[IPv6]] addresses to public keys, creating a secure and efficient mechanism for address generation and verification. This innovation reuses the [[Proof of Work]] computed by [[nodes]] to enhance security and reduce the computational burden on hosts.

---

## Overview

BCA improves upon the concept of [[Cryptographically Generated Addresses (CGA)]] by using Bitcoin's distributed infrastructure to solve the inefficiencies and vulnerabilities associated with CGA. By registering public keys on the BSV blockchain, BCA establishes a provable link between IPv6 addresses and their owners, ensuring strong resistance to spoofing attacks and privacy protection.

---

## How Bitcoin-Certified Addresses Work

### Public Key Registration

1. Hosts register their [[public key]] on the BSV blockchain via a transaction containing:
   - The [[hash]] of the public key.
   - A [[Merkle Tree]] root derived from a list of randomly generated modifiers.
   
2. Once included in a block, the transaction is verified using:
   - The block header.
   - A Merkle proof of inclusion for the transaction.

3. The [[Difficulty]] value of the block determines the **security parameter (sec)** of the BCA.

### Address Generation

To generate an IPv6 address, hosts use the following inputs:
- [[Modifier value]] (from the committed list).
- [[Block header]].
- [[Subnet prefix]].
- Transaction data.

The process involves:
1. Hashing the inputs to compute `Hash1`.
2. Deriving the IPv6 interface identifier by encoding the `sec` parameter and setting the appropriate IPv6 bits.
3. Concatenating the subnet prefix and interface identifier to form the IPv6 address.

Addresses can be quickly generated and changed by selecting new modifiers from the committed list.

### Verification

Verification ensures the integrity of the address and its binding to the public key:
1. Validate the format and consistency of the [[BCA Parameters]].
2. Verify the Merkle proofs for the transaction and modifier inclusion.
3. Check that the block header satisfies the required PoW difficulty.

---

## Advantages of Bitcoin-Certified Addresses

### Security
- BCA inherits the robustness of BSV's PoW, making it more resistant to spoofing than CGA.
- The security parameter `sec` scales with BSV's network difficulty, ensuring future-proof resistance.

### Efficiency
- BCA eliminates the need for hosts to perform computationally intensive tasks during address generation.
- A new address can be generated in microseconds, compared to minutes for CGA.

### Privacy
- Hosts can frequently change their addresses by using different modifiers, protecting against activity correlation attacks.
- Modifier randomness ensures unlink-ability between addresses derived from the same public key.

### Disibutred
- BCA leverages the existing BSV infrastructure, avoiding reliance on centralized authorities or additional security systems.

---

## Applications of BCA

### IPv6 Network Security
- Protects against address spoofing in [[Neighbor Discovery Protocol (NDP)]].
- Enhances security in environments like public wireless networks and [[IoT]] systems.

### Identity and Authentication
- Ensures provable ownership of IPv6 addresses through binding with public keys.
- Supports secure communication protocols requiring address authenticity.

### [[Internet of Things]] (IoT)
- Provides lightweight, scalable address generation suitable for low-power devices.
- Reduces computational overhead for IoT networks requiring frequent address changes.

---

## Comparison: BCA vs. CGA

| **Aspect**               | **BCA**                                  | **CGA**                                 |
|--------------------------|------------------------------------------|-----------------------------------------|
| **Security**             | PoW-based, scales with Bitcoin difficulty. | Limited by host computational power.   |
| **Performance**          | Microseconds per address.               | Minutes per address.                   |
| **Decentralization**     | Relies on the Bitcoin network.           | Fully decentralized but resource-heavy. |
| **Privacy**              | Frequent address changes with modifiers. | Address changes disincentivized.       |
| **Usability**            | Minimal computational cost for hosts.    | High cost limits practicality.         |

---

## Technical Components

### BCA Parameters
| **Field**                | **Description**                          | **Size**                                |
|--------------------------|------------------------------------------|-----------------------------------------|
| Modifier                 | Randomly generated, enhances privacy.   | 16 bytes                               |
| Public Key               | Associated with the IPv6 address.       | Variable length                        |
| Transaction              | Registers the public key on the blockchain. | Variable length                     |
| Block Header             | Secures the binding with PoW.           | 80 bytes                               |
| Subnet Prefix            | IPv6 subnet information.                | 8 bytes                                |
| Collision Count          | Handles duplicate address detection.    | 1 byte                                 |
| Merkle Proof of Transaction | Verifies transaction inclusion in block. | Max 896 bytes (with \( M_{max} = 2^{28} \)) |
| Merkle Proof of Modifier | Verifies modifier inclusion in transaction. | Max 160 bytes (with \( N_{max} = 32 \)) |

### Security Parameter (sec)
Derived from Bitcoin's PoW difficulty, the `sec` parameter determines the resistance against spoofing:
- **Minimum:** `sec = 0` (32 bits of PoW).
- **Maximum:** `sec = 7` (144 bits of PoW).

---

## Deployment Considerations

- **Scalability**: Requires Bitcoin implementations with high transaction throughput (e.g., [[BSV Blockchain]]).
- **Transaction Costs**: Minimal fees for public key registration.
- **IoT Integration**: Ideal for low-power devices due to efficient address generation.
- **Interoperability**: Can be combined with CGA for transitional use cases.

---

## Tags

#Bitcoin #IPv6 #ProofOfWork #BitcoinCertifiedAddresses #Security #Decentralization #Privacy #IoT #NeighborDiscoveryProtocol

---

## See Also

- [[Cryptographically Generated Addresses (CGA)]]
- [[Proof of Work]]
- [[Merkle Tree]]
- [[Bitcoin Network]]
- [[BSV Blockchain]]
- [[Neighbor Discovery Protocol (NDP)]]




