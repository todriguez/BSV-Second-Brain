A **paper wallet** is the name given to a method of storing bitcoin
which involves printing a paired [[Private Key|Bitcoin private key]]and [[Address|Bitcoin address]]onto paper and
depositing funds into a
[[Bitcoin Transactions|P2PKH]]script
using the address. Funds can be spent by accessing the physical paper
and entering the private key into a wallet. This is usually achieved by
scanning a QR code of the private key in [[Wallet_import_format|Wallet import format]](WIF).

# Redeeming bitcoins stored using paper wallets

The best way to redeem the bitcoins from a private key is to use the
\"sweep\" feature of certain wallet software. This process creates a new
transaction that sends the entire balance of the paper wallet to a new
address controlled by that wallet.

Various wallets support sweeping private keys including
-   [ElectrumSV](https://electrumsv.io/)-   [Simply Cash](https://simply.cash/)[Downsides/Risks]

Paper wallets are generally regarded as a secure method of long-term
storage of funds; however, there are downsides to using this method.

# Printing and print media

Paper wallets require using a printer to transfer them to paper which
presents a risk if networked printers are used in an insecure
environment.

Additionally, while QR codes have a checksum and robust error
correction, print media can be damaged by water, soilage or through
crumpling or folding of the paper.

# Address reuse

Paper wallets have just one Bitcoin address, leading to [[Address_reuse|address reuse]].

# Poor user experience

Dealing with raw private keys can be unintuitive and may lead to loss of
funds if not managed properly. It is recommended that users of paper
wallets understand how they function before using them as long-term
funds storage.

# Bitcoin ATMs and paper wallets

Many Bitcoin ATMs use a paper-wallet-like system for delivering bitcoins
if the customer doesn\'t have a Bitcoin wallet. The ATMs can print out a
private key/address pair onto paper which contain the customer\'s
bitcoins. Ideally the customer should sweep the bitcoins into their own
wallet as soon as they can.

# See Also

-   [[Seed_phrase|Seed phrase]]# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Paper_wallet](https://en.bitcoin.it/wiki/Paper_wallet)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.