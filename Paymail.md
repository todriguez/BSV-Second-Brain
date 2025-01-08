Paymail is a practical implementation of the family of related protocols
collectively referred to as [[BSVAlias|BSVAlias]]. In
brief, it is an identity protocol that removes Bitcoin addresses from
the user experience. Instead of addresses, Paymail uses human-readable
names that look exactly the same as email addresses. Paymails are much
easier to type into a device than Bitcoin addresses and can be used to
identify an individual via the Paymail identifier.

The protocol describes a procedure where a wallet provider will be able
to be discovered and contacted, and can respond to payments and payment
requests in real time so that payment receivers don't have to re-use
their Bitcoin [[Address_reuse|addresses]]thereby
maintaining privacy.

As a simplified example, in order for Alice to send some bitcoin to Bob,
Alice sends the payment to
[\[email protected\]](https://wiki.bitcoinsv.io/cdn-cgi/l/email-protection). The paymail protocol
implemented by Bob\'s wallet will provide a Bitcoin script to pay to for
the actual Bitcoin transaction creation rather than relying on the
concept of the Bitcoin address which is actually just a compact encoding
of a script, but limits the form of the script to one particular type.
This is done behind the user experience. Note that the security will
rely on a public key infrastructure.

At the time of writing, the protocols cover
-   BRFC Specifications
-   Service Discovery
-   Public Key Infrastructure
-   Payment Addressing

For more information visit the [BSVAlias
website](https://bsvalias.org/).

An implementation of these protocols can be used for access delegation
in a similar fashion to [[0auth|0auth]].

Paymail is the name for the implementation of the following protocols
-   Service Discovery
-   Public Key Infrastructure
-   Basic Address Resolution from the Payment Addressing protocol group

The Paymail brand is reserved for products and services that, at a
minimum, implement each of the above protocols.

[Moneybutton](https://moneybutton.com)has published content describing Paymail and why it is needed
[here](https://blog.moneybutton.com/2019/05/31/introducing-paymail-an-extensible-identity-protocol-for-bitcoin-bsv/)