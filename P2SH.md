
**Pay to Script Hash (P2SH)** was deprecated as part of the [[Genesis Upgrade]] on the [[BSV Blockchain]] network in February 2020.

---

## History of P2SH

P2SH transactions were designed to lock funds with a **script hash**. To spend funds locked in a P2SH output, the spender had to provide a script matching the hash and the necessary data to satisfy the script's conditions. P2SH was introduced as [BIP-0016](https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki).

- **Purpose**:  
  P2SH was developed to expand the use of Bitcoin [[Script]] while adhering to the constraints introduced by limits and transaction standardization on the BTC network.
  
- **Script Hashing**:  
  Users could create customized scripts, hash them, and convert them into a ~34-character P2SH address. These addresses were most commonly used for:
  - Managing [[Multisignature Wallets|multisignature wallets]] (e.g., 2-of-3 signatures required).  
  - Simplifying complex scripts into a single hash for improved usability.

- **Address Format**:  
  P2SH addresses always started with the prefix `3`.

---

## Deprecation in Bitcoin SV

With the [[Genesis Upgrade]], P2SH was deprecated on the BSV blockchain. The deprecation reflects Bitcoin SV’s philosophy of adhering to [[Satoshi Nakamoto|Satoshi Nakamoto's]] original design for Bitcoin, which did not include P2SH.

- **Consensus Changes**:  
  While P2SH outputs remain technically spendable under network rules, any transactions generated after Genesis using a P2SH output script are considered invalid by [[Consensus Rules]].

- **Rationale for Deprecation**:  
  - Restoration of the original Bitcoin [[Protocol]].  
  - Removal of features that obscure the visibility of script logic, favoring transparent and auditable transactions.  

---

## Spending P2SH Outputs

- **Legacy Compatibility**:  
  P2SH outputs created before the [[Genesis Upgrade]] remain spendable under current network rules.  
  - To spend these outputs, users must provide the original script and satisfy its conditions.  

- **Post-Genesis Transactions**:  
  Any transaction attempting to generate new P2SH outputs after the Genesis Upgrade is invalid under BSV consensus.

---

## Tags

- [[Pay to Script Hash (P2SH)]]  
- [[BSV Blockchain]]  
- [[Genesis Upgrade]]  
- [[Multisignature Wallets]]  
- [[Script]]  
- [[Consensus Rules]]  
- [[Protocol Restoration]]  
