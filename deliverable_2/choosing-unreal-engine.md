# ADR 2: Using unreal engine as our games client and server engine

For our game, we need to decide on a game engine that will help us create our game whether it be a open source engine, closed source with a license, or one that we create ourselves.  We cannot get started on development and prototyping without deciding on a game engine, so this must be decided before production begins.  Game engines come with a suite of features that differ between each one, such as physics and particle simulation, networking, and most importantly graphics rendering. As we are making a multiplayer game, it must be able to also deploy and create packages that can be run on multiple operating systems and devices and be able to help in the process of creating and managing 3D objects and gameplay.  The engine must also be supported with updates and security updates over time.

# Decision

We have decided to go with the Unreal Engine game engine as our client and game server engine.

# Rationale

We considered a few different options when deciding on our game engine including building our own engine, the Unity Engine, Unreal Engine, and the Godot Engine.

We quickly ruled out building our own engine as the time and expertise needed to build one is not feasible and would require a large amount of specialized staff (this option is typically done at larger companies with multiple teams).  Next we also ruled out the Godot engine, while an up and coming engine and supports a suite of popular programming languages (C++ and C#), it does not currently have a large amount of features and would require a large amount of work to potentially add missing ones, if needed.  

This leads us to the 2 most popular engines that professional teams typically use, Unreal Engine and Unity Engine.  Unity Engine has typically been seen as a more beginner friendly engine that has an easier to use UI as well as its support for C#, great support for 2D graphics tools, previously its licensing used a simple subscription, but has recently changed to a 2.5% royalty (above 1 million dollars) and install based fee, but does also have a potential option to have a perpetual license of the version we use.   But it also has a reputation of usually having worse performance on consoles and its games have more prevalant bugs (due to immature tooling), it also has not as large of a professional base as more cutting edge graphical games have used Unreal and it does not have as large of features for networking.

What lead us to choosing Unreal, was:

- Support for Multiple Languages:  It supports C++ and C# (though support is new for C#) as its programming languages which gives teams flexibility of choices, Unity only allows C#
- Wide Use in Industry/Support: More widely used in professional teams throughout the industry, finding new developers with experience should be easier than using other engines.  Large amount of internal documentation exists as well.  
- State of the art features: It has by far the largest suite of features that includes all of the components we require (cutting edge graphics technologies, networking frameworks 
- Robust deployment tools: Large amount of building options and deployment tools including packaging for devices whether it be mobile, console or PCs.
- Great performance: Has options to scale perforamnce for many types of devices, allowing developers to maximize compatability without large code changes.
- Networking support: Has many toolsets for networking specific tasks and integrations with external services

To state some negatives of unreal though, are typically around its pricing, which is free until we pass 1 million in sales and then a perpetual 5% royalty as well as costly, its UI is typically seen as more complex with a high learning curve and the engine tools are more 3D focused (with little support for 2D tools).  

None of the engines considered are open source, but do come with a read-only license.

# Status

Proposed

# Consequences

Positives:

- Has state of the art graphics rendering, networking toolsets, and general features that that will allow us to quickly prototype and ship faster than on other engines, that would most likely have us needing to invest more development time into creating standard toolsets.
- Its large amount of support for different devices and hardware will allow us to release on a large amount of devices, while minimizing tooling and deployment tools (built-in).
- Because of its large use case in the professional industry, hiring and general support should be easier than training people on lesser used engines or propietary ones.
- Large amount of community plugins and integrations, which may allow us to develop new features faster

Negatives: 

- We have chosen the most expensive of options, compared to other engines, but because of our high requirement goals and networking focused game, we see it as worth the cost and its true impact (royalties) does not become evident until we start selling our game to the public, but still tied to any rules and limitations they may impose.

- Restriction on our code, because all engines have their own suite of tools and features, if we decide something does not work or terms change and Unreal becomes  unsuitable, a large amount of effort will be required to move to a new engine and need a complete rewrite of engine and rendering calls.

- Higher learning curve compared to other engines, as it is not widely used outside professional team (Unity is the beginners choice), new developers may need some ramp up to learn its differences.