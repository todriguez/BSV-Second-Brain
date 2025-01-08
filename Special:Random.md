nLocktime and nSequence are interlocks that can be applied to [[Bitcoin Transactions|Bitcoin Transactions]].

# nSequence

**nSequence** is a parameter applied to each
[[Bitcoin Transactions|input]]of a
transaction. If a transaction\'s nLocktime interlock is active (i.e.
nLocktime is set to a point in the future), a transaction which has one
or more inputs where nSequence is less than UINT_MAX (0xFFFFFFFF), then
the transaction cannot be accepted into a [[Block|block]].

# nLocktime

**nLockTime** is a parameter applied to each transaction specified in
either unix time or block height, before which, the transaction cannot
be accepted into a block. If all inputs in a transaction have nSequence
equal to UINT_MAX, then nLockTime is ignored.

If nLockTime \< 500,000,000, the integer is interpreted as the block
height after which this transaction can be accepted. Otherwise the
integer is interpreted as the UNIX timestamp after which this
transaction can be included in a block.

The [Unix
Timestamp](https://en.wikipedia.org/wiki/Unix_Timestamp "wikipedia:Unix Timestamp")is the number of seconds that have elapsed since the Unix epoch, which
began at 00:00:00 UTC on 1 January 1970, minus leap seconds. Leap
seconds are ignored, with a leap second having the same Unix time as the
second before it. Every day is treated as if it contains exactly 86400
seconds. Due to this treatment, Unix time is not a true representation
of UTC.

# Use in Payment Channels

In transactions where nLockTime is set in the future, and one or more
inputs have nSequence number fields less than 0xFFFFFFFF they are
considered non-final and may be held in a [[Transaction_Pools|transaction pool]]until either nLockTime
expires or all inputs have their nSequence finalised.

Non-final transactions are replaceable with transactions that include
the same inputs with a higher nSequence number. This function can be
used to build payment channels allowing dynamic exchange of data between
parties in a peer to peer manner.