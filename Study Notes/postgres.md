List all databases available

```sql
\l
```

# Commands

## Switch to another database

\c databasename

## Create database:

CREATE DATABASE test;

## Drop databse

DROP DATABASE test;

## Creating db:

> createdb mydb

## Dropping database

> dropdb mydb

## List databases

> \l

## Switching to another database

> \c other_db_name

## Seeing all tables in a selected database

> \dt

## Seeing postgres version

> SELECT version();

## Seeing the previous executed command

> \g

## Listing all commands

> \?

## See the syntax for a command (like DROP TABLE)

> \h DROP TABLE

## Showing execution time

> \timimg

## Opening text editor to write query:

> \e

# Aggregate functions

- max
- min
- avg
- etc

# Foreign Keys

```sql

CREATE TABLE cities (
        city     varchar(80) primary key,
        location point
);

CREATE TABLE weather (
        city      varchar(80) references cities(city),
        temp_lo   int,
        temp_hi   int,
        prcp      real,
        date      date
);

```

# Transaction

```sql

BEGIN;
UPDATE accounts SET balance = balance - 100.00
    WHERE name = 'Alice';
-- etc etc
COMMIT;

```

# Window Function

A window function performs a calculation across a set of table rows that are somehow related to the current row.

```sql
SELECT depname, empno, salary, avg(salary) OVER (PARTITION BY depname) FROM empsalary;
```

# Inheritance

```sql
CREATE TABLE cities (
  name       text,
  population real,
  elevation  int     -- (in ft)
);

CREATE TABLE capitals (
  state      char(2)
) INHERITS (cities);


SELECT name, elevation
    FROM ONLY cities
    WHERE elevation > 500;


```
