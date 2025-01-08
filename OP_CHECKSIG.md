**OP_CHECKSIG** is an opcode that verifies an [[Elliptic_Curve_Digital_Signature_Algorithm|ECDSA signature]].
It takes two inputs from the stack, a public key (on top of the stack)
and an ECDSA signature in its DER_CANONISED format concatenated with
sighash flags. It outputs true or false on the stack based on whether
the signature check passes or fails.

\

# Parameters

In addition to the stack parameters, OP_CHECKSIG needs to have

1.  the current transaction
    [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d662c7a919063d69ae5854f90fb6e2d8c943a7d)],
2.  the [[Index|index]]of the transaction input in which
    the signature is checked
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20|]]],
3.  the scriptPubKey in which this OP_CHECKSIG belongs
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/ce3be48c7113bf71aef9fad3345dcfeab61b3346|]]],
    and
4.  the value in satoshi that the outpoint represents
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/d6d89717a1ca9283cc3a1e9d896ecdaf8377c0a5|]]].

Note that
[[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/ce3be48c7113bf71aef9fad3345dcfeab61b3346|]]]
is from previous transaction, in which the output is spent in current
transaction.

# How it works

In short, OP_CHECKSIG calls a function called \"sighash\" which produces
a hash value of the serialised transaction. (For legacy sighash
algorithm, please click
[[Legacy_Sighash_Algorithm|here]].) The
hash value is the message on which the signature is verified. The
signature and the public key involved in the verification are obtained
from the stack.

In detail
1.  Check the stack size is not less than 2.
2.  The public key and the signature are popped as the top 2 items of
    the stack.
3.  Check the signature encoding is of the correct format \[\<DER
    signature\>\<hashtype\>\]. An example
    47304402205a2b556c71ee1c12d8e0b460c3446aeca0e3ee71b7bc11c6ddd3da8beeec99c60220783a1f0c0158674df8904022ec30fab5154c4fc4c7e8467086f0204cc8e16cbb01,
    where 47 indicates number of bytes in hex (71 in decimal) of the
    signature including 1 byte of sighash flag at the end, the next 46
    bytes (70 in decimal) are the ECDSA signature (r,s), the last byte
    is the sighash flag \"ALL\".
4.  Check the public key encoding is of the correct format. Both
    compressed public key and uncompressed public key can be acceptable.
    An example
    210220798b9772a8ae06d13027e6f501d09ea07f6dfc4b7afc3db3a6d6c57bf24239,
    where 21 indicates the number of bytes in hex of the public key, 02
    indicates this is a compressed public and the y-coordinate is an
    even number, the rest is the value of the x-coordinate of the public
    key. Note that if the second byte is 04, then it indicates that the
    public key is given in its uncompressed form.
5.  A new subScript is created from the
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/ce3be48c7113bf71aef9fad3345dcfeab61b3346|]]].
    The subScript starts from the most recent OP_CODESEPARATOR (the one
    just before the OP_CHECKSIG that is executed here) to the end of the
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/ce3be48c7113bf71aef9fad3345dcfeab61b3346|]]].
    If there is no OP_CODESEPARATOR, the entire
    [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/ce3be48c7113bf71aef9fad3345dcfeab61b3346|]]]
    becomes the subScript.
6.  Any remaining OP_CODESEPARATORS are removed from the subScript.
7.  A serialisation algorithm (sighash) is called to produce an input to
    double SHA256 depending on sighash type
    1.  nVersion in
        [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d662c7a919063d69ae5854f90fb6e2d8c943a7d)] (4-byte little endian).
    2.  double SHA256 of the serialisation of all input outpoints
        (32-byte hash).
        1.  if ANYONECANPAY flag is set, then this should be a 32-byte
            zero.
    3.  double SHA256 of the serialisation of nSequence of all inputs
        (32-byte hash).
        1.  if ANYONECANPAY flag is set, then this should be a 32-byte
            zero.
    4.  the outpoint being spent (32-byte for transaction ID + 4-byte
        little endian for index).
    5.  length in bytes of the subScript (big endian).
    6.  the subScript.
    7.  [[$$]![[https://wikimedia.org/api/rest_v1/media/math/render/svg/d6d89717a1ca9283cc3a1e9d896ecdaf8377c0a5|]]]
        (8-byte little endian).
    8.  nSequence of this outpoint (4-byte little endian).
    9.  double SHA256 of the serialization of all output amount (8-byte
        little endian) with scriptPubKey (These are the outputs in
        [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d662c7a919063d69ae5854f90fb6e2d8c943a7d)].).
        1.  If SINGLE flag is set and the input index is smaller than
            the number of outputs, then this should be the double SHA256
            of the output with scriptPubKey of the same index as the
            input.
        2.  If NONE flag is set, then this should be a 32-byte zero.
    10. nLocktime of the transaction
        [[$}$]![}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d662c7a919063d69ae5854f90fb6e2d8c943a7d)] (4-byte little endian). 11. sighash type of the signature (4-byte little endian).
8.  The serialisation in bytes from the step above will be fed to double
    SHA256 to produce the 32-byte message. This message is used to check
    the ECDSA signature, together with the public key and the signature
    obtained from the stack. Note that the
    [[Secp256k1|secp256k1]]elliptic curve is used for
    the verification with the given public key.

# Return values

OP_CHECKSIG will push true to the stack if the check passed, false
otherwise. OP_CHECKSIGVERIFY leaves nothing on the stack but will cause
the script validation to fail immediately if the check does not pass.

# References

[https://github.com/bitcoin-sv/bitcoin-sv/blob/master/src/script/interpreter.cpp](https://github.com/bitcoin-sv/bitcoin-sv/blob/master/src/script/interpreter.cpp)See [[SIGHASH Flags|SIGHASH flags]]for more detail
on the effect of combinations of flags.

# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/OP_CHECKSIG](https://en.bitcoin.it/wiki/OP_CHECKSIG)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.