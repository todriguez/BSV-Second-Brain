A [[Deterministic|deterministic]]wallet is a system
of deriving keys from a single starting point known as a seed. The seed
allows a user to easily backup and restore a wallet without needing any
other information and can, in some cases, allow the creation of public
addresses without the knowledge of the [[Private Key|private key]]. Seeds are typically serialised
into human-readable words in a [[Seed_phrase|Seed phrase]]. The [BIP
0032](https://github.com/bitcoin/bips/tree/master/bip-0032)standard for hierarchical deterministic wallets is
used by most wallets as of 2019.

# Benefits

Early clients such as the Satoshi client generate a
[[Buffer|buffer]]of fresh random private keys to be used
as receiving and [[Change|change addresses]]in the future.
This has the effect of invalidating backups after a short period when
the keypool [[Buffer|buffer]](typically 100 addresses) is
exhausted. Deterministic wallets can generate as many unique addresses
as are required on the fly and as such don\'t suffer from this issue. As
the addresses are generated in a known fashion, rather than randomly,
some clients can be used on multiple devices without the risk of losing
funds. Users can conveniently create a single backup of the seed in a
human readable format that will last the life of the wallet, without the
worry of this backup becoming stale.

# Master public key

Some deterministic wallets allow for the complete separation of private
and public key creation for greater security and convenience. In this
model a server can be set up to only know the Master Public Key (MPK) of
a particular deterministic wallet. This allows the server to create as
many public keys as is necessary for receiving funds, but a compromise
of the MPK will not allow an attacker to spend from the wallet. They can
alternatively be used to enable completely offline storage and spending.
In this case an offline computer knows the private key and an online one
knows only the MPK. Transactions spending coins are ferried between the
two computers using methods such as visual transfer (QR code) or USB
storage which avoids exposing the offline computer to a network-based
attack.

Deterministic wallets implemented by hardware wallets keep the generated
private keys offline and do not expose them to the computer even when
spending coins.

# Types

# Type 1 deterministic wallet

A type 1 deterministic wallet is a simple method of generating addresses
from a known starting string, as such it does not allow advanced
features such as a Master Public Key. To generate a private key take
SHA256(string + n), where n is an [[ASCII|ASCII]]-coded
number that starts from 1 and increments as additional keys are needed.

# Type 2 hierarchical deterministic wallet

This wallet type is described in [BIP
0032](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)and is the most common wallet type. The seed is a
random value presented to the user as a 12 or 24 word [[Seed_phrase|seed phrase]]using common English words. The
seed goes through 100,000 rounds of SHA256 before any keys are created,
to slow down attacks against weak user-chosen strings.

# Wallets using Diffie Hellman secret sharing

In order to leverage the techniques showcased in [nCrypt whitepaper
42](https://wiki.bitcoinsv.io/index.php "WP0042 (page does not exist)"),
wallets must be configured to manage the handshaking and Elliptic Curve
mathematics needed to support the generation of shared secrets.
Currently, no wallets support this type of deterministic addressing.

# See Also

-   [[Seed_phrase|Seed phrase]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Deterministic_wallet](https://en.bitcoin.it/wiki/Deterministic_wallet)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.