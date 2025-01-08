# Definition

Double-spending is the act of sending a
[[Bitcoin Transactions|transaction]]containing inputs that have already been spent, in an attempt to commit
fraud on the network.

# Consequences

Double spends are one of the most commonly discussed attacks on Bitcoin,
however there has yet to be a documented case of someone executing a
successful double-spend using Bitcoin in commerce.

The reason for this is that double-spending is a crime and analogous to
intentionally bouncing a check - the difference is that the merchant
would have cryptographic proof that the customer attempted such an act.

# Economic incentives

Bitcoin solves the double-spending problem via its economic incentives.
Miners have a strong incentive not to include these transactions in a
block because they are at risk of having their block rejected by other
Miners, and in addition, would be complicit in carrying out a crime.

These factors highlight why the solution to double-spending is an
economic solution, not a technical one. Many arguments have been made by
developers in the past that changes are necessary to the protocol to fix
this issue, but they have been deemed unnecessary.