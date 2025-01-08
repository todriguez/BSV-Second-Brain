# Coinbase Transaction

**Tags**: #Coinbase #GenerationTransaction #Mining #Miner #Block #BlockHeader #GenesisBlock #Protocol #BIP34 #VarInt #TXID #MinerSubsidy #TransactionFees #ExtraNonce #MerkleRoot #MerkleTree #Nonce #Index

A **Coinbase** (or **Generation Transaction**) is a **unique** transaction in every [[Block]]. It serves as the mechanism by which new coins—originally issued with the [[GenesisBlock|genesis block]]—are **distributed** (via the **[[Miner_subsidy|block subsidy]]**) and by which **[[TransactionFees|fees]]** are recirculated.

## Creation by the Winning Miner

The winning [[Miner]] creates this special transaction as part of the block templating process. Unlike a normal transaction, the **Coinbase** transaction:

1. **Has exactly one txin**.  
2. This txin’s **prevout hash** is `0000...0000`.  
3. This txin’s **prevout [[Index|index]]** is `0xFFFFFFFF`.  
4. The txin’s **prevout script** is an arbitrary byte array, historically used by miners to signal identity and embed small messages in the block.  
5. The sum of the values of all **txout** fields cannot exceed the total of the **[[Miner_subsidy|Miner subsidy]]** plus the mining fees paid by the other transactions in the block.

Because it has no actual inputs, the Coinbase transaction is **unique** among all transaction types in the blockchain.

---

## Extra Nonce and Large Hash Searches

A single [[ASIC_Miner|ASIC Miner]] can test more combinations than the $2^{32}$ possibilities offered by the [[Nonce]] in the [[Block header|block header]]. To circumvent this limitation, a part of the Coinbase can be used as an “extra nonce.” Incrementing the extra nonce changes certain hashes within the [[Merkle Tree|Merkle Tree]], resulting in a new **[[Merkle_root|Merkle Root]]**, which in turn alters the block header hash. This expansion effectively doubles the search space by another $2^{32}$ possibilities, enabling miners to continue seeking a valid block solution.

---

## Multiple Outputs

Miners can create as many outputs as needed in the Coinbase transaction. These outputs can serve **second-layer** functions, for instance:

- **[[Merchant_API|Merchant API (MAPI)]]**  
  Allows the winning Miner to provide real-time pricing, broadcast services, and fee quotes to users of the network.  
- **[[MinerID|Miner ID]]**  
  Presents information (node identity, MAPI access points, etc.) directly to the network via the Coinbase transaction. Wallets can read and parse this standardized data to keep updated on which nodes are currently mining.

---

## Historical Constraints and BIP 0034

Early in Bitcoin’s history, some blocks contained only a coinbase transaction that had the same coinbase text and outputs, leading to identical **[[TXID|TXIDs]]**. To fix this, the community enforced [[BIP 0034]] via [[Protocol|protocol]] consensus. BIP 0034 requires the **block height** to be specified as the first item in the coinbase transaction.  

- **Coinbase Script Size**  
  - Before BIP 0034, this size ranged from 2 to 100 bytes.  
  - Currently, the minimum length is 4 bytes, needed to store the block height as a [[VarInt|VarInt]].  
  - The maximum 3-byte value is **16,777,215**. At a rate of ~59,000 blocks per year, around the year 2300, this minimum length will likely need to increase to 5 bytes.

With these rules in place, the Coinbase transaction remains a core pillar of how new coins are introduced and how block rewards and fees are consolidated and distributed within the network.


