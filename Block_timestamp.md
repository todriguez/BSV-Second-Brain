Each block contains a [Unix
time](https://en.wikipedia.org/wiki/Unix_time) timestamp. In addition to serving as a source of
variation for the [[Block_hashing_algorithm|block hash]]these
timestamps serve as proof of existence for the information stored in the
transactions that the block validates.

A timestamp is accepted as valid if it is greater than the median
timestamp of previous 11 blocks, and less than the network-adjusted
time + 2 hours. \"Network-adjusted time\" is the median of the
timestamps returned by all nodes connected to you. As a result, block
timestamps are not exactly accurate, and they do not need to be. Block
times are accurate only to within an hour or two.

Whenever a node connects to another node, it gets a UTC timestamp from
it, and stores its offset from node-local UTC. The network-adjusted time
is then the node-local UTC, plus the median offset from all connected
nodes. Network time is never adjusted more than 70 minutes from local
system time, however.

Bitcoin uses an unsigned integer for the timestamp, so the [year 2038
problem](https://en.wikipedia.org/wiki/Year_2038_problem "wikipedia:Year 2038 problem")is delayed for another 68 years.

# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Block_timestamp](https://en.bitcoin.it/wiki/Block_timestamp)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.