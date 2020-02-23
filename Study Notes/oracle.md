
Having filters groups of rows.
Where filters rows.

--------------------------

A subquery which is nested within the FROM clause of the SELECT statement is called an inline view.
A subquery nested in the WHERE clause of the SELECT statement is called a nested subquery.

Oracle correlated subquery which is a subquery whose some clauses refer to the column expressions in the outer query.

-------------------

Oracle allows you to have an unlimited number of subquery levels in the FROM clause of the top-level query and up to 255 subquery levels in the WHERE clause.

--------------

CREATE TABLE customers_archive AS SELECT *...

------------

list_price != ANY(...

You can use any comparison operator with the ANY clause. <>, !=, =, >, <, >=, <=, etc.

ANY(list), ANY(20, 55, 10), ANY(SUBQUERY), ETC.

---


When using ANY(subquery), if the subquery returns no record, then the ANY will return false and no record will be returned to the outter query.

When using ALL(subquery), if the subquery returns no record, then the ALL will return true anyways and all the records from the outter query will be returned.

--------------------

INTERSECT, used like UNION, returns the records found in both tables.

---

MINUS, used like UNION and INTERSECT, returns all records from the left table that don't exist int the right table.

--------------------

A grouping set are a unique set of values used to group other values. Used with the group by clause to group them.

------------------------

DECODE(1, 1, 'ONE', 'NOT ONE'), is like if 1 == 1 then return 'ONE', else return 'NOT ONE'

----
DECODE(3, 1, 'One',  2, 'Two', 'Not one or two'), this is like the IF ELSIF ELSE clause

----

DECODE(country_id, 'US','United States', 'UK', 'United Kingdom', 'JP','Japan'
  , 'CA', 'Canada', 'CH','Switzerland', 'IT', 'Italy', country_id)

---

IF 2 = 1 THEN 
     RETURN 'One';
ELSIF 2 = 2 THEN 
    RETURN 'Two';
END IF;

-------------------------

ALTER TABLE DISABLE CONSTRAINT customconstraint;
ALTER TABLE ENABLE CONSTRAINT customconstraint;

ALTER TABLE persons 
ADD (
    phone VARCHAR(20),
    email VARCHAR(100)
); --------------------------------- To add multiple new columns.


ALTER TABLE persons MODIFY phone VARCHAR(10)...

ALTER TABLE table_name
MODIFY (
    column_name_1 action,
    column_name_2 action,
    ...
);

ALTER TABLE persons DROP COLUMN phone...

ALTER TABLE persons DROP (email, phone)

ALTER TABLE persons RENAME COLUMN email TO user_email;

ALTER TABLE persons RENAME TO thepersons; --- renames the table itseft.

---

select * from user_tab_cols; --- saves the metadata of all tables and columns.

---

DESC stands for DESCRIBE:

DESCRIBE ot.employees; -- is good

---

You can modify columns to be visible or invisible.

---

UPDATE
    accounts
SET
    phone = REPLACE( ---------------- Use the REPLACE function.
        phone,
        '+1-',
        ''
    );


---

full_name VARCHAR2(110) GENERATED ALWAYS AS (name || ', ' || last_name)); --- Virtual column

column_name [data_type] [GENERATED ALWAYS] AS (expression) [VIRTUAL]

---

ALTER TABLE table_name SET UNUSED COLUMN column_name; --- column_name will not be visible anymore. Like a logical drop.
ALTER TABLE table_name DROP UNUSED COLUMNS; --- will delete all the columns previously marked as UNUSED.

---

SELECT * FROM DBA_UNUSED_COL_TABS; --- To see all the UNUSED columns.   


---

SELECT * FROM all_constraints;
SELECT * FROM all_cons_columns;

--- 

FOREIGN KEY (brand_id) REFERENCES brands(brand_id) ON DELETE CASCADE;

---

drop table ot.brands cascade constraints; --- Will drop this table and the constraints they any other table may have on it, but not other records.

---


select * from all_tables;


---

TRUNCATE TABLE quotations CASCADE; --- TRUNCATE deletes all rows data from a table faster than DELETE;

---

Insert all at the same time. The values must come from the subquery:

INSERT ALL
    INTO table_name(col1,col2,col3) VALUES(val1,val2, val3)
    INTO table_name(col1,col2,col3) VALUES(val4,val5, val6)
    INTO table_name(col1,col2,col3) VALUES(val7,val8, val9)
subquery;


Or the values can come from literal values:

INSERT ALL 
    INTO fruits(fruit_name, color)
    VALUES ('Apple','Red') 
 
    INTO fruits(fruit_name, color)
    VALUES ('Orange','Orange') 
 
    INTO fruits(fruit_name, color)
    VALUES ('Banana','Yellow')
SELECT 1 FROM dual; ---------------- Where dual is a dummy table;


Multiple rows into multiple tables:

INSERT ALL
    INTO table_name1(col1,col2,col3) VALUES(val1,val2, val3)
    INTO table_name2(col1,col2,col3) VALUES(val4,val5, val6)
    INTO table_name3(col1,col2,col3) VALUES(val7,val8, val9)
Subquery;


Or based on some conditions:

INSERT [ ALL | FIRST ] ------------------------- ALL checks all conditions any ways. FIRST when meets a conditions, inserts and breaks;
    WHEN condition1 THEN
        INTO table_1 (column_list ) VALUES (value_list)
    WHEN condition2 THEN 
        INTO table_2(column_list ) VALUES (value_list)
    ELSE
        INTO table_3(column_list ) VALUES (value_list)
Subquery

---

CREATE PUBLIC SYNONYM sales FOR lion.sales; 


---

DROP SYNONYM schema.synonym_name FORCE;
DROP PUBLIC SYNONYM synonym_name FORCE;

---


 CREATE SEQUENCE item_seq;
 
INSERT INTO items(item_id) VALUES(item_seq.NEXTVAL);
INSERT INTO items(item_id) VALUES(item_seq.NEXTVAL);

---

	
ALTER SEQUENCE item_seq MAXVALUE 100;
DROP SEQUENCE item_seq;

--

select * from all_indexes;

--

......................................... INDICES .....................................

For primary keys, Oracle creates an index automatically. If you want an index for any other specific column:

CREATE INDEX members_last_name_i ON members(last_name);


DROP INDEX index_name;

CREATE INDEX members_name_i ON members(last_name,first_name); --- On multiple columns.

CREATE UNIQUE INDEX members_email_i ON members(email);

---


