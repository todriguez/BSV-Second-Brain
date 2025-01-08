The [[MAPI|mAPI]](formally known as Merchant API) is a new development in Bitcoin, [released](https://bitcoinsv.io/2020/04/03/miner-id-and-merchant-api-beta-release/)in April 2020.

The [[API|API]]enables merchants accepting Bitcoin
transactions to get all of the assurance they need to be able to accept
transactions on a \'zero confirmation\' basis (see
[[Confirmation|Confirmation]]). Merchants are able to
find out in advance (even before broadcasting a transaction) what
transaction fee is required by Miners to mine it.

# Background

As explained by Steve Shadders in [Steve Shadders Discusses the Bitcoin
SV (BSV) Tech Pillars - Bitstocks Podcast Ep.
7](https://youtu.be/WDuvYp77tJU)at 36m 12s
It also allows Miners to put user-based fee policies in place. See [The
dawn of the age of competitive
mining](https://www.yours.org/content/the-dawn-of-the-age-of-competitive-mining-1cc8d831dc34)(Steve Shadders, yours.org, October 2019)
[BRFC (Bitcoin Request for Comment) Specification]

The
[[Bitcoin_Request_For_Comment_(BFRC|BRFC]]"Bitcoin Request For Comment (BFRC)")
specification can be found
[here](https://github.com/bitcoin-sv-specs/brfc-merchantapi).

# Reference Implementation

The reference implementation can be found
[here](https://github.com/bitcoin-sv/merchantapi-reference).