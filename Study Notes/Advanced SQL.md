# SQL

## Terms

- Execution plan
- Scanning vs Indexes
- Full table scan
-

## Joins

1. Nested Loop Join
2. Hash Join
3. Sort Merge Join

## Partitions

Device a table into smaller tables.
With a partition key that could be based on time. So you can only scan one that is from, example, Mar 2019 when you know the record belongs to that month and year.
Also, you can have sub indices for them.

## Explain and Analyze

Only shows the query plan:

> EXPLAIN SELECT \* FROM ACCOUNT_ADDRESS;

Shows the query plan and executes the query to check the planning time and how long it took:

> EXPLAIN ANALYZE SELECT \* FROM ACCOUNT_ADDRESS;

It shows a cost, rows and width. The rows and width mean how big the data is.
If you select a single column, the width will be less.

## Indices

Postgres creates a B-Tree index by default when creating an index.

Postgres doesn't allow to create a bitmap index manually. It creates it whenever it knows it's best to.

To create a Hash index in Postgres, do:

> CREATE INDEX idx_email on staff USING HASH (email);

## Tuning Joins

When running joins, Postgres does some optimizations where it sees fit.
Now, to turn of some of those optimizations:

> set enable_nestedloop=true;
> set enable_hashjoin=false;
> set enable_mergejoin=false;

Run the EXPLAIN query and then check the type of join it did.

## Partitioning Data

- Horizontal partitioning
- Vertical partitioning

You can partition a table and use it like many tables.
They can have their on indices, constraints, defaults, etc.

```sql

CREATE TABLE iot_measurement(location_id int not null, measure_data data not null)
PARTITION BY RANGE (measure_data);

-- Then

CREATE TABLE iot_measurement_wk1_2019 PARTITION OF iot_measurement FOR VALUES FROM
('2019-01-01') TO ('2019-01-08');

CREATE TABLE iot_measurement_wk1_2019 PARTITION OF iot_measurement FOR VALUES FROM
('2019-01-08') TO ('2019-01-15');

-- You should then see a new node called Partitions present in the table nodes.

-- You can partition a table by Range, List, Hash.

PARTITION BY RANGE...


...PARTITION BY LIST(product_category)
...FOR VALUES IN ('cat1', 'cat2')

...PARTITION BY HASH(col)
...FOR VALUES WITH (MODULUS 5, REMAINDER 0)

```

## Materialized Views

This will save the records of a query as a copy.

```sql

CREATE MATERIALIZED VIEW my_staff AS...

```

## Hints

SELECT /_+ INDEX(sales_transaction st_cust_idx) +_/
...

Is a way to give postgres a hint on what indices to use.
