ADR 1: Using Containers as game servers

When running multiplayer game servers, we must have servers that clients connect to which will direct game state to all players connected to the server.  Game state could be things like player positions, attacks, simulating hits, score, etc.  The goal of this design should be to deploy our lobbies for players to connect to as fast as possible as player population can change drastically throughout the day (peak times vs off peak), while giving us flexibility on how many resources to give a server and ensuring certain servers do not impact the experience of other players.

Decision

We have decided to use containers to deploy and run our game server code, using a Docker solution and a Kubernetes architecture.  We will build Docker images for each version of our server code and align with front-end client version and allow us to deploy new lobbies much easier as everything is built into the container and not a deployment script.  Each container will act as a single instance of a server/game, and one lobby will connect to that container.

Rationale
The reason for choosing containers over other options like virtual machines or bare metal servers is explained mostly by speed, ability to update, and expected result of a deployment.  Bare metal servers are the most expensive option and would require a more complicated setup of game logic to handle multiple servers on a single instance of a machine, which depending on bugs or network, one game taking resources in the application could impact other games on the server as resource allocation is difficult at theat level and code must be created to manage that.  

So the option comes down to Virtual Machines or Containers, and the ability to scale with containers should allow us to start and get players into games faster as spinning up virtual machines and configuring could take a while, which forces us into a similar situation as bare metal, where we will have to prepare for load ahead of time and over provision multiple VMs for players to connect to, thus costing us more.  Also virtual machines need to be configured with a base set of CPU and Memory, where as containers we can limit and reserve much easier the resources and determine how many servers can fit on a single machine much easier. Also containers gives us portability and isolation, because a container will act as a single server that hosts a single type of game, where as to fully utilize the resources of a VM (as VMs need their own OS instance, etc), we may have to host multiple games on a single VM instance thus increasing our security needs and resource optimization.

Status
Proposed

Consequences

The advantages of using Containers over VMs for hosting our game server code is many:
    - Isolation:  Each game server is hosted on a single pod, thus the ability for other clients to affect or impact other games is less as built in resource utilization is easier to control and defined in Kubernetes
    - Speed of deployment and Portability: The ability to deploy new game servers relies only on the speed of starting up the container and clients connecting.  In the instance of a pod or underlying server experiencing failure, it is easier to take and move containers to other servers, making impact to players minimal, where as VMs we would potentially need to spin up a new server more frequently to handle moving those players.
    - Scalability: The amount of servers to provision for player load can be made on the fly much easier, as the only setup would be to add more servers to a kubernetes environment and decrease them when needed.  Also the resource use of containers is much more variable as we can reserve and limit containers resources more defined per game type.
    - Built in monitoring: Kubernetes and containers have built in monitoring resources that allow us to see the state of network, resource utilization, and more.  This is built in or easy to deploy, where as other solutions would require us to build out or rely on third party services more.


Some of the disadvanatages of using containers and surrounding architecture are:
    - More robust infrastructure upfront: Virtual machines would require less up front resources to build as containers require a kubernetes infrastructure and relying on that infrastructure to handle all network communications and resource allocation.  But without, we would need to invest in ways to handle these problems with either our own solutions or bought solutions
    - Learning curve:  Where as virtual machines is really a OS level solution, that requires a deep knowledge.  Kubernetes will require our support staff to know both the OS level and how knowledge of both containers and Kubernetes to troubleshoot problems, potentially increasing the time to solve a problem.  If there is something wrong with our kubernetes stack, that may affect all games hosted on that kubernetes stack.  A Virtual machine only the underlying host may be affected, but its networking is not dependent on other hosts like they are in kubernetes.