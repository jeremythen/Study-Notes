
- [Cache](#cache)
  - [Terms](#terms)
  - [Types of Cache](#types-of-cache)
  - [Cache Invalidation](#cache-invalidation)
    - [Types](#types)
  - [Cache Eviction Policies](#cache-eviction-policies)
    - [Types of data structure to implement](#types-of-data-structure-to-implement)
- [Sharding](#sharding)
  - [Sharding Methods](#sharding-methods)
  - [Sharding Criteria](#sharding-criteria)
  - [Sharding Challenges](#sharding-challenges)
  

# Cache

Is a way to store data that is used a lot and/or requires same computation, so it can be served faster.

## Terms

* Cache miss

## Types of Cache

* Application Server Cache
* Distributed Cache
  *  Distributed for multiple nodes with load balancers
* Global Cache
* CDN
  * Content Distribution Network, to serve static media that is common to all.

## Cache Invalidation

A way to realize when to invalidate the cached data. When the data is no longer needed or when it changed. Keeping important data.
When the data is modified in DB, it should be invalidated in the cache.

### Types

* Write-through Cache
    * Data is written to cache and DB at the same time
* Write Around Cache
    * Store data to DB and not the Cache
* Write Back Cache
    * Data stored to cache and later to DB.
  
## Cache Eviction Policies

Deciding when to remove data from the cache, or the maximun size of data that will be allowed in that structure and decide which data will be removed from it.

### Types of data structure to implement

* FIFO
* LIFO
* LRU
* Most Recently Used
* Least Frequently Used
* Random Replacement


# Sharding

Sharding is deviding the data on multiple smaller chunks.
Like a file of 1gb, can be broken down to 4 files of 250mb.

## Sharding Methods

* Horizontal partitioning
  * Putting different rows into different Bs.
  * Range based Sharding, by number or alphabetically, etc.
* Vertical Partitioning
  * Devide tables based on features, like 1 for user, 1 for location, instead of 1 for both.
* Directory based Partitioning


## Sharding Criteria

* Hash based
  * Using hashcode on any entity value
* List Partitioning
  * Based on List. List, for each country you can have a table or DB to serve them important information for them
* Round-Robin Partitioning
  * Info on 1st db, another info on 2nd db, etc.
* Composite Partitioning
  * Combining any above schemes

## Sharding Challenges

* ACID Compliance
* Joins Inefficient

