# Elasticsearch

Elasticsearch is a distributed, RESTful search and analytics engine.

Uses JSON for data format.
For it's interface it uses HTTP.
Developed in Java. 

## The Elastic Stack, or ELK stack

* Logstash
  * Get the data and feeds it to Elasticsearch
* Beats 
  * Get the data and feeds it to Elasticsearch 
* Elastic Search
  * Get the data and destributes it through nodes on the cluster
* Kibana 
  * Web user interface

Outside of the ELK stack you have the X-Pack, which includes things like Security, Alerting, Monitoring, Reporting, Graph, etc.

## Advantages

* Scalability (horizontal)
* Near Real-Time results
* Schemaless, since is no SQL
* Advanced Query Lenguage

## ES User Cases

* Security/log analytics
* Marketing (analize user data)
* Operations
* Search
  
## Concepts

A Cluster is a collection of nodes.

A Node stores the data.
A Node has an Index.
Inside an index you have a Type.
Document in JSON format that recide in an Index.

The index needs to be distributed to be scalable.
For this, the index can be broken into Shards and Replica.
A Replica is a segment of the index.
An Shard is a portion of that index.

5 Shards and 1 replica.


