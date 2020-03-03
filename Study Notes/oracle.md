

- [Terms](#terms)
- [Inline View](#inline-view)
  - [Example](#example)
- [Notes](#notes)
  - [ANY clause](#any-clause)
  - [INTERSECT](#intersect)
  - [MINUS](#minus)
  - [Grouping set](#grouping-set)
  - [DECODE](#decode)
  - [Disabling and Enabling constraints](#disabling-and-enabling-constraints)
  - [Adding multiple columns at the same time](#adding-multiple-columns-at-the-same-time)
  - [Modifying a column](#modifying-a-column)
  - [Dropping one or multiple columns](#dropping-one-or-multiple-columns)
  - [Renaiming columns and tables](#renaiming-columns-and-tables)
  - [See all metadata of tables and columns](#see-all-metadata-of-tables-and-columns)
  - [Misc](#misc)
  - [Replacing records](#replacing-records)
  - [Create column from other columns (virtual columns)](#create-column-from-other-columns-virtual-columns)
  - [Make column invisible](#make-column-invisible)
    - [Remove invisible (UNUSED) columns](#remove-invisible-unused-columns)
    - [See all (insivible) UNUSED columns](#see-all-insivible-unused-columns)
  - [See all constraints and constraints columns](#see-all-constraints-and-constraints-columns)
  - [FOREIGN KEY that Cascades](#foreign-key-that-cascades)
  - [Dropping tables with constraints](#dropping-tables-with-constraints)
  - [See all tables](#see-all-tables)
  - [Delete all data from a table, but not the rows (TRUNCATE)](#delete-all-data-from-a-table-but-not-the-rows-truncate)
  - [INSERT ALL](#insert-all)
    - [INSERT ALL all from a subquery:](#insert-all-all-from-a-subquery)
    - [INSERT ALL from literal values:](#insert-all-from-literal-values)
    - [INSERT ALL multiple rows into multiple tables:](#insert-all-multiple-rows-into-multiple-tables)
    - [INSERT ALL based on some conditions:](#insert-all-based-on-some-conditions)
- [INDICES](#indices)
  - [Function-based Index](#function-based-index)
- [Oracle Bitmap Index](#oracle-bitmap-index)
- [Synonym](#synonym)
- [Sequence](#sequence)
  - [Usage:](#usage)
    - [Get the next value](#get-the-next-value)
    - [Get the current value](#get-the-current-value)
    - [Get the next 5 values](#get-the-next-5-values)
    - [Insert with sequence](#insert-with-sequence)
    - [Used in PL/SQL](#used-in-plsql)
    - [Altering the sequence](#altering-the-sequence)
    - [Drop the sequence](#drop-the-sequence)
    - [Grant privileges](#grant-privileges)


# Terms

* Execution plan
* Low Cardinality

# Inline View

A subquery which is nested within the FROM clause of the SELECT statement is called an inline view.
A subquery nested in the WHERE clause of the SELECT statement is called a nested subquery.

Oracle correlated subquery which is a subquery whose some clauses refer to the column expressions in the outer query.

Oracle allows you to have an unlimited number of subquery levels in the FROM clause of the top-level query and up to 255 subquery levels in the WHERE clause.

## Example

```sql
CREATE TABLE customers_archive AS SELECT *...
```

# Notes

## ANY clause

list_price != ANY(...

You can use any comparison operator with the ANY clause. <>, !=, =, >, <, >=, <=, etc.

ANY(list), ANY(20, 55, 10), ANY(SUBQUERY), ETC.

When using ANY(subquery), if the subquery returns no record, then the ANY will return false and no record will be returned to the outter query.

When using ALL(subquery), if the subquery returns no record, then the ALL will return true anyways and all the records from the outter query will be returned.

## INTERSECT

INTERSECT, used like UNION, returns the records found in both tables.

## MINUS

MINUS, used like UNION and INTERSECT, returns all records from the left table that don't exist int the right table.

## Grouping set

A grouping set are a unique set of values used to group other values. Used with the group by clause to group them.

## DECODE

DECODE(1, 1, 'ONE', 'NOT ONE'), is like if 1 == 1 then return 'ONE', else return 'NOT ONE'

DECODE(3, 1, 'One',  2, 'Two', 'Not one or two'), this is like the IF ELSIF ELSE clause

DECODE(country_id, 'US','United States', 'UK', 'United Kingdom', 'JP','Japan'
  , 'CA', 'Canada', 'CH','Switzerland', 'IT', 'Italy', country_id)

## Disabling and Enabling constraints


```sql
ALTER TABLE DISABLE CONSTRAINT customconstraint;
ALTER TABLE ENABLE CONSTRAINT customconstraint;
```

## Adding multiple columns at the same time

```sql
ALTER TABLE persons 
ADD (
    phone VARCHAR(20),
    email VARCHAR(100)
); --------------------------------- To add multiple new columns.
```

## Modifying a column

```sql
ALTER TABLE persons MODIFY phone VARCHAR(10)...

ALTER TABLE table_name
MODIFY (
    column_name_1 action,
    column_name_2 action,
    ...
);
```

## Dropping one or multiple columns

```sql
ALTER TABLE persons DROP COLUMN phone...

ALTER TABLE persons DROP (email, phone)
```
## Renaiming columns and tables

```sql
ALTER TABLE persons RENAME COLUMN email TO user_email;

ALTER TABLE persons RENAME TO thepersons; --- renames the table itseft.
```

## See all metadata of tables and columns

```sql
select * from user_tab_cols; --- saves the metadata of all tables and columns.
```

## Misc

DESC stands for DESCRIBE:

DESCRIBE ot.employees; -- is good

You can modify columns to be visible or invisible.

## Replacing records

```sql
UPDATE
    accounts
SET
    phone = REPLACE(phone, '+1-', '');
```

## Create column from other columns (virtual columns)

column_name [data_type] [GENERATED ALWAYS] AS (expression) [VIRTUAL]

```sql
full_name VARCHAR2(110) GENERATED ALWAYS AS (name || ', ' || last_name)); --- Virtual column
```

## Make column invisible

```sql
ALTER TABLE table_name SET UNUSED COLUMN column_name; --- column_name will not be visible anymore. Like a logical drop.
```

### Remove invisible (UNUSED) columns

```sql
ALTER TABLE table_name DROP UNUSED COLUMNS; --- will delete all the columns previously marked as UNUSED.
```

### See all (insivible) UNUSED columns

```sql
SELECT * FROM DBA_UNUSED_COL_TABS; --- To see all the UNUSED columns.   
```

## See all constraints and constraints columns

```sql
SELECT * FROM all_constraints;
SELECT * FROM all_cons_columns;
```

## FOREIGN KEY that Cascades

```sql
FOREIGN KEY (brand_id) REFERENCES brands(brand_id) ON DELETE CASCADE;
```

## Dropping tables with constraints

```sql
drop table ot.brands cascade constraints; --- Will drop this table and the constraints they any other table may have on it, but not other records.
```

## See all tables

```sql
select * from all_tables;
```

## Delete all data from a table, but not the rows (TRUNCATE)

```sql
TRUNCATE TABLE quotations CASCADE; --- TRUNCATE deletes all rows data from a table faster than DELETE;
```

## INSERT ALL

### INSERT ALL all from a subquery:

```sql
INSERT ALL
    INTO table_name(col1,col2,col3) VALUES(val1,val2, val3)
    INTO table_name(col1,col2,col3) VALUES(val4,val5, val6)
    INTO table_name(col1,col2,col3) VALUES(val7,val8, val9)
subquery;
```

### INSERT ALL from literal values:

```sql
INSERT ALL 
    INTO fruits(fruit_name, color)
    VALUES ('Apple','Red') 
 
    INTO fruits(fruit_name, color)
    VALUES ('Orange','Orange') 
 
    INTO fruits(fruit_name, color)
    VALUES ('Banana','Yellow')
SELECT 1 FROM dual; ---------------- Where dual is a dummy table;
```

### INSERT ALL multiple rows into multiple tables:

```sql
INSERT ALL
    INTO table_name1(col1,col2,col3) VALUES(val1,val2, val3)
    INTO table_name2(col1,col2,col3) VALUES(val4,val5, val6)
    INTO table_name3(col1,col2,col3) VALUES(val7,val8, val9)
Subquery;
```

### INSERT ALL based on some conditions:

```sql
INSERT [ ALL | FIRST ] ------------------------- ALL checks all conditions any ways. FIRST when meets a conditions, inserts and breaks;
    WHEN condition1 THEN
        INTO table_1 (column_list ) VALUES (value_list)
    WHEN condition2 THEN 
        INTO table_2(column_list ) VALUES (value_list)
    ELSE
        INTO table_3(column_list ) VALUES (value_list)
Subquery
```

# INDICES

For primary keys, Oracle creates an index automatically. If you want an index for any other specific column:

* Creating an index
  
```sql
 CREATE INDEX members_last_name_i ON members(last_name);
```

* Dropping an index
  
```sql
DROP INDEX index_name;
```

* Index on multiple columns
  
```sql
CREATE INDEX members_name_i ON members(last_name,first_name);
```

* Creating unique indices
  
```sql
CREATE UNIQUE INDEX members_email_i ON members(email);
```

## Function-based Index

```sql
* CREATE INDEX members_last_name_fi ON members(UPPER(last_name));
```

* If you create a normal index for a column and a function is used while creating a query with it, the index will not work because the function (like UPPER(last_name) will return a different result that the value the index has). To solve this, use Function-based Indices.
* Keep in mind that a function-based index will make Oracle call that function for each record on that column and save it as index values. _fi


# Oracle Bitmap Index

* Is an index based on an array bitmap.
* Is special for low cardinate columns (columns with few types of values)

```sql
CREATE BITMAP INDEX members_gender_i ON members(gender);
```

# Synonym

Synonyms help specify an alias for an object (table). For security, to simplify the name, for backward compatibility, etc.

Syntax:

```sql
CREATE [OR REPLACE] [PUBLIC] SYNONYM schema.synonym_name
FOR schema.object;
```

Example:

```sql
CREATE SYNONYM stocks FOR inventories;
```

Drop it:

```sql
DROP SYNONYM schema.synonym_name FORCE;
```

Examples:

```sql
DROP PUBLIC SYNONYM synonym_name FORCE;
```

```sql
DROP SYNONYM stocks;
```

# Sequence

Create a sequence:

```sql
CREATE SEQUENCE item_seq;
```
## Usage:

### Get the next value
```sql
SELECT item_seq.NEXTVAL FROM dual;
```

### Get the current value

```sql
SELECT item_seq.CURRVAL
FROM dual;
```

### Get the next 5 values

```sql
SELECT item_seq.NEXTVAL
FROM   dual
CONNECT BY level <= 5;
```

### Insert with sequence

```sql
INSERT INTO items(item_id) VALUES(item_seq.NEXTVAL);
```

### Used in PL/SQL

```
v_seq  := item_seq.NEXTVAL;
```

### Altering the sequence
  
  ```sql
  ALTER SEQUENCE item_seq MAXVALUE 100;
  ```

 ### Drop the sequence

```sql
DROP SEQUENCE item_seq;
```

### Grant privileges
  
```sql
GRANT CREATE SEQUENCE 
TO user_name;
```

```sql
GRANT CREATE ANY SEQUENCE, 
    ALTER ANY SEQUENCE, 
    DROP ANY SEQUENCE, 
    SELECT ANY SEQUENCE 
TO user_name;
```

```sql
GRANT SELECT ON user_name.sequence_name 
TO another_user;
```