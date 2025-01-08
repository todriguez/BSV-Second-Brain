The Bitcoin network is a made up of one (and only one) type of node that
is defined in section 5 of the white paper. These nodes are often
referred to as miners and are characterised by an ability to produce
valid blocks, distribute them to their peers (other nodes), and validate
blocks they receive. Nodes are responsible for upholding the consensus
mechanism of the system based on block publication and proof-of-work.
There is no other definition of a node in the Bitcoin network.

-   A node constructs, distributes and validates blocks

Old nodes may drop off the network and new nodes may join at any time.
There is no hierarchy in the process of block distribution or
validation, making the network truly peer-to-peer. Nodes are
incentivised to maintain a high degree of connectivity with other nodes.
This means that the network topology is that of a nearly complete graph.
At any one time there are typically less than ten nodes that publish the
majority of blocks.

 thumbcaption

An example of the bitcoin network with six nodes. The topology is that
of a nearly complete graph.

Bitcoin nodes also validate and propagate transactions. Transactions
enter the network through users of the system. The users themselves are
outside the Bitcoin network and interact with one or more Bitcoin nodes
through client software.

-   A user interacts with nodes through client software

An example of a user may be a service provider, storage entity,
propagation entity, autonomous agent (smart contract), or a wallet
belonging to a person or business. Note that the users do not play a
role in the production, distribution, or validation of blocks on the
Bitcoin network. Therefore, they are not involved in the consensus
process.

The direct connection between users for the purpose of sending a
transaction does not necessarily mean that they are part of any network.
However, there may exist complex user networks that are separate to the
Bitcoin network. A user may be a node on their own network whilst being
a client on the Bitcoin network. Such networks may be thought of as
being overlaid on top of the Bitcoin network. User networks may be
peer-to-peer or hierarchical in structure, for example service providers
and consumers. These user networks may be layered on top of one another
in such a way that they form a [Bitcoin-Layered
Network](https://wiki.bitcoinsv.io/index.php "Bitcoin Layered Networks (page does not exist)").

There is no requirement for a Bitcoin node to be made up of a single
machine. A node may be made up of several different linked systems
including routing, database and processing modules. However, there is no
such thing as an archival or transaction propagation node on the Bitcoin
network.