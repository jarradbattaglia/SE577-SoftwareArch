ADR 4: Choosing Redis as our  game state storage database

As players send commands to our game servers, the actions and events that they produce we would like to store, so that we may use in a variety of use cases.  For instance, we may need to transition a game lobby off a server in the case the underlying server is no longer functional, we could read back the previous state and transition the game to another server quickly instead of canceling the game.  We may also be able to analyze player input and events for things such as cheating and game balancing.  This would allow our testing and corresponding teams to move ahead early with a known technology base.

Decision

We have decided to use the Redis database as our in-memory/cache database.

Rationale

There were 2 choices that we considered for our in-memory/cache database

Status
Proposed

Consequences
Describe here the resulting context, after applying the decision. All consequences should be listed, not just the "positive" ones.