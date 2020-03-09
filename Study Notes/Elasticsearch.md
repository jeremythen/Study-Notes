# Elasticsearch

Elasticsearch is a distributed, RESTful search and analytics engine.

Uses JSON for data format.
For it's interface it uses HTTP.
Developed in Java. 

## Terms

* Index pattern
* Tokenizers and analyzers
* "aggs" (aggregation)
* percentiles 

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


# Using Kibana

To create request with Kibana, you basically use REST calls:

\<REST Verb> \<Index>

```
PUT sales
GET sales
DELETE sales
```

## Kibana Operations

### Check cluster health

```
GET _cat/health?v
```

### Check the nodes

```
GET _cat/nodes?v
```

### Check indeces

```
GET _cat/indices?v
```

---

### Add an index sales

```
PUT /sales
```

### Add a document to that index sales

```json
PUT /sales/order/123
{
  "orderId": "123",
  "orderAmmount":"500"
}
```

### Get that document

```
GET /sales/order/123
```

### Delete an idx

```
DELETE sales
```

## Bulk API

### Bulk load from cURL:
Where 'reqs' is the file name with the json data

```
curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/_bulk --data-binary "@reqs"; echo
```
Print pretty, specifying the index and type

```
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/bank/account/_bulk?pretty' --data-binary @accounts.json
```

### Bulk load from the Kibana console

```
POST _bulk
jsondata
```

```json
POST _bulk
{ "index" : { "_index" : "my-test-console", "_type" : "my-type", "_id" : "1" } }
{ "col1" : "val1" }
{ "index" : { "_index" : "my-test-console", "_type" : "my-type", "_id" : "2" } }
{ "col1" : "val2"}
{ "index" : { "_index" : "my-test-console", "_type" : "my-type", "_id" : "3" } }
{ "col1" : "val3" }

GET /my-test-console/my-type/1
```

### Show indices with regex

```
GET _cat/indices/logstash*
```

### Getting records with constraints

```json
GET bank/_search
{
  "query": {
    "match": {
      "state": "FL"
    }
  }
}
```
### Getting data with multiple constaints

```json
GET bank/_search
{
  "query": {
    "bool": {
      "must": [ ## or "must_not" to negate it.
      {
        "match": {
          "state": "CA
          "
        }
      },
      {
        "match": {
          "employer": "Techade"
        }
      }
    ]
    }
  }
}
```

### To get data and specify importance and relevance with 'should'

```json
GET bank/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "match": {
            "state": "CA"
          }
        },
        {
          "match": {
            "lastname": {"query": "Smith", "boost": 3}
          }
        }
      ]
    }
  }
}
```

### A term query

```json
GET bank/_search
{
  "query": {
    "term": {
      "balance": 44940
    }
  }
}
```

### A terms query

```json
GET bank/_search
{
  "query": {
    "terms": {
      "balance": [516, 851]
    }
  }
}
```

### A range query
```json
GET bank/_search
{
  "query": {
    "range": {
      "account_number": {
        "gte": 516,
        "lte": 851,
        "boost": 2
      }
    }
  }
}


GET bank/_search
{
  "query": {
    "range": {
      "age": {
        "gte": 35
      }
    }
  }
}

```

## Data types

### Core


### Complex


### Geo

### Specialized


## Notes

KIBANA uses New Line JSON to load data.
Array stores complex data

* A "term" query only searches keywords and numeric values
* "match" is for text field.
* 


## Tokenizer

```json


GET bank/_analyze
{
  "tokenizer": "standard",
  "text": "The Moon is Made of Cheese Some Say"
}

GET bank/_analyze
{
  "tokenizer": "standard",
  "text": "The Moon-is-Made of Cheese.Some Say$"
}

GET bank/_analyze
{
  "tokenizer": "letter",
  "text": "The Moon-is-Made of Cheese.Some Say$"
}

GET bank/_analyze
{
  "tokenizer": "standard",
  "text": "you@example.com login at https://bensullins.com attempt"
}

GET bank/_analyze
{
  "tokenizer": "uax_url_email",
  "text": "you@example.com login at https://bensullins.com attempt"
}


```

## Aggregates

```json
# Count of Accounts by State
# Must be keyword field
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# Add average balance in each state
# Nesting the metric inside the agg
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "avg_bal": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}

# Breakdown further with Nesting
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "avg_bal": {
          "avg": {
            "field": "balance"
          }
        },
        "gender":{
          "terms": {
            "field": "gender.keyword"
          }
        }
      }
    }
  }
}

# Add avg_price metric to lowest level
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "avg_bal": {
          "avg": {
            "field": "balance"
          }
        },
        "gender":{
          "terms": {
            "field": "gender.keyword"
          },
          "aggs": {"avg_bal": {"avg": {"field": "balance"} }
          }
        }
      }
    }
  }
}


## Get stats about bank balances
## Size=1 to omit search results
GET bank/account/_search
{
  "size": 1,
  "aggs": {
    "balance-stats": {
      "stats": {
        "field": "balance"
      }
    }
  }
}


# Count of Accounts by State
# Must be keyword field
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# This is the equivalent of using match_all
GET bank/account/_search
{
  "size": 0,
  "query": {
    "match_all": {}
  },
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# Aggs work in the context of the query, so apply a filter like normal
GET bank/account/_search
{
  "size": 0,
  "query": {
    "match": {
      "state.keyword": "CA"
    }
  },
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# You can also filter on terms
GET bank/account/_search
{
  "size": 0,
  "query": {
    "bool": {
      "must": [
        {"match": {"state.keyword": "CA"}},
        {"range": {"age": {"gt": 35}}}
      ]
    }
  },
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# Lets add a metric back in
GET bank/account/_search
{
  "size": 0,
  "query": {
    "bool": {
      "must": [
        {"match": {"state.keyword": "CA"}},
        {"range": {"age": {"gt": 35}}}
      ]
    }
  },
  "aggs": {
    "states": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {"avg_bal": {"avg": {"field": "balance"} }}
    }
  }
}

# You can also just filter the results
GET bank/account/_search
{
  "size": 0,
  "query": {
    "match": {"state.keyword": "CA"}
  },
  "aggs": {
    "over35":{
      "filter": {
        "range": {"age": {"gt": 35}}
      },
    "aggs": {"avg_bal": {"avg": {"field": "balance"} }}
    }
  }
}


# Look at state avg and global average
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "state_avg": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {"avg_bal": {"avg": {"field": "balance"}}}
    },
    "global_avg": {
      "global": {},
      "aggs": {"avg_bal": {"avg": {"field": "balance"}}}
    }
  }
}


```

## Percentiles


```json

# Look at the percentiles for the balances
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "pct_balances": {
      "percentiles": {
        "field": "balance",
        "percents": [
          1,
          5,
          25,
          50,
          75,
          95,
          99
        ]
      }
    }
  }
}

# Can also calculate High Dynamic Range (HDR) Historgram
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "pct_balances": {
      "percentiles": {
        "field": "balance",
        "percents": [
          1,
          5,
          25,
          50,
          75,
          95,
          99
        ],
        "hdr": {
          "number_of_significant_value_digits": 3
        }
      }
    }
  }
}

# We can use the percentile ranks agg for checking a individual values
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "bal_outlier": {
      "percentile_ranks": {
        "field": "balance",
        "values": [35000,50000],
        "hdr": {
          "number_of_significant_value_digits": 3
        }
      }
    }
  }
}

# Similarly we can create a histogram
GET bank/account/_search
{
  "size": 0,
  "aggs": {
    "bals": {
      "histogram": {
        "field": "balance",
        "interval": 500
      }
    }
  }
}


```

