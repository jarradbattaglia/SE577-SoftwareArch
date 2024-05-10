# ADR 1: Choosing Amazon Web Services (AWS) as our Cloud Service

When looking to build our online infrastructure for our game we need an environment that allows us the flexibility to scale to multiple areas of the world quickly, while offering an infrastructure that can scale to millions of customers in a short period of time, while having a standard of high availability and ensuring low latency for our clients and internal services.  We would also like to consider leveraging any game tools that the providers have that may improve development and deployment of our tools or reduce development of key features.

# Decision

We have decided to use only one cloud provider and that will be Amazon Web Services.  They will be used to host all of our networking services and resources including our game servers.

# Rationale

There were 3 choices of cloud providers considered during our decision making process.  They were Azure, Google Cloud Platform and Amazon Web Services (AWS).  All 3 of the options considered are large, global infrastucture as a service products with a large amount of features and global footprints.  All 3 offer similar pricing models and pricing (pay as you go model with upfront options), similar availability guarantees, and feature sets to each other in the form of virtual servers, storage, databases and Kubernetes support and all offer robust serverless services.  Each also offer large virtual machine flavors  that go well beyond our desired use cases.

Google Cloud Platform has a similar footprint of availability zones and regions than AWS.  But for game development tools their support is not wide spread and their cancellation of their gaming studio may be seen as a negative to their upcoming support of similar technologies.  They are also the least used cloud service of the big 3 cloud providers, so finding developers with experience with our use case and documentation may be harder to support.

Azure offers the largest amount of availability zones, with more regions and services than GCP and AWS.  They offer a robust game service suite called PlayFab which is supported and used by their own large internal studios, and a large amount of public use case and support and offers matchmaking scaling services, authentication and identity services, and party/chat services.  Their Playfab technology also does not support kubernetes (though some public plugins exist).  Generally in the middle on price, services and availability zone locations of the 3.  If we rely on microsoft products/services (Windows VMs, SQL Managed Services, etc, they may be cheapest/best for these features), we currently do not plan on using microsoft services though.  We viewed Azure as being better if fully invested into the Microsoft ecosystem of products, while having lesser support for products and services outside of that.

But the reason we decided on AWS is:

- Flexibility: AWS offers a wide range of products that support linux and Windows, with a larger amount of images than other services
- Availability: Offers a large amount of regions and availability zones, with a higher amount of availability zones per region than other providers
- Amount of Services: Offers a larger amount of general services than Azure and GCP and offers more community products, while Azure has Microsoft specific
- Gaming Services Support: Gamelift services supports all environments (Linux/Windows), and offers a larger amount of services and integrations than competitors
- Maturity: Has been the longest running of all 3 considered and has a large amount of documentation and with it being the largest provider, also has a large amount of public documentation and support
- Kubernetes/Container Support: Many of its products offer robust container and Kubernetes support compared to Azure, as well as its gaming services having kubernetes support and general container services 

# Status

Proposed

# Consequences:

Positives:
    
- Global reach and availability zones across the world should allow us to load and deploy games in a large amount of regions allowing our players to have low latency connections.  
- Their gaming products support for kubernetes may be leveraged for our game servers and reducing costs compared to competitors, and they seem to be introducing new products and services more often than their competitors.  
- Their large amount of services and feature development we view as having benefits for new features that can be leveraged at a later time.  
- Robust documentation on internal sites and on public forums is considered the best. 
- One provider allows us to fully take advantage of services, without needing to provide support for other kinds of services

Negatives:
    
- Going with one cloud provider may lead to vendor lock in, most scripts and knowledge will be more AWS oriented.  
- We are subject to their availability, if their services go down we will not have an option of migrating service easily.

