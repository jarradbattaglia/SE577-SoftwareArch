# ADR 3: Using Containers for game servers

When running multiplayer game servers, we must have servers that clients connect to which will direct game state and updates to all players connected to the server.  Game state could be things like player positions, attacks, simulating hits, score, etc.  The goal of this design should be to deploy our lobbies for players to connect to as fast as possible as player population can change drastically throughout the day (peak times vs off peak), while giving us flexibility on how many resources to give a server and ensuring game server instances do not impact the experience of other players.

# Decision

We have decided to use containers to deploy and run our game server code.  Also easier to run development servers locally, without much drift from server environment (MiniKube, local containers, etc).

# Rationale

The 2 choices we considered were virtual machines/instances like EC2 using bare virtual instances or running containers (most likely using some orchestration tool like Kubernetes or ECS) 

The reason for choosing containers over other options like bare virtual machines instances is explained mostly by ease of deployment and ability to update.  Instances would require a more complicated setup of game servers to handle multiple instances of a game server on a single instance of a machine, which depending on network/cpu/or memory, one instance of a game taking resources in the application could impact other games on the server as resource allocation is difficult at that level and tools must be created to manage that or leverage more services to handle that load, which may increase cost and latency.  Though using a bare instance, has the least amount of overhead (where as kubernetes has many network calls and container overhead).

Containers work best, especially for a game our size as we would think the server requirements should be lower as games are typically short 

Also virtual machines need to be configured with a base set of CPU and Memory, where as containers we can limit and reserve much easier the resources and allow Kubernetes to determine how many servers can fit on a single machine much easier. 

Also containers gives us portability and isolation, because a container will act as a single pod that hosts a single instance of a game, it should not brown out or cause issues with other containers on the same machine. Where as to fully utilize the resources of a EC2 instance (as VMs need their own OS instance, etc), we will have to host multiple games on a single instance thus increasing our security needs, resource optimization tools, and server code to not conflict.

# Status

Proposed

# Consequences

The advantages of using Kubernetes for running containers over projects like ECS or EC2 VMs for hosting our game server code is many:

- Kubernetes is a known industry product/service, and migrating to other clouds should not require large refactoring for deployments and settings.
- Each game server is hosted on a single pod, thus the ability for other clients to affect or impact other games is less as built in resource utilization is easier to control and defined in Kubernetes
- The ability to deploy new game servers relies only on the speed of starting up the container and clients connecting.  In the instance of a pod or underlying server experiencing failure, it is easier to take and move containers to other servers, making impact to players minimal, where as VMs we would potentially need to spin up a new server more frequently to handle moving those players.
- The amount of servers to provision for player load can be made on the fly much easier, as the only setup would be to add more servers to a kubernetes environment and decrease them when needed.  Also the resource use of containers is much more variable as we can reserve and limit containers resources more defined.  Managed services like EKS leverages this better than us provisioning servers.
- Kubernetes and containers have built in monitoring resources that allow us to see the state of network, resource utilization, and more.  This is built in or easy to deploy, where as other solutions would require us to build out or rely on third party services.
- Managed solutions like EKS allows us to upgrade our environment in an automated way to a supported version, no knowledge needed of how to upgrade kubernetes

Some of the disadvanatages of using containers and surrounding kubernetes architecture are:
    
- Where as virtual machines is really a OS level solution, that requires a deep knowledge.  Kubernetes will require our support staff to have knowledge of both containers and Kubernetes to troubleshoot problems, potentially increasing the time to solve a problem as well as knowledge of network plugins and more. 
- If there is something wrong with our kubernetes stack, that may affect all games hosted on that kubernetes stack.  With a Virtual machine only the underlying host may be affected, but its networking is not dependent on other hosts like they are in kubernetes.
- There is more overhead in the kubernetes infrastructure than a bare instance server and that may cause some latency delay.
