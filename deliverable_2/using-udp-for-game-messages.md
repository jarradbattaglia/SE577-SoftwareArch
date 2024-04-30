ADR 5: Using UDP for sending client-server messages for game commands

When players communicate with our servers we must decide what message protocol to use so it ensures low latency (<30-40 ms) between our servers and clients and the least amount of interruption to a players game session.

Decision

We have decided to use UDP as the message protocol when sending game state and commands to our game servers. 

Rationale

The choice for message protocol for sending our game state was between TCP and UDP.  TCP is a protocol that guarantees the messages arrive in the order that they were sent, can retransmit data if packets failed to arrive, and can 

Status
Accepted

Consequences
Describe here the resulting context, after applying the decision. All consequences should be listed, not just the "positive" ones.