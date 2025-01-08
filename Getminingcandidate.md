*getminingcandidate* or GMC is a Remote Procedure Call (RPC) available
in the Bitcoin SV node software.

Its purpose is to provide mining software/pools with a suitable block
[[Mining Candidate|candidate]]for hashing in
order to mine a block. In addition it is greatly decoupled from block
size unlike its predecessor
[[GetBlockTemplate_interface|GetBlockTemplate]]meaning it can scale and support very large block
sizes.

The way it supports blocks of very large sizes is by only providing a
minimal set of data required for mining hardware to hash and generate a
possible block solution. If a blocksolution is found it can be returned
to the node software via the sibling RPC call *submitminingsolution*.

GMCs predecessor *getblocktemplate* gave the call mining software more
control, but in order to do this, it had to provide a full and complete
dataset of the current block and pending transactions in the mempool. A
Miner trying to mine large blocks must put a lot more strain on both the
node software and RPC interface to transmit a record of every
transaction that is in the mempool, often resulting in lack of memory
and/or performance issues.

GMC removes this issue by only providing the mining software with a
merkle proof of included transactions, rather than a complete listing,
this lowers the amount of data to be produced and transmitted to
log2(blocksize).

\
When the node software receives a GMC request it will respond with a
[JSON](https://www.json.org/json-en)representation of the current block candidate. A
description of this response body is shown below.

# Response body of getminingcandidate

  ------------------------------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                Variable                                                                                                                                                                                    Description
              \[uuid\] id                                                                                                                                            The assigned id from Bitcoind. This must be provided with submitting a potential solution
        \[hex string\] prevHash                                                                                                                                                                Big Endian hash of the previous block
   \[hex string\] Coinbase (optional)   Suggested coinbase transaction is provided. Miner is free to supply their own or alter the supplied one. Altering will require parsing and splitting the coinbase in order to splice in/out data as required. Requires Wallet to be enabled. Only returned when provide_coinbase_tx argument is set to true. Returns error if Wallet is not enabled
          \[int32_t\] version                                                                                                                                                                            The block version
       \[int64_t\] coinbaseValue                                                                                                                                                      Total funds available for the coinbase tx (in Satoshis)
           \[uint32_t\] nBits                                                                                                                                                                    Compressed hexadecimal difficulty
           \[uint32_t\] time                                                                                                                                                                            Current block time
             \[int\] height                                                                                                                                                                         The candidate block height
         \[array\] merkleProof                                                                                 Merkle branch/path for the block, used to calculate the [[Merkle_root|Merkle root]]of the block candidate. This is a list of Little-Endian hex strings ordered from top to bottom
  ------------------------------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

For a more technical breakdown of *GetMiningCandidate* and its
implementation, see the protocol spec
[here](https://github.com/bitcoin-sv-specs/protocol/blob/master/rpc/GetMiningCandidate.md)