The Genesis block is the first block in the Bitcoin
[[Blockchain|Blockchain]]and can be found at block
height zero. The hash of the Genesis block is
**[000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f](https://whatsonchain.com/block/000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f)**

The **Genesis block** is the common ancestor of all other blocks. It is
hard wired into the Bitcoin node client software and [cannot be
deleted](https://github.com/bitcoin-sv/bitcoin-sv/blob/master/src/chainparams.cpp)The Genesis block has a timestamp of January 3rd 2009, 18:15:05h UTC.

# Coinbase

The [[Coinbase|coinbase]]parameter contains, along with
the normal data, the following text
> The Times 03/Jan/2009 Chancellor on brink of second bailout for banks

The quote is from the following article from [The Financial
Times](https://web.archive.org/web/20140309004338/http://uk.reuters.com/article/2009/01/03/idUKPTIP32510920090103)(archive.org cached copy)

The article concerns the intervention of The State in banking during
times of crisis and the devaluation of centrally issued currencies in
times of bailout as an incentive for bad actors. [[Satoshi_Nakamoto|Dr Craig Wright]]discusses this topic
in [this
article](https://medium.com/@adam_selene/genesis-c5b4edff6b9c)written under the pseudonym \'Adam Selene\'.

# Timestamp

Although the average time between Bitcoin blocks is 10 minutes, the
timestamp of the next block is a full 6 days after the Genesis block. Dr
Craig Wright has indicated that the delay occurred because a scheduled
patch for Windows was released by Microsoft which caused all of his
computers to shut down at once, and it required several days before he
was able to get it back up and running.

# Raw block data

The [raw hex
version](https://bitcointalk.org/index.php)of the Genesis block looks like
    00000000   01 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00   ................
    00000010   00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00   ................
    00000020   00 00 00 00 3B A3 ED FD  7A 7B 12 B2 7A C7 2C 3E   ....;£íýz

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Genesis_block](https://en.bitcoin.it/wiki/Genesis_block)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.