# ADR 4: Choosing NoSQL as our game state storage database

As players perform actions, finish matches, score, level up, use inventory, have specific customization, etc we need to store and retrieve their data in a database.  The database should be available and scalable and be able to receive a large amount of reads and writes as player information and actions may change frequently, but also will require player information to be up-to-date from game to game.

# Decision

We have decided to use a NoSQL database, to store game server events and update including player information, inventory, actions, etc.

# Rationale

There were a few choices that we considered for our player data database and that was whether we should go with a NoSQL database or SQL database.

First we looked at relational databases such as MySQL, PostgresSQL, and Amazon Aurora.  Relational databases use SQL, are ACID compliant, and consistent when data is written to them, but their restriction is based on their data model being much more strict and potential issues around unstructured data, but performance is usually better than their NoSQL counterparts when trying to relate data together.  Also data integrity, for SQL databases, implements things like constraints and primary/foreign keys and allow for data to be kept intact easily.

Next we looked at NoSQL databases such as MongoDB and DynamoDB (one being cloud provider specific), their main advantages being their many types of data models supported, for instance document based models (JSON) or key value models, or  and high horizontal scalability, with options for strong or eventually consistent data options.  The document model would allow us to change information much more freely, without needing to edit table models like in SQL, but needing to build relational information into data model could lead to messy collections and issues in data.  Depending on databases, consistency is a setting and can be changed to be strongly consistent or not, but the more consistent you need your data, write speeds are affected.

The main factors that lead to us choosing NoSQL database:

- Flexibility: Many types of databases allow us to have many different data model types in a single collection, for instance items with different attributes or properties we could add at any time and allows developers to add new fields as they choose.
- Scalability: NoSQL databases of many types, allow for more horizontal scalability and adding servers to service our load should be easier
- Consistency Settings: Many types of NoSQL databases allow some flexibility in writing consistency between databases, which gives us options to how we read and write player information
- Documentation and Support: Many developers know document style databases, the most popular ones whether managed or community versions have large amount of documentation, so learning and examples should be abundant
- Deployment Options: We can manage ourselves or go with cloud providers options
- Latency: NoSQL databases gives us many options around latency and many of the types are known for low latency operations

# Status

Proposed

# Consequences


Positive Consequences:

- Many AWS options, whether built in to AWS (DynamoDB) and many open source options to choose from that are supported in cloud services 
- Tables are unstructured which allows for easier data changes and additions, with less maintenance required around replication
- Scalable infrastructure is standard for many databases of this type, easier to add replication shards and servers to environment, with better write performance generally than SQL DBs
- Large community of documentation for many databases
- Many settings around consistency and ACID operations in general for many databases, can change requirements and performance targets if needed


Negative Consequences:

- Data management may be more intensive as relating data can be more difficult
- Has less data integrity and application must make sure it is updating or using data correctly, more calls may be needed to keep data intact
- Because of consistency, if our game requires the need for all replicas to have up to date information, may need to design more architecture to support that
- Many languages or styles to learn depending on database, SQL is standard on their database type, while many layers of NoSQL may require wholly different ways of interacting with them
