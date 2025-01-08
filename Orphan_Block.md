# Orphan Block in Blockchain

## Definition

An **Orphan Block** is a block of data in a blockchain that is not included in the final, confirmed ledger of transactions. This occurs because it was not integrated into the network's confirmed blockchain, which results in the block being literally "orphaned" and left alone. It is crucial to note that the transactions contained within orphan blocks are not invalidated; instead, they are typically re-integrated into the following blocks in the chain.

## Reasons for Orphan Blocks 

Orphan blocks are often created when two miners mine a block at similar times. As miners receive the broadcast of a newly mined block, they begin mining a new block that builds upon it. If two miners solve this next block at the same time and broadcast their solutions, this results in a temporarily forked chain, with two different blocks appended at the end. The network treats these blocks as [[Temporary Blocks]] until one of them gets an additional block appended. When this happens, one chain becomes longer, and, by general agreement, the network adopts the longer chain and discards the shorter one, orphaning the block.

## Impact of Orphan Blocks

While orphan blocks are essentially harmless, they can create temporary confusion and delay in the transaction verification process. Moreover, they cause disappointment to the miners who had mined the orphaned block as the network will reject their proof-of-work, and they will lose their claim on mining rewards. However, this forms the essential part of the consensus process, serving to decentralize the [[Decentralisation|block verification process]] and reduce the risk of double-spending [[Double-spending]].

## Conclusion

In summary, orphan blocks are an inherent aspect of the blockchain's design and the stochastic nature of block mining. They highlight the decentralized nature of the network and are instrumental in preventing double-spending and securing the overall network.
```