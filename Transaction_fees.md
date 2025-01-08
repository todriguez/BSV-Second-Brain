**Transaction fees** are fees that Bitcoin users may include in any
[[Bitcoin Transactions|Bitcoin Transactions]]. The
fees may be collected by the Miner who includes the transaction in a
[[Block|Block]].

Transaction fees are a service charge paid to the Miners who record the
Bitcoin ledger. The services provided by Miners are transaction
validation, storage of the ledger, and the construction and security of
the Bitcoin network.

# Overview

Every Bitcoin transaction transfers one or more satoshis to one or more
recipients. The difference between the amount being spent from previous
outputs and the amount being sent to new outputs is the transaction fee
(which must be zero or more).

Bitcoin\'s design makes it easy and efficient for the sending party to
specify how much fee to pay, however it is theoretically possible for a
merchant to pay the mining fees on behalf of their customers as an
incentive to use their service. Services that make this possible have
been proposed.

When a Miner creates a [[Getminingcandidate|block template]]they are
entitled to specify where the fees paid by the transactions in that
block proposal should be sent. If the proposal results in a valid block
that becomes a part of the [[Blockchain|Blockchain]]the full block reward including the transaction fees and the [[Block subsidy|block subsidy]]will be sent to the
specified recipient. Miners are forced to wait 100 blocks before they
can use coins received in a [[Coinbase|Coinbase]]transaction.

# Loss of fees

If a valid block awards its finder less than the available fees plus the
[[Block subsidy|Block subsidy]]the
[[Satoshis|Satoshis]]which are not collected are
permanently destroyed. This has happened on more than 1,000 occasions in
Bitcoin\'s history reducing the token supply by over 50 Bitcoins.

An example of this can be seen in [block
164246](https://whatsonchain.com/block-height/164246)where the Miner lost 1.76 Bitcoins by not claiming the
fees.

# The Bitcoin Fee Market

A default minimum fee is usually needed for a transaction to be
propagated across the network and mined into a block however a market
has arisen offering discounted transactions for bulk generators. The
upcoming [[Merchant_API|Merchant API]](mAPI) package
will give Miners a means by which to interface with regular users and to
offer their own unique pricing on a per-node basis. User wallets will be
able to make use of this service to present users with fee rates that
present estimated \'time to confirmation\' giving them flexibility to
choose lower fees for larger or less important transactions, without
having to worry about those transactions failing to propagate.

[This
article](https://bitcoinsv.io/2019/11/24/on-the-future-of-bitcoin-transaction-fees/)contains a deeper perspective on this aspect of
Bitcoin fees.