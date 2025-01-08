BSVAlias is a family of related standard protocols that enable the use
of email style addresses for Bitcoin SV. Services that implement these
protocols can be run by a domain owner or through a third party.

The goals of BSVAlias are
-   User friendly payments
-   Permissionless implementation
-   Self hosting
-   Automatic discovery process
-   PKI infrastructure (IPV4)
-   Security
-   [[Extensibility|Extensibility]][[Paymail|Paymail]]leverages BSVAlias into a set of
protocols that allows BSV wallets to receive payments using email
addresses as handles.

The protocols allow for flexibility in capabilities and implementation.

# Service Discovery

The Service Discovery Process is split into two phases
1.  Host Discovery
2.  Capability Discovery

# Host Discovery

Host Discovery is a DNS based lookup of the responsible host for a given
BSVAlias. One practical implementation that exists today is Paymail, in
which the host is identified through the domain attached to the
receiving party\'s paymail address, which is in standard email format
(e.g.
[\[email protected\]](https://wiki.bitcoinsv.io/cdn-cgi/l/email-protection)).

BSVAlias can be
1.  Self hosted
2.  Hosted using 3rd party providers (done using a DNS SRV record)

This makes BSVAlias compatible with the internet infrastructure we have
today.

# Capability Discovery

Once the host has been identified, the sending party must learn its
supported features.

This is in the format of a machine readable ([[JSON|JSON]])
document which is placed on the host web server in the .well-known
folder
https://\<target\>:\<port\>/.well-known/bsvalias

Capabilities of a host are not necessarily reflected in an individual
account.

# References

1\. BSVAlias specification -
[https://bsvalias.org/](https://bsvalias.org/)