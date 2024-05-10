# ADR 3: Using Containers for game servers

When running multiplayer game servers, we must have servers that clients connect to which will direct game state and updates to all players connected to the server.  Game state could be things like player positions, attacks, simulating hits, score, etc.  The goal of this design should be to deploy our lobbies for players to connect to as fast as possible as player population can change drastically throughout the day (peak times vs off peak), while giving us flexibility on how many resources to give a server and ensuring game server instances do not impact the experience of other players.

# Decision

We have decided to use containers to deploy and run our game server code.  Also easier to run development servers locally, without much drift from server environment (MiniKube, local containers, etc).

# Rationale

The 2 choices we considered were virtual machines/instances like EC2 using bare virtual instances or running containers (most likely using some orchestration tool like Kubernetes or ECS) 

We first looked at using EC2 instances and either running multiple instances of a application on that server or spinning up many instances on smaller servers and scaling down when a match is finished.  Using EC2 instances compared to containers and a orchestration layer,  allows the machine to take full advantage of its resources, containers would typically need some overhead factored in, this would mainly come in on servers servicing hundreds of players or games.  There is support for scaling using auto scaling groups and deployment services to ensure applications are running  The main negatives with EC2 instances is in its monitoring and scale, monitoring a large amount of machines and its running services will require robust monitoring that we will have to manage or if we use many services on a machine, managing that state to ensure other instances of game servers do not steal or interfere with resources, would require another tool to manage all our servers.  Also cost is more expected, as managed services for containers do cost extra and using orchestration layers like Kubernetes have a larger area to learn and manage, with more overhead.
 
What lead us to using containers over virtual machines:

- Portability: Using containers, we can deploy the same image locally or on a server and expect similar performance and setup, no matter the operating system or settings required.  
- Ease of deployment: Similar to above, but containers we can use tools like ECS or Kubernetes to deploy and scale our applications much easier and applications load faster than spinning up virtual machine instances.
- Resource Limiting: Using orchestration layers like ECS or Kubernetes, allows us to limit how much resources a container may use, which helps limit the impact multiple pods on a machine can cause
- Monitoring: Easier to monitor pods of containers over singular OS instances of those same applications, many monitoring tools exist to monitor pods of containers
- Scale: As we expect to use either small machines or have multiple games hosted on a single instance of a machine, it becomes important to scale fast and waiting for VM instances to load settings may cause longer load times and thus money.

# Status

Proposed

# Consequences

The advantages of using Containers for running our game servers over using EC2 VMs for hosting our game servers is:

- Flexible to choose orchestration layer, many options exist that range from being simpler to complex (ECS to Kubernetes), and gives us options to how we want to deploy our code and services.
- Each game server is hosted on a single pod, thus the ability for other clients to affect or impact other games is less as built in resource utilization is easier to control and can be defined easier using orchestration
- The ability to deploy new game servers relies only on the speed of starting up the container and clients connecting.  In the instance of a pod or underlying server experiencing failure, it is easier to take and move containers to other servers, making impact to players minimal, where as VMs we would potentially need to spin up a new server more frequently to handle moving those players.
- The amount of servers to provision for player load can be made on the fly much easier, as the only setup would be to add more pods and scale servers up and decrease them when needed.  Also the resource use of containers is much more variable as we can reserve and limit containers resources more defined.  Managed services like EKS leverages this better than us provisioning servers.
- Kubernetes and ECS have built in monitoring resources that allow us to see the state of network, resource utilization, and more.  This is built in or easy to deploy, where as other solutions would require us to build out or rely on third party services.
- Managed solutions like EKS allows us to upgrade our environment in an automated way to a supported version, no knowledge needed of how to upgrade kubernetes

Some of the disadvanatages of using containers and surrounding kubernetes architecture are:
    
- Where as virtual machines is really a OS level solution, that requires a deep knowledge.  Containers/Kubernetes/ECS will require our support staff to have knowledge of both containers and underlying networking to troubleshoot problems, potentially increasing the time to solve a problem as well as knowledge of network plugins and more. 
- If there is something wrong with our instance, that may affect all games hosted on that instance.  With a Virtual machine only the underlying host may be affected, but its networking is not dependent on other hosts like they are when hosting multiple pods.
- There is more overhead in the container infrastructure than a bare instance server and that may cause some latency delay.
