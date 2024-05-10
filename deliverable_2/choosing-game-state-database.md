# ADR 4: Choosing NoSQL as our game state storage database

As players perform actions, finish matches, score, level up, use inventory, have specific customization, etc we need to store and retrieve their data in a database.  The database should be available and scalable and be able to receive a large amount of reads and writes as player information and actions may change frequently, but also will require player information to be up-to-date from game to game.  

# Decision

We have decided to use a NoSQL database to store player information, inventory, actions, etc.

# Rationale

There were a few choices that we considered for our database and that was whether we should go with a NoSQL database or SQL database.

First we looked at NoSQL databases such as MongoDB and DynamoDB (one being cloud provider specific), their main advantages being their document based models (JSON) and high horizontal scalability, with options for strong or eventually consistent data options.  The document model would allow us to change information much more freely, without needing to edit table models like in SQL, but needing to build relational information into data model could lead to messy collections and issues in data.  Depending on databases, consistency is a setting and can be changed to be strongly consistent or not, but the more consistent you need your data, write speeds are affected.

Next we looked at relational databases such as MySQL, PostgresSQL, and Amazon Aurora.  Relational databases use SQL, are ACID compliant, and consistent when data is written to them, but their restriction is based on their data model being much more strict and potential issues around unstructured data, but performance is usually better than their NoSQL counterparts when trying to relate data together.  Also data integrity, for SQL databases things like constraints and primary/foreign keys allow for data to be kept intact easily, while because of the nature of NoSQL DBs (mainly JSON documents), the service writing to the DB needs to be generally more aware of updating and deleting data.

Most of the data stored in our game, may come in different form and events and have the flexibility of a document style database allows teams to write their data more freely.  Where as using SQL managing tables and either using unstructured table formats or changing schema would be more difficult.

# Status

Proposed

# Consequences


Positive Consequences:

- Many AWS options, whether built in to AWS (DynamoDB) and many open source options to choose from that are supported in cloud services 
- Great performance and constantly updated with new features, with a large community and plugins for many databases
- Tables are unstructured which allows for easier data changes and additions
- Scalable infrastructure is standard for many databases
- Large community of documentation for many databases


Negative Consequences:

- Data management may be more intensive as relating data can be more difficult
- Has less data integrity and application must make sure it is updating or using data correctly, more calls may be needed to keep data intact