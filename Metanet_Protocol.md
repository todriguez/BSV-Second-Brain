[[../images/thumb/8/80//images/Metanet_graph.png/300px-/images/Metanet_graph.png|![]]](./File:/images/Metanet_graph.png.html)

 magnify
[](./File:/images/Metanet_graph.png.html "Enlarge")

The **Metanet Protocol** is a layer-2 overlay protocol that defines a
method for creating data structure over Bitcoin SV. The protocol
utilises [[Metanet_Protocol|nodes and edges]]to specify directed acyclic graph (DAG) data structures on the Bitcoin
SV ledger. The Metanet protocol can be used to construct diverse systems
such as file systems, internet domains, ownership structures and code
repositories.

There are tools available to write and read Metanet graphs, and a
growing range of projects that use the Metanet protocol to structure
their application data.

# Node and Edge Structure

The Metanet Protocol (MNP) is a protocol for creating graph structures
comprising nodes and edges on the ledger. In the Metanet protocol the
following definitions of node and edge are used
-   **Metanet Node** - A transaction using the Metanet protocol format.
-   **Metanet Edge** - An input signature linking two Metanet nodes.

A Metanet node is a transaction that conforms to the Metanet transaction
format specified in [Metanet technical
summary](https://www.bitcoinsv.io/files/metanet.pdf)document produced by nChain. The basic components of a
Metanet transaction include a protocol flag, Metanet-specific data
attributes, and any content data that is to be stored by a Metanet node
transaction.

The protocol flag is a 4-byte
[[Hexadecimal|hexadecimal]]prefix that signifies that
a transaction is using the format of the Metanet protocol. The
hexadecimal value of the prefix was chosen to be the hexademical
encoding 0x4d455441 of the string \'meta\' by [public
poll](https://twitter.com/BitcoinAssn/status/1136232235798016001)on June 5th 2019.

The Metanet-specific data attributes of a Metanet node transaction
include the following
-   **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a582275c5bb6b84f374ebd43d9d17f9605a17281)]** -
    the public key defining the node.
-   **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af086abc8b9e20e79598b7bde02ed2fb518308e5)]** -
    the unique transaction ID of the node.
-   **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e6a5a1121f87209c12105f47b75c51357e67e404)]** -
    the public key defining a parent of the node.
-   **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/846ecfa0eb364067c566285e1c43bd237bc0d188)]** -
    a signature created using the private key associated with the public
    key defining a parent of the node.
-   **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/be9d8bb3483363d3d62d2c047cd909204828ad3d)]** -
    the unique transaction ID of the parent of the node.

The Metanet-specific data attributes listed above are used collectively
to define a Metanet node and its position within a larger graph
structure of multiple Metanet nodes, known as a *Metanet graph*.

It is possible that a node does not have any parents and such a node is
termed a *root node*. A root node will have null values for any
[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e6a5a1121f87209c12105f47b75c51357e67e404)], [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/846ecfa0eb364067c566285e1c43bd237bc0d188)], and [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/be9d8bb3483363d3d62d2c047cd909204828ad3d)]
attributes, and can therefore use a valid signature from any public key
in its input(s).

A Metanet transaction is defined as a transaction that contains an
OP_FALSE OP_RETURN payload containing
-   The Metanet flag

[[../images/thumb/8/8d//images/Metanet_node.png/300px-/images/Metanet_node.png|![]]](./File:/images/Metanet_node.png.html)

 magnify
[](./File:/images/Metanet_node.png.html "Enlarge")

-   A node public key
    **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a582275c5bb6b84f374ebd43d9d17f9605a17281)]**
-   A parent transaction ID
    **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/be9d8bb3483363d3d62d2c047cd909204828ad3d)]** (null if a root node).

In order to qualify as a Metanet-valid node, the transaction must also
be signed by the public key corresponding to its parent
**[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e6a5a1121f87209c12105f47b75c51357e67e404)]**.

Any content data and its encoding can be included following these core
Metanet attributes in the OP_FALSE OP_RETURN payload. The Metanet
protocol does not specify the use of any one scheme for content data and
additional attributes, and any valued usage of the Metanet protocol
attributes above constitute a Metanet node transaction.

A basic example of a Metanet node transaction that conforms to this
format is shown in the diagram on the right.

The Metanet graph is formed by creating edges between parent Metanet
nodes and child Metanet nodes. An edge is created between a parent and
child by the creation and insertion of the signature
**[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/846ecfa0eb364067c566285e1c43bd237bc0d188)]**
in the child node, using the parent public key.

[[../images/thumb/a/a6//images/Metanet_edge.png/300px-/images/Metanet_edge.png|![]]](./File:/images/Metanet_edge.png.html)

 magnify
[](./File:/images/Metanet_edge.png.html "Enlarge")

The fact that this signature is in a transaction input means that the
signature itself may be validated by Miners. This means that attempts to
spoof a Metanet node can be mitigated either by validating the signature
explicitly or by confirming that the node is spending an appropriate
previous output.

# Rules of the Metanet Protocol

The Metanet protocol specifies a simple and extensible rule set for
creating Metanet graphs and data structures. The base rule set is the
following
-   Nodes are transactions.
-   Edges are created by signatures.
-   Each node is uniquely identified by the pair of attributes
    **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a582275c5bb6b84f374ebd43d9d17f9605a17281)]**, **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af086abc8b9e20e79598b7bde02ed2fb518308e5)]**.
-   Each node must specify the node ID of itself and its parent
    **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/336c6b84ffb7eb81857a12ec90c17be78a30dae7)]**, **[[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ada7995575c4070043779d4382ed430a80cd7a3e)]**.

The unique node identifier for a node is defined mathematically as
**[[$||TxID_)}$]![\|\|TxID\_)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c460ed6c7ca582d8c8e73921c459ca76807f5b25)]**,
where **[[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/4926618205c853a718a53fab532f65fd3b14f998|]]]**
is a cryptographic hash function.

Metanet graph structures may be created using this base rule set alone.
It is also possible to impose additional rules to Metanet graph
structures to achieve different properties for data structures.

A simple extension of the rule set is to impose the following
[[Constraint|constraints]][[../images/thumb/7/71//images/Metanet_rules.png/300px-/images/Metanet_rules.png|![]]](./File:/images/Metanet_rules.png.html)

 magnify
[](./File:/images/Metanet_rules.png.html "Enlarge")

-   The
    [in-degree](https://wiki.bitcoinsv.io/index.php "In-degree (page does not exist)") of a node should be 0 (no parent) or 1 (one parent).
-   The [[Out-degree|out-degree]]of a node should be a
    free parameter.

These additional rules allow domain-like structures to emerge as Metanet
DAGs, which can be used to structure websites and file systems which
inherit the permission structure of a Metanet graph.