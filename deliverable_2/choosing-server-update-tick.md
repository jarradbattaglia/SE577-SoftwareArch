# ADR 5: Choosing a 30hz tick rate for servers

When playing online multiplayer games, typically players send commands and actions to their game server and then the game server will process everyones actions on the same tick, it will then send this information out to all players in the game to update the client state.  We must choose a tick rate for our application as it determines the smoothness and preferred latency of our clients, also a higher tick rate requires faster servers to process actions and game state in a lower period of time and forces a preferred lower latency on players.

# Decision

We have decided to choose a 30 hz (about 33 milliseconds) tick rate for our server application and performance target.

# Rationale

When choosing a tick rate, we need to determine how frequently our game servers need to update our clients and process/simulate player actions.  A tick rate corresponds updates per second so 30 tick rate would update every 33 seconds where as a 100 tick rate would update clients every 10 ms.  

Certain styles of games require higher tick rates such as First Person Shooters (Counter Strike, Valorant), which rely on precise and fast mouse movements from a small amount of players (10-20 players per server) in the game.  Games like MMORPGs (World of Warcraft, etc) require low tick rates as many players are performing actions on cooldowns, but require large servers to handle hundreds of players at a time.  Games in the battle arena space have typically required around 20-30 ticks per second and we would like to be on the higher side and match our competitors. 

Because the nature of our game is slated to use more time based restrictions (cooldowns) and does not require a large amount of player actions per second, we can afford to use a lower tick rate.

# Status

Proposed

# Consequences

Positives Consequences:

- Lower server resources potentially required and allows more time to process game state
- Allows a higher latency requirement as players get updates more infrequently
- On the higher side of performance compared to competitors, with room to increase if needed

Negative Consequences:

- Clients and game do not update as fast, higher frame rates may see some hitching/lag as game state updates
- If we change game style to something more fast paced, server flavor and settings would need to be changed, with potentially more architecture changes to support higher tick rate/lower latency requirements.
