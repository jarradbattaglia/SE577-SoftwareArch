ADR 3: Choosing AWS as our Cloud Service

When looking to build our online infrastructure for our game we need an environment that allows us the flexibility to scale to multiple areas of the world quickly, while offering an infrastructure that can scale to millions of customers in a short period of time, while having a standard of high availability and ensuring low latency.

Decision

We have decided to use only one cloud provider and that will be Amazon Web Services.  They will be used to host all of our networking services and resources including our game servers.

Rationale

There were multiple choices that we could have chosen, whether that be building our own datacenter, using a mix of cloud providers together, or 
The rationale for choosing AWS over the decision to use other cloud providers, or a mix of cloud providers is 

Status
Proposed

Consequences:

One negative consequence of going with one cloud provider is vendor lock in, most scripts and knowledge will be more AWS oriented and if AWS is having issues, it will take more effort or not be possible to fix and our service will be down.  