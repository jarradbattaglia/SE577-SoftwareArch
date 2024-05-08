# ADR 4: Choosing PostgreSQ: as our game state storage database

As players perform actions, level up, use inventory and have specific customization we need to store and retrieve their data in a database.  The database should be available and scalable and be able to receive a large amount of writes as player information may change frequently.  

# Decision

We have decided to use the Postgresql database as our database to store player information, inventory, etc.

# Rationale

There were a few choices that we considered for our database and that was whether we should go with a NoSQL database or SQL database and whether we should go with their vendor given options.  They both offer their own issues and advantages.

First we looked at NoSQL databases such as MongoDB and DynamoDB (one being cloud provider specific), their main advantages being their document based models (JSON) and high scalability, with options for strong or eventually consistent data options.  Also the document model would allow us to change information much more freely, without needing to edit table models like in SQL, but needing to build relational information into data model could lead to messy collections and issues in data.  Also an issue around consistency is that it is an option and write speeds are affected the more consistency is required of the data.  DynamoDB in contrast to MongoDB is run as an AWS service and offers built in scalability and management, but at a cost and vendor lock in, while MongoDB is offered as an option to deploy, but requires more management of its resources.  

Next we looked at relational databases such as MySQL, PostgresSQL, and Amazon Aurora.  Relational databases use SQL, are ACID compliant, and consistent when data is written to them, but their restriction is based on their data model being much more strict and potential issues around unstructured data, but performance is usually better than their NoSQL counterparts.  Options like Amazon Aurora, like DynamoDB, offer built in management of resources, but for a large cost.  Options like MySQl or Postgres require more management and documentation knowledge (though AWS options are available).  Historically MySQL was seen as more scalable as PostgreSQL, but in recent years postgres has added more features around JSON integration and replication/scalability, while being known as more performant.

# Status

Proposed

# Consequences


Positive Consequences:

- Freely able to move to other services compared to vendor options, and potentially cheaper than managed options
- Great performance and constantly updated with new features, with a large community and plugins
- It is ACID compliant, while being more performant than NOSQL counterparts and other SQL databases, with SQL query language being more well known.
- Easy to move to other SQL technologies, even managed ones if we so choose
- Tables are structured with built in data integrity options and offer options for unstructured data like JSON
- Large community of documentation and frequent updates



Negative Consequences:

- More management of resources compared to a built-in vendor option
- Data management may be more intensive, as large changes to data models may lead to more database maintenance and table changes or our use of unstructured data
- Potential issues around Postgres scalability, typically relies on more resources given to the server itself instead of adding more servers to the cluster, though this issue has been worked on in recent years