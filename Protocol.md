# Bitcoin Protocol Rules

The rules of the Bitcoin protocol are the rules that precisely define
the Bitcoin system.

There are different classes of rule in the Bitcoin system including
-   [[Immutable|Immutable]]rules
-   Mutable rules
    -   Local Policies
    -   Standard Policies
-   Communication rules

# Immutable Rules

The [[Immutable|immutable]]rules are codified into
Bitcoin node clients and must be strictly adhered to, in order to
implement the Bitcoin specification in software \[1\]. They are a set of
rules that define the format and constraints that transactions and
blocks must follow.

These include
-   The sum of the value of the inputs of a transaction must be greater
    than or equal to the sum of the values of the outputs.
-   The [[Block subsidy|block subsidy]]will drop by
    half at a scheduled rate of every 210,000 blocks, starting with a
    subsidy of 5,000,000,000 [[Satoshis|satoshis]]per
    block from the genesis block.
-   The network will adjust the [[Target|target]]for the
    [[Difficulty|difficulty]]of the [[Proof of Work|Proof of Work]]needed for a valid block
    to maintain an approximate 10 minute block discovery rate.
-   Only blocks that add to the
    [[Blockchain|blockchain]]formed by building upon
    the [[Genesis_block|Genesis block]]are valid.
-   The structure of the Bitcoin database as a timestamp server
    validating chains of transaction outputs.
-   Transaction data formatting, including sizes of certain fields and
    their encoding schema.
-   Block structure and header information including sizes of certain
    fields and their encoding schema.
-   The [[Advanced_Bitcoin_Scripting|Bitcoin scripting language]]and its specification including
    -   Lists of opcodes that are usable in script and the exact outcome
        of their execution

Forced changes to these protocol rules in the past have resulted in
duplications of the Bitcoin database. In doing so, creating BTC which
implemented \'Segregated Witness\', removing the requirement for Bitcoin
to be a chain of digital signatures. BCH enforced a transaction ordering
schema onto the timestamping function of the system, and modified the
scripting language to add op codes, with functionality outside the scope
of the original design.

The Bitcoin SV philosophy is, where aspects of these rules have been
changed in the past, they should be returned to be as close to the
original rules as possible and then "set in stone". Only changes needed
to protect the security of the network such as, the migration to a new
hash function should SHA256 be broken, will be allowed, with this rule
being enforced through [[Nakamoto_Consensus|Nakamoto Consensus]].

# Mutable Rules

Mutable rules are consensus rules that mining clients implement but
which are not hard coded into the BitcoinSV node client. Miners can
change these at any time provided there is enough agreement among Miners
to do so under [[Nakamoto_Consensus|Nakamoto Consensus]]. Miners who do
not maintain these settings in-line with the rest of the network, risk
having their blocks invalidated. Examples of these include
-   The maximum script memory usage rule which governs how much memory a
    transaction can consume during the execution of its script.
-   The maximum block-size rule.
-   Transaction script rules such as the rule preventing the use of
    opcodes other than pushdata in ScriptSig.

It is important to note that these rules can be violated in special
cases by Miners, through a negotiation process that ends with a
transaction or block that violates these rules being accepted and built
upon. This can only be achieved through Nakamoto consensus. No examples
of this happening have yet been encountered.

When modifying these rules, Miners tend to act as a collective, changing
a particular rule all at once (e.g. maximum transaction memory limits
and maximum block size). Since the [[Genesis_upgrade|Genesis upgrade]]these changes no
longer require hard forks or scheduled network upgrades, and the
settings that govern these changes available to Miners through node
client configuration tools. All that is required is a loose agreement
between Miners to change the settings across the network at a particular
date and time.

This means that Miners must be aware of the actions being taken by the
rest of the network, lest they find themselves rejecting transactions or
blocks that a majority of the network is accepting and become stuck on a
non-productive chain-tip while the remainder of the network move
forward.

# Local rules

These rules are "local" by definition. They apply to the instance of
software that is running, they do not apply to the validation of blocks,
or the transactions within a block. A block accepted from another Miner
may contain transactions that do not conform to local rules. Local rules
include
-   The "minimum fee" rule, which specifies that the node will only
    accept and/or relay unconfirmed transactions that pay above a
    certain fee.
-   Dust rules which specify the smallest value output a transaction can
    contain that the node will accept and/or relay.
-   Rules relating to inbound and outbound connections on the network,
    such as RPC responses, specific IP addresses to connect to, and
    more.

# Standard Policies

Standard policies are local rules that are used by a significant
proportion of network nodes. They are defined as a \"Standard\" to
facilitate common application across independent software
implementations, but it is important to note that, it is not required
that software implement or adhere to these policies.

Bitcoin users who transact within the guidelines of standard policy will
face the least issues with their transactions on the network. Some
Miners can enact local rules outside of the standard policies however
this can cause issues for the Miner, who may be attempting to mine
blocks that carry large numbers of transactions which other Miners have
rejected. This can lead to [[Orphan_Block|orphan blocks]]due to slow propagation.

# Communication Rules

The communication rules govern how transaction and block data is
propagated across the Bitcoin network. Commonly referred to as the
Bitcoin [[Peer-To-Peer_Protocol|Peer-To-Peer (P2P) Protocol]]this
current version is well defined method and used by the majority of
Bitcoin nodes in the network to communicate. The P2P Protocol can be
changed and there are plans among Miners to modify the implementation in
future. It is conceivable that at a certain point, several different
inter-node communication protocols may be in-use to propagate block and
transaction information between Miners, and optimising this aspect of
the network is strongly incentivised by the economics of Bitcoin mining.
A large amount of the innovation that scales Bitcoin SV has been and
will, in future, be done by improving the P2P protocol.

# See Also

-   [[The_Bitcoin_Network|The Bitcoin Network]]-   [[Nakamoto_Consensus|Nakamoto Consensus]]-   [[P2P_Network|P2P Network]]# References

\[1\] -
[https://github.com/bitcoin-sv-specs/protocol/blob/master/updates/genesis-spec.md](https://github.com/bitcoin-sv-specs/protocol/blob/master/updates/genesis-spec.md)