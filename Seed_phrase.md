A **seed phrase**, **seed recovery phrase** or **backup seed phrase** is
a list of words which correspond to the master private key of a Bitcoin
SV wallet. In typical usage, a wallet will generate a seed phrase and
instruct the user to write it down on paper. If the user\'s computer
breaks or their hard drive becomes corrupted, they can download the same
wallet software again and use the paper backup to deterministically
re-generate their wallet. Seed phrases are the most frequently
encountered means of backing up Bitcoin SV wallets.

Anybody with access to the phrase can steal the bitcoins, so it must be
kept safe. Phrases should not be transmitted electronically and should
never be written on any website.

# Example

An example of a seed phrase is
       witch collapse practice feed shame open despair creek road again ice least

The word order is important.

# Explanation

A simplified explanation of how seed phrases work is that the wallet
software has a list of words taken from a dictionary, with each word
assigned to a number. The words in the seed phrase are each converted to
their corresponding number and concatenated to generate the seed integer
to a [[Deterministic_wallet|deterministic wallet]]. From this
seed integer the wallet generates all [[Private Key|key pairs]]used in the wallet.

The English-language wordlist for the BIP39 standard has 2048 words, so
if the phrase contained only 12 random words, the number of possible
combinations would be 2048\^12 = 2\^132 and the phrase would have 132
bits of security. However, some of the data in a BIP39 phrase is not
random (see: [BIP39: Generating the
mnemonic](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki#Generating_the_mnemonic)), so the actual security of a 12-word BIP39 seed
phrase is only 128 bits.

# Two-Factor Seed Phrases

Several wallets enable their users to generate seed phrases with an
added layer of encryption to prevent someone who discovers the words
from accessing the wallet. The password can be used to create a
two-factor seed phrase where both *\"something you have\"* plus
*\"something you know\"* is required to recover the wallet.

This works by the wallet creating a seed phrase and asking the user for
a password. Then both the seed phrase and extra word are required to
recover the wallet. [ElectrumSV](https://electrumsv.io/)and some other wallets call the passphrase a **\"seed
extension\"**, **\"extension word\"** or **\"13th/25th word\"**. The
BIP39 standard defines a way of passphrase-protecting a seed phrase. A
similar scheme is also used in the Electrum SV standard. If a passphrase
is not present, an empty string \"\" is used instead.

# Storing Seed Phrases for the Long Term

Most people write down phrases on paper but they can be stored in many
other ways such as [[Brainwallet|memorising]]engraving on metal, writing in the margins of a book or any other
creative and inventive way.

For storing on paper, writing with pencil is much better than pen
[Pencil Does Not
Fade](https://www.joethorn.net/blog/2011/12/07/pencil-does-not-fade)[How do I maintain a paper notebook that can
remain for
years?](https://www.quora.com/How-do-I-maintain-a-paper-notebook-that-can-remain-for-years). Paper should be acid-free or archival paper, and
stored in the dark avoiding extremes of heat and moisture [Essential
facts about preservation of
Paper](https://www.loc.gov/preservation/care/deterioratebrochure)[Writing in a notebook with
pencil](https://www.quora.com/If-I-write-with-a-pencil-on-my-notebook-will-the-writing-last-for-a-long-time-say-50-years-or-will-it-just-fade-away-gradually)[CoPAR: Creating records that will
last](https://copar.org/bulletin14.htm).

# Word Lists

Generally a seed phrase only works with the same wallet software that
created it. If storing for a long period of time it\'s a good idea to
write the name of the wallet too.

The BIP39 English word list has each word being uniquely identified by
the first four letters, which can be useful when space to write them is
scarce.

-   [BIP39
    wordlists](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md)-   [Electrum old-style
    wordlist](https://github.com/spesmilo/electrum/blob/1.9.8/lib/mnemonic.py)-   [Electrum new-style
    wordlist](https://github.com/spesmilo/electrum/blob/master/electrum/wordlist/english.txt)[Alternative name \"Mnemonic Phrase\"]

Seed phrases are sometimes called \"mnemonic phrases\" especially in
older literature. This is a bad name because the word mnemonic implies
that the phrase should be memorised. It is less misleading to call them
seed phrases.

# The power of backups

An especially interesting aspect in the power of paper backups is
allowing your money to be in two places at once. You can store backups
on multiple devices/physical media in different locations and with
password encryption. With that, you can carry \$100,000 which can
instantly be moved to a phone or transferred with total security. If
it\'s stolen, then there is no risk because it is backed up elsewhere.
[\[1\]](https://www.reddit.com/r/Bitcoin/comments/2hmnru/poll_do_you_use_paper_wallets_why_why_not_what)

# See Also

-   [[Deterministic_wallet|Deterministic wallet]]-   [[Brainwallet|Brainwallet]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Seed_phrase](https://en.bitcoin.it/wiki/Seed_phrase)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.