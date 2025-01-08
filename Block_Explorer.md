A Block Explorer is an application that allows users to view and query
data stored on the BitcoinSV ledger and network. Typically accessed
through a web browser, Block Explorers allow users to view details of
Bitcoin
[blocks](https://wiki.bitcoinsv.io/index.php/Block) [transactions](https://wiki.bitcoinsv.io/index.php/Transactions)and
[addresses](https://wiki.bitcoinsv.io/index.php/Address).
Their primary function is to allow users to track network activity in
real-time.

# Structure

The structure of a typical Block Explorer is to have a mining client
with a front end that pulls data from its own copy of the
[blockchain](https://wiki.bitcoinsv.io/index.php/Blockchain)and presents it to users through a web interface.

In future it is expected that Block Explorers will develop their own
tooling and client that can detect additional information that is not
typically monitored by a mining client such as the emergence of a block
race, transactions which the node is not set up to validate and more.

Real time information on both blocks and transactions is typically
provided in addition to other information such as the history of a given
Bitcoin address or a list of transactions containing particular
[metadata](https://wiki.bitcoinsv.io/index.php/Metadata).

# Block information

The explorer provides data on all blocks that have been added to the
ledger, and are usually updated within seconds of a valid block being
discovered. This data shows
-   **Block height:** Number of blocks since the Bitcoin [Genesis
    block](https://wiki.bitcoinsv.io/index.php/Genesis_block)was mined
-   **Age:** Elapsed time between now and the timestamp that indicates
    when the block was discovered
-   **Transaction Count:** number of transactions included in the block
-   **Fees:** Aggregate value of all [Transaction
    fees](https://wiki.bitcoinsv.io/index.php/Transaction_fees)paid to the Miner by users
-   **Reward:** Total Miner reward including transaction fees and [block
    subsidy](https://wiki.bitcoinsv.io/index.php/Block_subsidy)-   **Mined by:** Identity of the Miner or mining pool whose node mined
    this block
-   **Size:** Size of the block as obtained by adding the sizes of each
    transactions included in the block

# Real time Transaction information

In addition, the Block Explorer provides a full set of information
regarding transactions that have either been mined into a block, or
accepted into the Block Explorer\'s node client\'s mempool.

-   **[Block](https://wiki.bitcoinsv.io/index.php/Block)**
    The hash of the block in which the transaction was mined (if the
    transaction has not yet been mined, the confirmation field is
    typically not shown)
-   **Status:** If a transaction isn\'t mined, this field may show the
    transaction as **Unconfirmed**
-   **[Timestamp](https://wiki.bitcoinsv.io/index.php/Block_timestamp)**
    The timestamp in the block header in which this transaction was
    mined (if the transaction has not yet been mined, the timestamp
    field is typically not shown)
-   **Version:** The version of the protocol against which this
    transaction is to be validated
-   **Size:** The size of the serialised transaction in bytes
-   **[Confirmations](https://wiki.bitcoinsv.io/index.php/Confirmation)**
    The number of blocks mined on top of the block containing the
    transaction (if the transaction has not yet been mined, the
    confirmation field is typically not shown)
-   **[Fee
    Paid](https://wiki.bitcoinsv.io/index.php/Transaction_fees)**
    The total transaction fee paid by the spending party
-   **Fee Rate:** The transaction fees paid by the spending party as a
    ratio of Satoshis/Byte which is the total fee paid divided by the
    size of the transaction
-   **[Coinbase
    data](https://wiki.bitcoinsv.io/index.php/Coinbase)**
    If the transaction is the coinbase transaction of a block, the
    explorer will typically show the coinbase text that the Miner has
    embedded in the transaction

In addition to these fields, the explorer will usually include other
information about the transaction including the number of inputs and
outputs, the values of those inputs and outputs, the scripts used to
spend the inputs, and the new scripts created in the outputs. Most
explorers will also offer the user different ways to view this
information such as raw hex, interpreted Bitcoin script or in
[JSON](https://en.wikipedia.org/wiki/JSON "wikipedia:JSON")format.

# Searchable Information

The main function of Block Explorers is to allow users to search for
data in the Bitcoin ledger and
[blockchain](https://wiki.bitcoinsv.io/index.php/Blockchain).
This is typically performed using a search tool.

Typical search functions include
-   Transaction hash or
    [TXID](https://wiki.bitcoinsv.io/index.php/TXID)-   Block height
-   Block hash
-   [Bitcoin
    address](https://wiki.bitcoinsv.io/index.php/Bitcoin_address)-   Transaction metadata

Typically, the explorer responds to a search with a page containing all
the details about the subject of a search request.

# List of BitcoinSV explorers

-   [https://whatsonchain.com](https://whatsonchain.com)-   [https://bitcoinblocks.live](https://bitcoinblocks.live)-   [https://blockchair.com](https://blockchair.com)-   [https://coin.dance](https://coin.dance)# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Block_chain_browser](https://en.bitcoin.it/wiki/Block_chain_browser)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.