# Bitcoin Request for Comments (BRC)

**BRC: Bitcoin Request for Comments**  
A repository for submitting, discussing, sharing, and indexing technical proposals for use across the Bitcoin ecosystem.

---

## 🛠 Contributing
Contributions from all builders are welcome.  
- To propose a new [[BRC]], fork the repo and use the [[EXAMPLE.md]] template.
- Submit a pull request for review once your proposal is ready.  
For full guidelines, see [[Contributing]].

---

## 📂 Directory Structure and Standards

### [[Apps]]
- **BRC-102**: [[deployment-info.json Specification]]  
  Tags: #apps #deployment

---

### [[Key Derivation]]
- **BRC-32**: [[BIP32 Key Derivation Scheme]]  
  Tags: #key-derivation #BIP32
- **BRC-42**: [[BSV Key Derivation Scheme (BKDS)]]  
  Tags: #key-derivation #BSV
- **BRC-43**: [[Security Levels, Protocol IDs, Key IDs]]  
  Tags: #security
- **BRC-44**: [[Admin-reserved Key Derivation Protocols]]  
  Tags: #key-derivation
- **BRC-69**: [[Revealing Key Linkages]]  
  Tags: #privacy #key-linkages
- **BRC-72**: [[Protecting BRC-69 Key Linkage Information]]  
  Tags: #privacy #key-protection
- **BRC-75**: [[Mnemonic for Master Private Key]]  
  Tags: #mnemonic #key-derivation
- **BRC-84**: [[Linked Key Derivation Scheme]]  
  Tags: #key-derivation #linked-keys
- **BRC-86**: [[Bidirectionally Authenticated Derivation of Privacy-Restricted Keys]]  
  Tags: #privacy #key-authentication
- **BRC-93**: [[Limitations of BRC-69 Key Linkage Revelation]]  
  Tags: #privacy #key-linkages
- **BRC-94**: [[Verifiable Revelation of Shared Secrets Using Schnorr Protocol]]  
  Tags: #security #schnorr

---

### [[Opinions]]
- **BRC-49**: [[Users Should Never See an Address]]  
  Tags: #user-experience #address-privacy
- **BRC-51**: [[List of User Experiences]]  
  Tags: #user-experience
- **BRC-57**: [[Legitimate Uses for mAPI]]  
  Tags: #mAPI #networking
- **BRC-59**: [[Security and Scalability of UTXO-based Overlay Networks]]  
  Tags: #overlay-networks #scalability
- **BRC-80**: [[Improving on MLD for BSV Multicast Services]]  
  Tags: #multicast #improvements
- **BRC-89**: [[Web 3.0 Standards (High-Level Overview)]]  
  Tags: #web3 #standards
- **BRC-90**: [[Thoughts on the Mandala Network]]  
  Tags: #mandala-network
- **BRC-91**: [[Outputs, Overlays, and Scripts in the Mandala Network]]  
  Tags: #mandala-network

---

### [[Outpoints]]
- **BRC-36**: [[Format for Bitcoin Outpoints]]  
  Tags: #outpoints #format
- **BRC-37**: [[Spending Instructions for UTXO Storage Format]]  
  Tags: #UTXO #outpoints

---

### [[Overlays]]
- **BRC-22**: [[Overlay Network Data Synchronization]]  
  Tags: #overlay-network #synchronization
- **BRC-23**: [[Confederacy Host Interconnect Protocol (CHIP)]]  
  Tags: #overlay-network #confederacy
- **BRC-24**: [[Overlay Network Lookup Services]]  
  Tags: #overlay-network #lookup
- **BRC-25**: [[Confederacy Lookup Availability Protocol (CLAP)]]  
  Tags: #overlay-network #availability
- **BRC-26**: [[Universal Hash Resolution Protocol]]  
  Tags: #overlay-network #hash-resolution
- **BRC-64**: [[Overlay Network Transaction History Tracking]]  
  Tags: #overlay-network #transaction-history
- **BRC-81**: [[Private Overlays with P2PKH Transactions]]  
  Tags: #overlay-network #private-overlays
- **BRC-87**: [[Naming Conventions for BRC-22 Managers and BRC-24 Services]]  
  Tags: #overlay-network #naming
- **BRC-88**: [[Overlay Services Synchronization Architecture]]  
  Tags: #overlay-network #architecture
- **BRC-101**: [[Diverse Facilitators for SHIP and SLAP Overlay Ads]]  
  Tags: #overlay-network #advertising

### [[Payments]]
- **BRC-27**: [[Direct Payment Protocol (DPP)]]  
  Tags: #payments #protocol
- **BRC-28**: [[Paymail Payment Destinations]]  
  Tags: #payments #paymail
- **BRC-29**: [[Authenticated BSV P2PKH Payment Protocol]]  
  Tags: #payments #P2PKH
- **BRC-41**: [[PacketPay HTTP Payment Mechanism]]  
  Tags: #payments #HTTP
- **BRC-54**: [[Hybrid Payment Mode for DPP]]  
  Tags: #payments #hybrid
- **BRC-55**: [[HTTPS Transport Mechanism for DPP]]  
  Tags: #payments #HTTPS
- **BRC-70**: [[Paymail BEEF Transaction]]  
  Tags: #payments #BEEF

---

### [[Peer-to-Peer]]
- **BRC-31**: [Authrite Mutual Authentication](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0031.md)  
  Tags: #peer-to-peer #authrite
- **BRC-33**: [PeerServ Message Relay Interface](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0033.md)  
  Tags: #peer-to-peer #message-relay
- **BRC-34**: [PeerServ Host Interconnect Protocol](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0034.md)  
  Tags: #peer-to-peer #interconnect
- **BRC-52**: [Identity Certificates](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0052.md)  
  Tags: #peer-to-peer #identity
- **BRC-63**: [Genealogical Identity Protocol](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0063.md)  
  Tags: #peer-to-peer #identity
- **BRC-68**: [Publishing Trust Anchor Details at a Domain](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0068.md)  
  Tags: #peer-to-peer #trust-anchor
- **BRC-77**: [Message Signature Creation and Verification](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0077.md)  
  Tags: #peer-to-peer #signatures
- **BRC-78**: [Portable Encrypted Messages Format](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0078.md)  
  Tags: #peer-to-peer #encryption
- **BRC-82**: [IPv6 Multicast Protocol for Blockchain](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0082.md)  
  Tags: #peer-to-peer #IPv6
- **BRC-85**: [Proven Identity Key Exchange (PIKE)](https://github.com/bitcoin-sv/BRCs/blob/master/peer-to-peer/0085.md)  
  Tags: #peer-to-peer #PIKE

---

### [[Scripts]]
- **BRC-14**: [Bitcoin Script Binary, Hex, and ASM Formats](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0014.md)  
  Tags: #scripts #formats
- **BRC-15**: [Bitcoin Script Assembly Language](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0015.md)  
  Tags: #scripts #assembly
- **BRC-16**: [Pay to Public Key Hash](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0016.md)  
  Tags: #scripts #P2PKH
- **BRC-17**: [Pay to R Puzzle Hash](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0017.md)  
  Tags: #scripts #R-puzzle
- **BRC-18**: [Pay to False Return](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0018.md)  
  Tags: #scripts #false-return
- **BRC-19**: [Pay to True Return](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0019.md)  
  Tags: #scripts #true-return
- **BRC-21**: [Push TX](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0021.md)  
  Tags: #scripts #push-TX
- **BRC-47**: [Bare Multi-Signature](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0047.md)  
  Tags: #scripts #multi-signature
- **BRC-48**: [Pay to Push Drop](https://github.com/bitcoin-sv/BRCs/blob/master/scripts/0048.md)  
  Tags: #scripts #push-drop

---

### [[State Machines]]
- **BRC-60**: [Simplifying State Machine Event Chains in Bitcoin](https://github.com/bitcoin-sv/BRCs/blob/master/state-machines/0060.md)  
  Tags: #state-machines #event-chains
