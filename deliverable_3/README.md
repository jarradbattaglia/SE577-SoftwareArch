# System Context Overview

The project is the networking architecture for a game client to connect to dedicated game servers in our environment and communicate with other players and also allow players to make in-app purchases, which they may use in their multiplayer games.  We have identified 2 users of the system, the internal developer and a player who has downloaded our game client on a device of their choosing.  

Below we will describe the general flow of a player user logging in, buying an item and then playing a match.

# Project Container Overview

## Account Component

At the beginning we have a player (user), that first logs in to our authentication service.  They will take that token with them to all services that  will use that to authenticate the user.  Next the user, may want to go purchase a skin or item from our in-game store.  They will contact our api, which will return a list of products, they will choose one and communicate their payment information with our store api, which will verify with the external payment provider (think Paypal/Venmo/Stripe/etc).  Once we get confirmation of purchase, we write that information to the store/account database.

## Matchmaking Component

If the player would like to play a match with other players, in the client they may hit "play match" which will send a request to our matchmaking service api, which will put that player in a "queue", this uses Amazon Gamelift service and their matchmaking logic, which puts a "ticket" into a dynamodb, while another service, which we call a "ranker" service will sort through various metrics (like match history, rank, connection, etc) and match players together, with players not being matched the longest being prioritized higher.  After finding a match for a group of players, it updates the ticket which when the client requests an update on status, will get a notification and accept the match.  

We put a Amazon load balancer in front to distribute load 

## Game Service Component

Once a match is configured from matchmaking, it sends a notification to our game manager, which will spin up a game instance and report those connections details back to the matchmaking service.  Once players receive that info, they connect the particular instance.  As players load in, the service requests general game information about the players and current patch, which it retrieves from the data service api, as players configure their character, the game server will also get purchase information from account services and allow a player to use skins if available.  After the game is completed, the game manager updates the data api service with match information and stats.

## Data Services Component
As players play and communicate with the server, it will store events that occur in the game to a set of cache servers that an ingest service will go through and write to our data service database, this data is considered non-critical so if lost, does not break any services, but is used to enhance matchmaking and internal metrics.

The developers role is there to either update the store (S3 backend/Store API/promotions) and also the data service (for instance, edit a characters damage or health or a weapons stats, which would reflect in future games).
