Genesis was a major update to the BitcoinSV mining client used by the
majority of Miners on the BitcoinSV network at the time. Genesis went
into effect at block height
[620538](https://whatsonchain.com/block-height/620538)which was mined with a timestamp of 01:35:06 UTC on the
4th of February 2020.

The upgrade restored many aspects of the Bitcoin protocol that had been
modified in previous software updates including the removal of most
limit based consensus rules, replacing them with Miner configurable
settings that give node operators the autonomy needed to set their own
limits as they determine are practical.

The upgrade was locked in when [this
transaction](https://whatsonchain.com/tx/4ec3b63d764558303eda720e8e51f69bbcfe81376075657313fb587306f8a9b0)was mined at block height 620539. The transaction
uses a script that would previously have been considered to violate the
protocol rules and rejected by network nodes running the BitcoinSV node
client.

Further details on the changes made in the upgrade can be found
[here](https://bitcoinsv.io/2020/01/15/changes-for-the-genesis-upgrade/)and the full specification is available [here](https://github.com/bitcoin-sv-specs/protocol/blob/master/updates/genesis-spec.md).

# Block Consensus Rules

These consensus rules apply to blocks that are produced after Genesis
activation.

-   [[Block_Size_Rule|Block Size Rule]]- The
    consensus rule that restricts the maximum size of a block to a
    specific number of bytes has been converted into a configurable
    consensus rule. The size of a block is the size in bytes of the
    serialised form of the block including the block header and all of
    the transactions confirmed by the block. MINERS ARE EXPECTED TO
    REACH CONSENSUS ON THIS VALUE AND CONFIGURE IT MANUALLY.

<!-- -->

-   Number of CheckSig Operations per MB of Block Space - The consensus
    rule that limits the number of checksig operations per megabyte of
    block space has been removed.

# Transaction Consensus Rules

These consensus rules apply to transactions that are confirmed in blocks
after Genesis activation.

-   Maximum Transaction Size - The size of a transaction is the size in
    bytes of the serialised form of the transaction. The maximum size of
    a transaction is 1GB (1,000,000,000 bytes). This limitation is
    expected to be lifted in the future.

<!-- -->

-   Maximum Number of CheckSig Operations per Transaction - The
    consensus rule that limits the number of checksig operations per
    transaction has been removed.

<!-- -->

-   nLockTime and nSequence - After Genesis activation, the
    functionality of the nLockTime field of a transaction and the
    nSequence fields of transaction inputs revert to their original
    purpose. The rules defined here only apply to transactions that are
    confirmed after Genesis activation.

# Script Language Rules

This section contains changes to the Script Language Rules. Bitcoin
Script is the programming language that is used to lock and unlock
transaction outputs. More can be found at: [[Advanced_Bitcoin_Scripting|Advanced Bitcoin Scripting]]. The rules defined here apply to locking and unlocking
scripts for transaction outputs that are created after the Genesis
activation. The previous rules apply to transaction outputs created
prior to Genesis activation.

# OP_RETURN Functionality

The functionality of the OP_RETURN operation is being restored.
OP_RETURN will cause termination of the script and the validity of the
script is determined by the value of the top item on the stack. See
[[OP_RETURN|OP_RETURN]].

# Data Types

All data items in Bitcoin Script are a byte sequence. Some operations
interpret their parameters as numeric or boolean values and require the
item to fulfill the requirements of those types. Some operations produce
items on the stack which are valid numeric or boolean values.

# Bitcoin Script Formal Grammar

Formal grammar has been defined for Bitcoin Script. More can be found
at: [[Opcodes|Opcodes used in Bitcoin Scripting]].

-   Validity of Script Consensus Rule - The locking and unlocking
    scripts for every input of a transaction must be grammatically
    valid, as defined by the formal grammar above.

<!-- -->

-   PUSHDATA Only in Unlocking Script Consensus Rule - After Genesis
    activation, the unlocking scripts used in transaction inputs may
    only contain PUSHDATA operations, as defined by the formal grammar.
    In contrast to all the other updates in this section, this consensus
    rule is activated for all inputs of transactions that are, or will
    be, confirmed in a block after Genesis activation, regardless of the
    height of the UTXO being spent. This rule is a subset of the
    Validity of Script Consensus Rule defined above but is included
    separately because the activation conditions are different.

# Consensus Rule Replacement

Functionality provided by these consensus rules is now covered by the
Stack Memory Usage Consensus Rule.

  ------------------------------------------ -------------------------------------------------------------------------------------------------------
  Consensus Rule                             Description
  Script Element Size                        Limits the maximum size of a script element.
  Stack Size                                 Limits the combined number of elements that can be placed on the stack and the altstack.
  Script Size\*                              The maximum size of the script
  Number of Non-Push Operations per Script   Limits the number of non-push operations per script. Other capabilities manage the cost of execution.
  ------------------------------------------ -------------------------------------------------------------------------------------------------------

-   functionality also covered by the Maximum Transaction Size Consensus
    Rule.

# Consensus Rule Changes

  -------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Consensus Rule                                                       Description
  [[Numeric_Value_Size|Numeric Value Size]]For a byte sequence to represent validly a numeric value, the length of the byte sequence must be less than or equal to 750,000 bytes. A byte sequence that is larger than this is a valid byte sequence but is not a valid numeric value.
  Number of Public Keys per Multisig Consensus Rule                    Limits the number of public keys per multisig has been changed to be 2\^31-1 (INT32_MAX).
  Stack Memory Usage                                                   Limits the amount of memory that can be used on the stacks. This rule is evaluated against the sum of the memory used by the stack and the memory used by the altstack.
  -------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Sunsetting

-   P2SH, OP_CHECKLOCKTIMEVERIFY, and OP_CHECKSEQUENCEVERIFY - The P2SH
    capability is being removed by the Genesis upgrade and the presence
    of a P2SH script template in an output will invalidate a
    transaction. The opcode operations revert to NOPs, which have no
    effect.

<!-- -->

-   Disabling Operations Consensus Rule - OP_2MUL, OP_2DIV, OP_VERIF,
    OP_VERNOTIF. If they are present in un-executed script, the script
    execution may succeed.

# Standard Local Policies

Policies are settings that are configured by software operators. These
settings are generally required by software implementations.

Policies control which transactions the software will propagate across
the P2P network or include in a block. However, policies are not Bitcoin
Rules or Consensus Rules and are not used to determine the validity of
blocks or the transactions confirmed by the block.

Standard Local Transaction Policies

-   Maximum Acceptable Transaction Size Policy - The maximum acceptable
    transaction size is a standard policy that configures the largest
    transactions that the software will propagate across the P2P network
    or include in a block.
-   Transaction Evaluation Timeout - The transaction evaluation timeout
    is a standard policy that defines the maximum amount of time that
    the software will allow for the evaluation of a transaction, before
    terminating the evaluation and rejecting the it. This setting is
    always defined with a time unit and the default value 1 second.

Standard Local Script Language Policies

-   Numeric Value Length - the length of numeric value policy defines
    the maximum length of a byte sequence to be considered a valid
    numeric value. The default value for this value is 250,000 bytes.
-   Stack Memory Usage - The stack memory usage policy limits the amount
    of memory that can be used on the stacks. This policy is evaluated
    against the sum of memory used by the stack and the altstack.

Standard Local P2P Network Policies

-   Propagation of non-Standard Transactions - After Genesis activation,
    the default setting for this policy is that non-standard
    transactions will be propagated across the P2P network. Before
    Genesis activation, the default setting for this policy was
    non-standard transactions were not propagated by the P2P Network.
    Policies such as Maximum Acceptable Transaction Size Policy still
    apply.