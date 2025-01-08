A **private key** is a secret number that can be used to transfer
bitcoins, encrypt data and more. Each private key corresponds to a
public key which is a coordinate on the [[Secp256k1|Bitcoin Elliptic Curve]].

Every Bitcoin wallet contains one or more private keys, which are
typically generated from a root key, and which are saved in the wallet
file. Having knowledge of a private key allows any coins that can be
unlocked with that key to be spent, so it is important that these are
kept secret and safe.

Private keys themselves are almost never handled by the user, instead
the user will typically be given a [[Seed_phrase|seed phrase]]from which their wallet\'s root
key can be derived.

# Range of valid ECDSA private keys

Nearly every 256-bit integer is a valid
[[Elliptic_Curve_Digital_Signature_Algorithm|ECDSA]]private key. Specifically, any 256-bit number from 0x1 to 0xFFFF FFFF
FFFF FFFF FFFF FFFF FFFF FFFE BAAE DCE6 AF48 A03B BFD2 5E8C D036 4140 is
a valid private key.

The range of valid private keys is governed by the
[[Secp256k1|secp256k1]]ECDSA standard used by Bitcoin.
[Hierarchical Deterministic (HD) Wallet Keys]

Wallet software may use a [mnemonic
seed](https://github.com/bitcoin/bips/tree/master/bip-0032)to generate many private keys and corresponding
public keys from a single secret value. This is called a *hierarchical
deterministic wallet*, or *HD wallet* for short. The seed value, or
*master extended key*, consists of a 256-bit private key and a 256-bit
*chain code*, for 512 bits in total. The seed value should not be
confused with the private keys used directly to sign Bitcoin
transactions.

Users are strongly advised to use HD wallets, for safety reasons: An HD
wallet only needs to be backed up once, typically using a [[Seed_phrase|seed phrase]]; thereafter in the future, that
single backup can always deterministically regenerate the same private
keys. Therefore, it can safely recover all addresses, and all funds sent
to those addresses. Non-HD wallets generate a new randomly selected
private key for each new address; therefore, if the wallet file is lost
or damaged, the user will irretrievably lose all funds received to
addresses generated after the most recent backup.

# Base58 Wallet Import format

When importing or sweeping ECDSA private keys, a shorter format known as
[[Wallet_import_format|wallet import format]]is often used, which offers a few advantages. The wallet import format
is shorter, and includes built-in error checking codes so that typos can
be automatically detected and/or corrected (which is impossible in hex
format) and type bits indicating how it is intended to be used. Wallet
import format is the most common way to represent private keys in
Bitcoin.

For private keys associated with uncompressed public keys, they are 51
characters and always start with the number 5 on mainnet (9 on testnet).
Private keys associated with compressed public keys are 52 characters
and start with a capital L or K on mainnet (c on testnet). This is the
same private key in (mainnet) wallet import format
\
5Kb8kLf9zgWQnogidDA76MzPL6TsZZY36hWXMssSzNydYXYB9KF

\
When a WIF private key is imported, it always corresponds to exactly one
Bitcoin address. Any utility which performs the conversion can display
the matching Bitcoin address. The mathematical conversion is somewhat
complex and best left to a computer, but it\'s notable that the WIF
guarantees it will always correspond to the same address no matter which
program is used to convert it.

The Bitcoin address implemented using the sample above is
1CC3X2gu58d6wXUWMffpuzN9JAfTUWu4Kj

# Summary

Any Bitcoins sent to the address 1CC3X2gu58d6wXUWMffpuzN9JAfTUWu4Kj can
be spent by anybody who knows the private key implementing it in *any*
of the three formats, regardless of when the bitcoins were sent, unless
the wallet receiving them has since made use of the coins generated. The
private key is only needed to spend the bitcoins, not necessarily to see
the value of them.

If a private key controlling unspent bitcoins is compromised or stolen,
the value can be protected if it is immediately spent to a different
output which is secure. Because bitcoins in an unspent transaction
output can only be spent once, when they are spent using a private key,
the private key becomes worthless. It is often possible, but inadvisable
and insecure, to use the address implemented by the private key more
than once, in which case the same private key would be
[[Address_reuse|reused]].

# See Also

-   [[Paper_wallet|Paper wallet]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Private_key](https://en.bitcoin.it/wiki/Private_key)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.

