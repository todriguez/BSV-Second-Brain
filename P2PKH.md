A Bitcoin **transaction** consists of a version number, a locktime
value, a list of inputs and a list of outputs.

The primary functionality of a Bitcoin transaction is to transfer
custody of bitcoin from one to another.

A Bitcoin transaction can also serve as a vehicle for smart contracts,
recording data, attestation and many other secondary functionalities.

A transaction can be created and iterated inside a [[Payment Channel|Payment Channel]]using [[./Special:Random|nLocktime and nSequence]]interlocks,
or sent directly to [[The_Bitcoin_Network|The Bitcoin Network]]for inscription
into a [[Block|block]]. A transaction uses [[UTXO|unspent transaction outputs (UTXOs)]]as inputs and distributes
their value to new outputs. UTXOs are the \'coins\' in which all
bitcoins are stored.

Transactions are not encrypted, so it is possible to browse and view
every transaction ever collected into a block. Once transactions have
been seen and validated by a majority of block creating nodes in the
Bitcoin network, they can be considered settled. When they are
eventually mined into a block, miners collaboratively agree on the order
in which they were seen by the network.

Transactions are referenced using their [[TXID|TXID]]which
is a double [[SHA-256|SHA-256]]hash of the fully
serialised transaction.

Transaction outputs are puzzle scripts called ScriptPubKeys which are
typically used to lock the contained bitcoin value, sometimes also
called locking script. Outputs are redeemed by making them inputs to new
transactions and providing a ScriptSig (sometimes called unlocking
script) which is a valid solution that unlocks the bitcoin held in the
ScriptPubKey (locking script). Outputs may have zero value in bitcoin,
but may carry value in another form such as data or tokens. Scripts can
be complex and specialised and may have more than one way to be
redeemed.

All transactions are captured on the ledger in
[[Block|blocks]] on the
[[Blockchain|blockchain]] and can be viewed with a
[[Block_explorer|block explorer]].
This can be useful for seeing the technical details of transactions in
action and for verifying payments.

# General format of a Bitcoin transaction

The following outlines the elements that are serialised to build a valid
Bitcoin transaction.

  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------- -----------------------------------------------------
  Field                                                                    Description                                                                                               Size
  Version no                                                               currently 2                                                                                               4 bytes
  In-counter                                                               positive integer VI = [[VarInt|VarInt]]1 - 9 bytes
  list of inputs                                                           [[Bitcoin Transactions|Input Structure]]\<in-counter\> qty with variable length per input
  Out-counter                                                              positive integer VI = [[VarInt|VarInt]]1 - 9 bytes
  list of outputs                                                          [[Bitcoin Transactions|Output Structure]]\<out-counter\> qty with variable length per output
  [[./Special:Random|nLocktime]]if non-zero and sequence numbers are \< 0xFFFFFFFF: block height or timestamp when transaction is final   4 bytes
  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------- -----------------------------------------------------

# Transaction Inputs and Outputs

Each Bitcoin transaction is comprised of Inputs and Outputs. Inputs
provide the funds to be spent in the transaction, and Outputs define
where those funds should be allocated.

# Inputs

An [[input]] is a reference to an output from a previous transaction,
and a transactions can include between 1 and 2^32^ inputs.

All of the new transaction\'s input value (that is, the total coin value
of the previous outputs referenced by the new transaction\'s inputs) are
added up, and the total (less any
[[Transaction_fees|transaction_fees]]) is
consumed by the outputs of the new transaction.

**Previous tx** is the [[TXID|TXID]] of a previous
transaction.

**Index** is the specific output in the referenced transaction.

**ScriptSig** is the first half of a
[[Opcodes|script]] which is provided when a UTXO is spent as an input to a transaction.

An input ScriptSig may contain many components. To redeem a P2PKH script
the input must provide a public key and an
[[Elliptic_Curve_Digital_Signature_Algorithm|ECDSA]] signature. The Public key is doubled hashed (First
[[SHA-256|SHA-256]] then
[[RIPEMD-160|RIPEMD-160]]) and the resultant hash must
match the hash embedded in the ScriptPubKey of the output being
redeemed.

The public key is then used to verify the redeemer\'s signature.
Dependent on the [[SIGHASH Flags|SIGHASH flags]] used, the signature may cover a hash representing part or all of the
transaction. Combined with the public key, this proves the transaction
was created by a person or process that controls the keys needed to
spend the bitcoin in the input.

# Format of a Transaction Input

Otherwise known as a TXIN, the following table outlines the required
elements of a valid transaction input.

  --------------------------- --------------------------------------------------------------------------------------------- ---------------------------------
  Field                       Description                                                                                   Size
  Previous Transaction hash   [[TXID|TXID]] of the transaction the output was created in                         32 bytes
  Previous Txout-index        Index of the output (Non negative integer)                                                    4 bytes
  Txin-script length          Non negative integer VI = [[VarInt|VarInt]]1 - 9 bytes
  Txin-script / scriptSig     [[Opcodes|Script]]\<in-script length\>-many bytes
  Sequence_no                 Used to iterate inputs inside a payment channel. Input is final when nSequence = 0xFFFFFFFF   4 bytes
  --------------------------- --------------------------------------------------------------------------------------------- ---------------------------------

The input sufficiently describes where and how to get the bitcoin amount
to be redeemed. If it is the (only) input of the first transaction of a
block, it is called the [[Coinbase|Coinbase]]message and
includes information about which block it was mined in and a miner
configurable data element.

# Outputs

An **output** contains a piece of [[Opcodes|Bitcoin Script]]which can be used to lock bitcoins, requiring a certain set of keys or
information to be provided to unlock them. Outputs can also be used to
inscribe data onto the ledger.

This **ScriptPubKey** is the second half of a full script and is only
completed when the output is spent. There can be more than one output,
and they share the combined value of the inputs. The **Value** of each
output is the number of Satoshis that the script unlocks when solved.
Because each output from one transaction can only ever be referenced
once by an input of a subsequent transaction, the entire value of the
combined inputs needs to be allocated to the transaction outputs. Any
[[Satoshis|Satoshis]]left unallocated are considered to
be paid in mining fees and are awarded to the miner whose node generates
the block that the transaction is included in.

If a user\'s input is larger than the value they want to send, the
transaction must create at least two outputs, one sending the required
funds to the destination, and one sending the
[[Change|change]]back to the user.

Outputs can have a value of zero satoshis. Currently, these outputs are
limited to [[False_Return|False Return]]scripts and
are typically used to carry other information or tokens for [[Application_layer_protocol|Application layer
protocols]].

# Format of a Transaction Output

Otherwise known as a TXOUT, the following table outlines the required
elements of a valid transaction output.

  ----------------------------- -------------------------------------------------------------------------------------------------- -------------------------------------------------
  Field                         Description                                                                                        Size
  value                         non negative integer giving the number of [[Satoshis|Satoshis]]to be transferred   8 bytes
  Txout-script length           non negative integer                                                                               1 - 9 bytes VI = [[VarInt|VarInt]]Txout-script / scriptPubKey   [[Opcodes|Script]]\<out-script length\>-many bytes
  ----------------------------- -------------------------------------------------------------------------------------------------- -------------------------------------------------

The output\'s scriptPubKey sets the conditions to release this bitcoin
amount later. The sum of the output values of the first transaction is
the value of the mined bitcoins for the block plus possible transactions
fees of the other transactions in the block.

# Transaction Validation

To verify that inputs are authorized to collect the values of referenced
outputs, Bitcoin uses a
[Forth](https://en.wikipedia.org/wiki/Forth_(programming_language)"wikipedia:Forth (programming language)")-like
[[Advanced_Bitcoin_Scripting|scripting]]system. The input\'s scriptSig and the referenced output\'s scriptPubKey
are evaluated (in that order), with scriptPubKey using the values left
on the stack by the scriptSig. The input is authorized if scriptPubKey
returns true. Through the scripting system, the sender can create very
complex conditions that must be met in order to claim the output\'s
value.

For example, it\'s possible to create an output that can be claimed by
anyone without any authorization. It\'s also possible to require that an
input be signed by ten different keys or be redeemable with a password
instead of a key.

# Puzzles and Solutions

The flexible scripting language enabled by the Bitcoin protocol allows a
multitude of different transaction types to be created. Each
scriptSig/scriptPubKey pair is validated by the network miners and mined
into a block if the script returns true. Some commonly used Bitcoin
puzzle types are described below[Pay to Public Key (P2PK)]

scriptPubKey: \<pubKey\> OP_CHECKSIG scriptSig: \<sig\>

When redeeming coins that have been sent to a Bitcoin public key the
script validates that the provided signature was generated by the
private key that also corresponds to the public key.

Checking process
  -------------------- -------------------------------- ------------------------------------------
  Stack                Script                           Description
  Empty.               \<sig\> \<pubKey\> OP_CHECKSIG   scriptSig and scriptPubKey are combined.
  \<sig\>              \<pubKey\> OP_CHECKSIG           Signature is added to the stack.
  \<sig\> \<pubKey\>   OP_CHECKSIG                      Pubkey is added to stack.
  true                 Empty.                           Signature is checked.
  -------------------- -------------------------------- ------------------------------------------
[Pay to Public Key Hash (P2PKH)]

    scriptPubKey: OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
    scriptSig: <sig> <pubKey>

A [[Address|Bitcoin address]]is only a
hash, so the sender can\'t provide a full public key in scriptPubKey.
When redeeming coins that have been sent to a Bitcoin address, the
recipient provides both the signature and the public key. The script
verifies that the provided public key does hash to the hash in
scriptPubKey, and then it also checks the signature against the public
key.

Checking process
  ------------------------------------------------ -------------------------------------------------------------------------------- ------------------------------------------------------
  Stack                                            Script                                                                           Description
  Empty.                                           \<sig\> \<pubKey\> OP_DUP OP_HASH160 \<pubKeyHash\> OP_EQUALVERIFY OP_CHECKSIG   scriptSig and scriptPubKey are combined.
  \<sig\> \<pubKey\>                               OP_DUP OP_HASH160 \<pubKeyHash\> OP_EQUALVERIFY OP_CHECKSIG                      Constants are added to the stack.
  \<sig\> \<pubKey\> \<pubKey\>                    OP_HASH160 \<pubKeyHash\> OP_EQUALVERIFY OP_CHECKSIG                             Top stack item is duplicated.
  \<sig\> \<pubKey\> \<pubHashA\>                  \<pubKeyHash\> OP_EQUALVERIFY OP_CHECKSIG                                        Top stack item is hashed.
  \<sig\> \<pubKey\> \<pubHashA\> \<pubKeyHash\>   OP_EQUALVERIFY OP_CHECKSIG                                                       Constant added.
  \<sig\> \<pubKey\>                               OP_CHECKSIG                                                                      Equality is checked between the top two stack items.
  true                                             Empty.                                                                           Signature is checked for top two stack items.
  ------------------------------------------------ -------------------------------------------------------------------------------- ------------------------------------------------------
[Pay to R-Puzzle Hash (P2RPH)]

**NOTE:** Since the discovery of a [[R-Puzzles|transaction malleation exploit]]which allows
a message hash and signature to be modified to redirect R-Puzzle inputs
to modified outputs, the advised method for using R-Puzzles is to
include two signatures generating using different SIGHASH types in order
to create a distinct message hash. Take care to generate each signature
with a different **k** value.

scriptPubKey: **OP_OVER OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP
OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK
OP_CHECKSIGVERIFY OP_CHECKSIG** scriptSig: **\<sig\'\> \<sig\>
\<pubKey\>**

Bitcoins locked in an [[R-Puzzles|R-Puzzle]]script
require the spending party to sign using a known value for
\'[[R-Puzzles|k]]\' rather than a random number. To
redeem the script, the spending party provides both the signature and
the public key.

The script verifies that the provided signature was signed using the
correct k-value, then checks the signature against the public key.
Because the public key is not checked as part of the script solution, it
is possible to sign the transaction using any keypair.

This can be useful when dealing with tokens that are associated with a
Bitcoin address as the pubkey that corresponds to that address can be
used to sign the transaction without the requirement for there to be
bitcoin in the address. The technique is also relevant for Metanet node
signing as the Metanet keys can be signed with an R-Puzzle without
needing a separate signature.

Checking process
  ----------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------
  Stack                                                 Script                                                                                                                                                                       Description
  Empty.                                                \<sig\'\> \<sig\> \<pubKey\> OP_OVER OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG   scriptSig and scriptPubKey are combined.
  \<sig\'\> \<sig\> \<pubKey\>                          OP_OVER OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                Constants are added to the stack.
  \<sig\'\> \<sig\> \<pubKey\> \<sig\>                  OP_3 OP_SPLIT OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                        Second from top stack item is duplicated.
  \<sig\'\> \<sig\> \<pubKey\> \<3 bytes\> \<sig\'\>    OP_NIP OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                      First 3 bytes of signature are split
  \<sig\'\> \<sig\> \<pubKey\> \<sig\'\>                OP_1 OP_SPLIT OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                             3 byte data item is removed
  \<sig\'\> \<sig\> \<pubKey\> \<R Length\> \<sig\"\>   OP_SWAP OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                           1 byte containing R length is split from sig\'
  \<sig\'\> \<sig\> \<pubKey\> \<sig\"\> \<R Length\>   OP_SPLIT OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                   R Length parameter is moved to top of stack
  \<sig\'\> \<sig\> \<pubKey\> \<R\> \<sig\'\"\>        OP_DROP OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                            R is split from sig\"
  \<sig\'\> \<sig\> \<pubKey\> \<R\>                    OP_HASH160 \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                                    sig\'\"== is dropped from stack
  \<sig\'\> \<sig\> \<pubKey\> \<rHashA\>               \<rHash\> OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                                               R is double hashed (SHA256 followed by RIPEMD160) and result left on stack
  \<sig\'\> \<sig\> \<pubKey\> \<rHashA\> \<rHash\>     OP_EQUALVERIFY OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                                                         Previously defined R-Hash is pushed onto stack
  \<sig\'\> \<sig\> \<pubKey\>                          OP_TUCK OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                                                                        Script checks if rHashA = rHash
  \<sig\'\> \<pubKey\> \<sig\> \<pubKey\>               OP_CHECKSIGVERIFY OP_CHECKSIG                                                                                                                                                Pubkey is tucked behind \<sig\>
  \<sig\'\> \<pubKey\>                                  OP_CHECKSIG                                                                                                                                                                  Script checks \<sig\> against \<pubKey\>
  true                                                  Empty.                                                                                                                                                                       \<sig\'\> is checked against \<pubKey\>
  ----------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------
[Pay to Multi Signature (P2MS)]

    scriptPubKey: OP_3 <pubKey1> <pubKey2> <pubKey3> <pubKey4> <pubKey5> OP_5 OP_CHECKMULTISIG
    scriptSig: OP_1 <sig1> <sig2> <sig4> 

OP_CHECKMULTISIG offers users the capability to lock coins with a
requirement for multiple parties to sign the scriptSig before coins can
be spent. OP_CHECKMULTISIG can check many signatures against many public
keys as long as the signatures in the scriptSig are provided in an order
that corresponds to the order in which the public keys are arrayed on
the stack when it is executed. The first opcode in the ScriptPubKey
defines how many signatures must be provided in order for the coin to be
successfully spent. The last one before OP_CHECKMULTISIG indicates to
the scripting engine how many public keys to evaluate those signatures
against. There must be at least as many items on the stack as are
required for the OP_CHECKMULTISIG opcode to process or the script will
be invalid.

**Note:** The current version of the scripting engine also includes a
bug that requires an additional value to be placed on the stack before
the signatures. In this example, OP_1 has been used to push a 1 to the
top of the stack, but in theory any piece of data can be used. This
value is consumed by the checking process but is not evaluated.

Checking process
  ---------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------ -----------------------------------------------------
  Stack                                                                                          Script                                                                                                                   Description
  Empty.                                                                                         OP_1 \<sig1\> \<sig2\> \<sig4\> OP_3 \<pubKey1\> \<pubKey2\> \<pubKey3\> \<pubKey4\> \<pubKey5\> OP_5 OP_CHECKMULTISIG   scriptSig and scriptPubKey are combined.
  1 \<sig1\> \<sig2\> \<sig4\>                                                                   OP_3 \<pubKey1\> \<pubKey2\> \<pubKey3\> \<pubKey4\> \<pubKey5\> OP_5 OP_CHECKMULTISIG                                   Constants from scriptSig are added to the stack.
  1 \<sig1\> \<sig2\> \<sig4\> 3 \<pubKey1\> \<pubKey2\> \<pubKey3\> \<pubKey4\> \<pubKey5\> 5   OP_CHECKMULTISIG                                                                                                         Constants from scriptPubKey are added to the stack.
  true                                                                                           Empty.                                                                                                                   Multisignature script evaluation is performed
  ---------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------ -----------------------------------------------------

# Other Puzzle Types

Bitcoin\'s scripting language is rich and diverse and allows a user to
create almost any kind of financial instrument that we have today, and
many that we don\'t have. Puzzles do not need to conform to any
particular standard or template however it is expected that the vast
majority of transactions will be built using template scripts.

Examples of more complex script can be found
[[Complex_Script_Examples|here]]Pieces of script can be combined to make larger and more complex
transactions, and scripts can be built inside conditional loops allowing
a single transaction output to be redeemed in multiple different ways.

Prior to the Genesis upgrade, complex scripts that fell outside the
\'isstandard\' testing schema were required to be compressed into a
transaction format called \'[[P2SH|Pay to Script Hash (P2SH)]]\' This format is now deprecated in favour of
using the full, rich scripting language inside transactions.

# See Also

-   [[Opcodes|Opcodes used in Bitcoin Script]]-   [[Protocol|Protocol rules - \"tx\" messages]]-   [[Protocol|Protocol documentation - Transaction Verification]]-   [[Transaction_Malleability|Transaction Malleability]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Transaction](https://en.bitcoin.it/wiki/Transaction)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated we acknowledge the original authors.