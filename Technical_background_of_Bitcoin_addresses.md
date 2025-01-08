A [[Address|Bitcoin addressis]]based
primarily on the 160-bit hash representation of the public key of an
[ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_DSA "wikipedia:Elliptic Curve DSA")public-private keypair. Using [public-key
cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography")
you can \"sign\" data with your [[Private Key|private key]]and anyone who knows your public
key can verify that the signature is valid.

For the private key of the ECDSA keypair, using applicable public-key
cryptography solutions, one can \"sign\" data (e.g. details of a Bitcoin
SV Transaction) with their [[Private Key|private key]]. Any interested party who knows
the public key can verify that the signature is valid (i.e. the private
key used to generate the digital signature is the unique private key
that corresponds to the public key).

It is highly recommended that a new address is generated for each
instance one is to receive funds.; each new address corresponds to a new
keypair (with HD wallets this is done deterministically). The public
keys and their associated private keys (or the seed needed to generate
them in the case of HD wallets) are stored in the
[wallet](https://wiki.bitcoinsv.io/index.php "Wallets and key management (page does not exist)")
data file. This is the only file users should need to backup.

A \"send\" transaction to a specific BitcoinSV address requires that the
corresponding (receiving) wallet knows the private key implementing that
address. This has the implication that, if using a non-HD wallet, if the
receiving wallet had created an address and coins were sent to that
address, but a restoration of the wallet from an earlier backup becomes
necessary, but the receiving address of interest had not as yet been
generated, then the coins sent to that address are permanently lost.
This is not an issue for HD wallets where all addresses are generated
from a single seed. Addresses are added to an address key pool prior to
being used for receiving coins. Bear in mind however that if you lose
your wallet 'entirely', all of your coins are lost and can never be
recovered.

Bitcoin SV has no restrictions on the number of addresses one may create
or utilise. Not only can one use a new address for every transaction, it
is highly recommended that this be done. There is no \"master address\";
the \"Your Bitcoin address\" area sometimes seen in wallet UIs has no
special importance. Such an inclusion is only there for your
convenience, and it should change automatically when used.

The inclusion of the checksum value in the Bitcoin addresses is to
remove, or at least drastically reduce the possibility of sending
Bitcoins to a mistyped address. However, note that it is entirely
possible that an address is well-formed (valid format, checksum etc.)
but no one owns it (or the owner lost their wallet.dat, private key),
resulting in coins sent to that correctly-formed address being lost
forever.

Along with the prefix, the 160-bit hash of the public key, and the
checksum data are, as a concatenated string, converted to an
alpha-numeric representation using a custom scheme---the [[Base58Check_encoding|Base58Check encoding]]scheme.
Under Base58Check, addresses can contain all alphanumeric characters
except 0, O, I, and l. Bitcoin SV addresses currently always begin with
the prefix 1. Testnet addresses usually start with m or n. Mainline
addresses can be 25-34 characters in length, and Testnet addresses can
be 26-34 characters in length. Most addresses are 33 or 34 characters
long.
[Collisions (lack thereof)]

Given that Bitcoin SV addresses are basically random numbers it is
possible, although extremely unlikely, for two people to independently
generate the same address. This is where the 160-bit hashes of their
respective ECDSA public keys result in the same output. This is called a
[collision](https://en.wikipedia.org/wiki/Collision_(computer_science)"wikipedia:Collision (computer science)").
If this happens, then both the original owner of the address and the
colliding owner could spend the money sent to that address even if the
address hashes had been created using different private keys. Despite
this, it would however not be possible for one of the parties to spend
the other's entire wallet.

Due to the fact that the space of possible addresses is so
astronomically large, it is more likely that the Earth is destroyed in
the next 5 seconds than for a collision occur in the next millennium.

# How to create an Address

While it is theoretically possible to manually create a BitcoinSV
address, the correct or recommended way to create an address is to use
well-tested, open source, peer-reviewed wallet software. Manually
handling keys has historically resulted in loss of funds. This is
particularly problematic given that, unlike centralized systems, losses
in Bitcoin are usually unrecoverable.

For informational purposes, the steps in the generation of a BitcoinSV
from an ECDSA private key are shown
\
0 - Having a private
[[Elliptic_Curve_Digital_Signature_Algorithm|ECDSA]]key

       18e14a7b6a307f426a94f8114701e7c8e774e7f9a47e2c2035db29a206321725

1 - Take the corresponding public key generated with it (33 bytes, 1
byte 0x02 (y-coord is even), and 32 bytes corresponding to X coordinate)

       0250863ad64a87ae8a2fe83c1af1a8403cb53f53e486d8511dad8a04887e5b2352

2 - Perform [[SHA-256|SHA-256]]hashing on the public key

       0b7c28c9b7290c98d7438e70b3d3f7c848fbd7d1dc194ff83f4f7cc9b1378e98

3 - Perform
[[Opcodes|RIPEMD-160]]hashing on the result of SHA-256

       f54a5851e9372b87810a8e60cdd2e7cfd80b6e31

4 - Add version byte in front of RIPEMD-160 hash (0x00 for Main Network)

       00f54a5851e9372b87810a8e60cdd2e7cfd80b6e31

*(note that below steps are the [[Base58Check_encoding|Base58Check encoding]]which has
multiple library options available implementing it)*\
5 - Perform SHA-256 hash on the extended RIPEMD-160 result

       ad3c854da227c7e99c4abfad4ea41d71311160df2e415e713318c70d67c6b41c

6 - Perform SHA-256 hash on the result of the previous SHA-256 hash

       c7f18fe8fcbed6396741e58ad259b5cb16b7fd7f041904147ba1dcffabf747fd

7 - Take the first 4 bytes of the second SHA-256 hash. This is the
address checksum

       c7f18fe8

8 - Add the 4 checksum bytes from stage 7 at the end of extended
RIPEMD-160 hash from stage 4. This is the 25-byte binary Bitcoin
Address.

       00f54a5851e9372b87810a8e60cdd2e7cfd80b6e31c7f18fe8

9 - Convert the result from a byte string into a base58 string using
[[Base58Check_encoding|Base58Check encoding]]. This is the
most commonly used Bitcoin Address format

       1PMycacnJaSqwwJqjawXBErnLsZ7RkXUAs

# See Also

-   [[Address|Bitcoin address]]-   [[Base58Check_encoding|Base58Check encoding]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Technical_background_of_version_1_Bitcoin_addresses](https://en.bitcoin.it/wiki/Technical_background_of_version_1_Bitcoin_addresses)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated we acknowledge the original authors.