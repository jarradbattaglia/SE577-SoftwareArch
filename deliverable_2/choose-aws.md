# ADR 3: Choosing Amazon Web Services (AWS) as our Cloud Service

When looking to build our online infrastructure for our game we need an environment that allows us the flexibility to scale to multiple areas of the world quickly, while offering an infrastructure that can scale to millions of customers in a short period of time, while having a standard of high availability and ensuring low latency for our clients and internal services.  We would also like to consider leveraging any game tools that the providers provide that may improve development and deployment of our tools or reduce development of key features.

# Decision

We have decided to use only one cloud provider and that will be Amazon Web Services.  They will be used to host all of our networking services and resources including our game servers.

# Rationale

There were 3 choices of cloud providers considered during our decision making process.  They were Azure, Google Cloud Platform and Amazon Web Services (AWS).  All 3 of the options considered are large, global infrastucture as a service products with a large amount of features and global footprints.  All 3 offer similar pricing (pay as you go model), availability guarantees, and feature sets to each other in the form of virtual servers, storage, databases and Kubernetes support and all offer robust serverless services, and each offer large virtual machine solutions that go well beyond our desired use cases.

Google Cloud Platform is seen as maybe the most performant network and latency wise between the 3 providers, but also has the smallest footprint of availability zones and regions.  They do have a game development tools available, but their support is not wide spread and their cancellation of their gaming studio may be seen as a negative to their upcoming support of similar technologies.

Azure offers a large amount of availability zones, with more regions and services than GCP.  They offer a robust game service suite called PlayFab which is supported and used by their own large internal studios, and a large amount of public use case and support and offers matchmaking scaling services, authentication and identity services, and party/chat services.  Their Playfab technology also does not support kubernetes.  Generally in the middle on price, services and availability zone locations of the 3.  If we rely on microsoft products/services (Windows VMs, SQL Managed Services, etc, they may be cheapest for these features), we currently do not plan on using microsoft services though.

AWS offers by far the largest amount of availability zones and services of the 3 being discussed.  They also offer their own game development services (Gamelift) that include matchmaking services, monitoring and metrics, and authentication and identity services, as well as scaling solutions for Kubernetes.  Their integrations and ownership with the largest active video gaming streaming site (twitch.com) was considered a positive as well.  Has maybe the most amount of documentation and public documentation and is the longest operating of all 3.

# Status

Proposed

# Consequences:

Negatives:
    
* Going with one cloud provider may lead to vendor lock in, most scripts and knowledge will be more AWS oriented and if AWS is having issues, it will take more effort or not be possible to fix and our service will be down.  
* If we decide to leverage any services of AWS especially their game oriented ones, the refactor of code and scripts will be a large effort if we migrate to another similar service.
* On average, their virtual servers may be considered the most expensive, but mostly dependent on use case and can we leverage other services to bring costs down.

Positives:
    
* Global reach and availability zones across the world should allow us to load and deploy games in a large amount of regions allowing our players to have low latency connections.  
* Their gaming products support for kubernetes may be leveraged for our game servers and reducing costs compared to competitors, and they seem to be introducing new products and services more than their competitors.  
* Also their large amount of services and feature development we view as having benefits for new features that can be leveraged at a later time.  
* Robust documentation on internal sites and on public forums is considered the best. 
