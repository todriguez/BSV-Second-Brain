The Byzantine Generals Problem was first proposed by Leslie Lamport,
Robert Shostak, and Marshall Pease as part of research being conducted
at NASA. The problem deals with, how to define, how to direct a network
of disconnected units in a leaderless situation. It has been somewhat
adapted to the problem of Bitcoin for this description, however the
original paper can be found
[here](https://people.eecs.berkeley.edu/~luca/cs174/byzantine.pdf).

The problem defines how Generals can issue commands without a
centralised communication structure, while remaining robust in the face
of bad actors who might try to issue malicious commands to the army.

The Byzantine army is encamped outside a city broken into divisions,
each controlled by a General. Generals have no means to communicate
other than through messengers. There are traitorous Generals in the army
who will try to issue commands that prevent the loyal Generals from
reaching agreement on a reasonable plan forward, so the messaging
protocol must ensure that message receivers can know that they are from
a loyal General.

Anyone can present a message to a General claiming it to be from another
General, so the protocol must have a means for Generals to know with
certainty, that any proposed moves are from another General. A cipher
that demonstrates the message is from a real General is needed. In
Bitcoin, [[Proof of Work|Proof of Work]]demonstrates a node\'s authority to write blocks to the ledger. This is
a core element of [[Nakamoto_Consensus|Nakamoto Consensus]].

The army sometimes becomes divided when two Generals find valid moves at
around the same time. It takes a short period of time for orders to be
propagated so the Generals may end up following divergent moves.

If the army starts moving apart, Generals in the group that falls behind
the front will stop what they are doing and catch up. This is what
happens in a network [[Re-org|Re-org]]with the abandoned
move creating an [[Orphan_Block|Orphan Block]].

The need for Generals to always be at the front of the army incentivises
the best Generals to form direct lines of communication with each other,
leading to much faster communication. In Bitcoin, this incentive drives
Miners to find the best way to connect to each other, driving the
[Bitcoin Core
Network](https://wiki.bitcoinsv.io/index.php "Bitcoin Core Network (page does not exist)")
members into forming a [[Small_World_Network|Small World Network]]with large
highly connected systems. This core trends towards a [[Nearly_Complete_Graph|Nearly Complete Graph]]where all
nodes are connected to almost all other nodes.

Finding valid solutions to proof of work, is generally limited to 6
nodes an hour, so the centre of the mandala trends towards a size maxima
constrained by [Metcalfes
law](https://en.wikipedia.org/wiki/Metcalfe%27s_law "wikipedia:Metcalfe's law").
As more nodes join the competition, it becomes more expensive to
maintain connections, so Miners will instinctively cut ties with
non-performing Miners to connect with newer, more powerful nodes. This
element of constant building to maintain position can be described as a
[Red Queen\'s
race](https://en.wikipedia.org/wiki/Red_Queen%27s_race "wikipedia:Red Queen's race")where participants must continuously accelerate in order to maintain
their position in the field.