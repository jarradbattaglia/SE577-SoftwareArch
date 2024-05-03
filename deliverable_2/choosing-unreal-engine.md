# ADR 2: Using unreal engine as our games client and server engine

For our game, we need to decide on a game engine that will help us create our game whether it be a open source engine, closed source with a license, or one that we create ourselves.  We cannot get started on development and prototyping without deciding on a game engine, so this must be decided before production begins.  Game engines come with a suite of features that differ between each one, such as physics and particle simulation, networking, and most importantly graphics rendering. As we are making a multiplayer game, it must be able to also deploy and create packages that can be run on multiple operating systems and devices and be able to help in the process of creating and managing 3D objects and gameplay, and preferably.  The engine must also be supported with updates or be open enough for our team to make any necessary changes.

# Decision

We have decided to go with the Unreal Engine game engine and the C++ programming language, due to its industry wide support, simple licensing structure, and high suite of features.

# Rationale

We considered a few different options when deciding on our game engine including building our own engine, the Unity Engine, Unreal Engine, and the Godot Engine.

We quickly ruled out building our own engine as the time and expertise needed to build one is not feasible and would require a large amount of specialized staff.  Next we also ruled out the Godot engine, while an up and coming engine, open source and supports a suite of popular programming languages (C++ and C#), it does not currently have a large amount of features and would require a large amount of work to potentially add missing ones, if needed.  

This lead us to the 2 most popular engines that teams typically use, Unreal Engine and Unity Engine.  Unity Engine has typically been seen as a more beginner friendly engine that has an easier to use UI as well as its support for C#, support for 2D graphics tools, previously a simple subscription, but has recently changed to a 2.5% royalty (above 1 million dollars) and install based fee and also a potential to have a perpetual license of the version we use.   Negatives, compared to Unreal, usually include worse performance and bugs and a lack of documentation, as well as not as large of a professional base as more cutting edge graphical games have used Unreal and not as large of features for networking.

What lead us to choosing Unreal, was its support for C++ and C#, though its C# support is new, and is more widely used in professional teams.  It has by far the largest suite of features that includes all of the components we require (cutting edge graphics technologies, networking frameworks and deployment tools, and packaging for devices whether it be mobile, console or PCs).  The negatives of unreal are typically around its pricing, which is free until we pass 1 million in sales and then a perpetual 5% royalty as well as costly, though thorough documentaiton and support and its UI is typically seen as more complex with a high learning curve and more 3D focused, but more feature laden.

None of the engines considered are open source, but do come with a restrictive read-only license.

# Status

Proposed

# Consequences

Negatives: 

* Because of choosing Unreal, we have chosen the most expensive of options, compared to other engines, but because of our high requirement goals and networking focused game, we see it as worth the cost and its true impact (royalties) does not become evident until we start selling our game to the public.  

* We are now restricted on our code, because all engines have their own suite of tools and features, if we decide something does not work or terms change and Unreal becomes not suitable, a large amount of effort will be required to move to a new engine and need a complete rewrite of engine and rendering calls.

Positives:

* Has state of the art graphics rendering, networking toolsets, and general features that that will allow us to quickly prototype and ship faster than on other engines, that would most likely have us needing to invest more development time into creating standard toolsets.
* Its large amount of support for different devices and hardware will allow us to release on a large amount of services, while minimizing tooling.
* Because of its large use case in the professional industry, hiring and general support should be easier than training people on lesser used engines.
