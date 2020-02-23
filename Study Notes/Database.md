
# Uses of databases

* Data Sources
    * Transactions and records
    * Business applications
    * Acquire in batch and real time

* Raw Dump
    * Persis raw data
    * Machine logs
    * Text Streams, audio and video files

* Persisten Backup

* Master/Lookup Data

* Online Transaction Processing (OLTP)

* Processed Data
    * Write-once, read-many databases used for analytics
    * Summaries
    * Relationships

* Real-Time Cache
    * Keep "live" data
    * Shopping cart
    * Active State

* Scoreboard
    * Leaderboards
    * Real-time Snapshots
    * Stock trading

---

No single database product supports all requirements optimaly.
Choose the right database for your requirements.
You may use several databases for you project.

---

# Requirements

* Data Integrity
* Supported operations (joining, ordering, functions, etc)
* Modeling relationships
* Supported data types
* Transation support
* Scalability
* Redundancy (copies of the same data in case one is unavailable)
* Availability (how long is acceptable for data to be down)
* Schema flexibility
* Performance
* Integrations

---

# Terms

* HDFS (Hadoop Distributed File System)
* RDBMS (Relational Database Management System)
* Linear scaling
* Master data
* Full text search
* Kafka
* Raw Dumps
* Entity Analytics
* Entity Based Summaries
* Sharding

---

# Oracle Assessment

* Transactions
    * Ensures consistency and integrity
* Speed (for queries, optimizations, etc)
* Data integrity
* Security
* Sharded clusters

# Document Database

* JSON documents
* Flexible structures
* Document key
* Indexing
* Sharded clusters

## Popular Document databases:

* MongoDB
* Elasticsearch
* Couchdb

# MongoDB Assessment

* Pros
    * Complex data types
    * Rich querying
    * Full text search
    * Scalability

* Cons
    * No transactions
    * No media storage
    * Joins not optimal
    * No attribute-based security

* Applications
    * Blogs
    * Catalogs
    * RDBMS
    * Searchable repository

# Columnar Database

* Stored column by column
* Tables/column families
* Key driven

## Columnar Database types

### Cassandra

* Pros
    * CQL - like SQL
    * Optimal updates
    * Transactions
    * Scalability

* Cons
    * No joins
    * No order by
    * Query by key only
    * Only small blobs

* Applications
    * Data warehouse
    * Real-time counters
    * Customer 360
    * Write intensive apps
    * Machine Learning

# Key-Value Database

* Keys and values
* Access by keys
* Composite keys
* Memory caching
* Distributed

## Key-Value Database types

### Redis

* Pros
    * Ultrafast access
    * Rich data types
    * Auto-expire keys
    * Scalability

* Cons
    * No search on values
    * Small values only
    * Consistency across nodes
    * No tables

* Applications
    * Session cache
    * Shopping cart
    * Scorecard (live scoredcard)
    * Real-time queues

# Graph Database

* All about relationships
* Nodes and attributes
* Relationships and attributes
* Query by relationship
* Chaining of relationships

## Redis

* Pros
    * Transactions
    * Relation-based queries
    * Deep/complex relationships
    * Relation attributes

* Cons
    * No Complex data
    * No aggregations
    * No subqueries
    * Large volume queries

* Applications
    * Social media (relationship network)
    * Network topology
    * Recommendation engines
    * Location services
    * Search (search with relationships between the nodes)

---

# Use Cases


* HDFS (for raw dumps)
    * Is the best option to store raw log files.
    * Scalability
    * No schema
    * Backup
    * Streaming (a video can be played while still streaming from the database)
    * Redundancy and high availability
    * Data in any format
    * Large files

* Oracle (for summaries)
    * SQL capabilities
    * Lookup data
    * Third-party support
    * Speed

* Neo4j (for Node Analysis)
    * Relationship modeling
    * Node statistics
    * Link statistics
    * Failure predictions
    * Triage capabilities
    * User items (Recommendations)
    * Relationships (between nodes)
    * Deep queries

* MongoDB
    * Nested data
    * Information (video/audio information like views, likes, reviews, etc)
    * link to HDFS
    * User data

---

# Ecommerce Platform example

You may have a database for Video/audio, antoher for Items information, another for a shopping cart info, another for orders, recommendations, etc.

## MongoDB
Can be used for Items information, since it provides a flexible schema for different items with different fields.

## HDFS
Is good for storing large files, like video, audio, big files, etc.

## Redis
Is good for shopping cart. Key = Customer id. Value is List of items. Etc.

## Oracle
Is good for orders. OLTP. Data integrity. It supports relationship, transaction support, fast operations.

## Cassndra
Is good for customer analytics data. Key = Customer. Customer 360 view. Summarized data. Real-time access, to make real-time decisions for the customer when the customer is online.

## Neo4j
Is good for recommendations (from machine learning).


---








