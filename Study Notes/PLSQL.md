# Procedural Language Extensions to the Structured Query Language (PL/SQL)


PL/SQL engine runs the procedural elements while the SQL engine processes the SQL statements.

## PL/SQL Blocks

A block consists of 3 parts:

1) Declaration
    * Declare variables, cursors, define data types
2) Execution
    * Code to execute. At least 1 statement, even a null one.
3) Exeption Handling

```SQL


DECLARE
        message varchar2(100) := 'This is the message';
BEGIN
    message := message || ' from Jeremy';
    DBMS_OUTPUT.PUT_LINE(message);
END;


DECLARE
    num number := 2;
BEGIN
    DBMS_OUTPUT.PUT_LINE(1 / num);
EXCEPTION
    WHEN ZERO_DIVIDE THEN
        DBMS_OUTPUT.PUT_LINE('You cant devide by 0');
END;


```

Only the Execution section is mandatory.

## Anonymous Block

 An anonymous block is not saved in the Oracle Database server, so it is just for one-time use. However, PL/SQL anonymous blocks can be useful for testing purposes.


## Actions

* To see the server outputs

```sql
SET SERVEROUTPUT ON;
```

# Notes

/ is used to execute the previous block.

There are two kinds of data type:

* Scalar (number, boolean, character, date)
* Composite ()

## char(5)

Specifies that the string will be maximun 5 characters long or less.

# Important notes

PLS_INTEGER values require less storage than NUMBER. Hence, you should always use PLS_INTEGER values for all calculation in its range to increase the efficiency of programs.

The BOOLEAN datatype has three data values: TRUE, FALSE, and NULL.

SQL does not have the BOOLEAN data type, therefore, you cannot


## varchar vs varchar2

VARCHAR is reserved by Oracle to support distinction between NULL and empty string in future, as ANSI standard prescribes.

VARCHAR2 does not distinguish between a NULL and empty string, and never will.

If you rely on empty string and NULL being the same thing, you should use VARCHAR2.






 