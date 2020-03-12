
- [Procedural Language Extensions to the Structured Query Language (PL/SQL)](#procedural-language-extensions-to-the-structured-query-language-plsql)
  - [PL/SQL Blocks](#plsql-blocks)
  - [Anonymous Block](#anonymous-block)
  - [Actions](#actions)
- [Notes](#notes)
  - [char(5)](#char5)
- [Important notes](#important-notes)
- [Section 1](#section-1)
  - [varchar vs varchar2](#varchar-vs-varchar2)
  - [Misc](#misc)
  - [Variables](#variables)
    - [Conventions](#conventions)
    - [Setting default values](#setting-default-values)
    - [Misc](#misc-1)
    - [Using column types on variables](#using-column-types-on-variables)
    - [Setting a vaiable type to another variable](#setting-a-vaiable-type-to-another-variable)
  - [Constants](#constants)
  - [Comments](#comments)
- [Section 2. Conditional control](#section-2-conditional-control)
  - [IF, ELSE IF, ELSE](#if-else-if-else)
  - [](#)
    - [Simple Case statement](#simple-case-statement)
    - [Searched Case statement](#searched-case-statement)
  - [GOTO](#goto)

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

Note that PL/SQL treats a zero-length string as a NULL value.

---

# Section 1

## varchar vs varchar2

VARCHAR is reserved by Oracle to support distinction between NULL and empty string in future, as ANSI standard prescribes.

VARCHAR2 does not distinguish between a NULL and empty string, and never will.

If you rely on empty string and NULL being the same thing, you should use VARCHAR2.

## Misc

A block cannot be empty, it needs to have at least 1 statement, even if is 'NULL;'

```SQL

-- Won't work

BEGIN
END;

-- Will work
BEGIN
    NULL;
END;

```


## Variables

Syntax:

```SQL
variable_name datatype [NOT NULL] [:= initial_value];
```

### Conventions

* Local variable should start with 'l_'
* Global variables should start with 'g_'
* Example: 'l_total_sales', 'g_module_name'

### Setting default values

```SQL
l_product_name VARCHAR2( 100 ) := 'Laptop'; 

-- Or

l_product_name VARCHAR2( 100 ) DEFAULT 'Laptop';

```

### Misc

Setting NOT NULL constraint
```SQL
l_shipping_status VARCHAR2( 25 ) NOT NULL := 'Shipped';

-- Now variable doesn't accept a NULL or an empty string

```

### Using column types on variables

```SQL
DECLARE
    l_status customers.name%TYPE;
    l_credit_limit customers.credit_limit%TYPE;
BEGIN
    SELECT
        name,
        credit_limit
    INTO
        l_name,
        l_credit_limit
    FROM
        customers
    WHERE PATRONID = 89
    AND ROWNUM = 1;
    DBMS_OUTPUT.PUT_LINE('Status : ' || l_name || ', Raw Card Number ' || l_credit_limit);
END;
```
### Setting a vaiable type to another variable

```SQL
DECLARE
    l_status MC_PROVISIONING.STATUS%TYPE;
    l_status2 l_status%TYPE;
BEGIN
    SELECT
        MAX(STATUS),
        MIN(STATUS)
    INTO
        l_status,
        l_status2
    FROM
        MC_PROVISIONING
    WHERE PATRONID = 89;
    --AND ROWNUM = 1;
    DBMS_OUTPUT.PUT_LINE('Status : ' || l_status || ', Raw Card Number ' || l_status2);
END;
```

## Constants

Constants use the 'co_' prefix by convention.
Use the NOT NULL keywords to not allow NULL or EMPTY strings.

```SQL

    co_variable_name CONSTANT TYPE [NOT NULL] := value_or_derived_value;

    co_pi CONSTANT NUMBER NOT NULL := 3.14;
    co_derived CONSTANT NUMBER := 5 + 10;

```

## Comments

You can use single line and multiple line comment:

```SQL

----- Single line comment

/*

Multiple line comment

*/

```

Nested multiline comments are not allowed.


# Section 2. Conditional control

## IF, ELSE IF, ELSE

Syntax:

```SQL

DECLARE

    l_condition BOOLEAN := FALSE;

BEGIN

i_condition := cost > money;

IF condition THEN

    -- Statements

    IF nested_condition THEN

        -- Nested statement

    END IF

ELSE IF condition2 THEN

    -- Statements2

ELSE

    -- Statements3

END IF

```

## 

You can put a NULL; statement in the ELSE of CASE.

Case syntax:

### Simple Case statement

Used to execute sequence of statements based on the result of a single expression.

```SQL

CASE l_variable -- Notice the CASE with a value
WHEN 'A' THEN
--Statement;
WHEN 'B' THEN
--Statement2;
ELSE
--Statement3;
END CASE

```

### Searched Case statement

Searched Case statements are used to execute sequence of statements based on the result of multiple Boolean expresions.

```SQL

CASE -- Notice the CASE with no value
WHEN l_price > 200000 THEN
--Statement;
WHEN l_price > 5000 THEN
--Statement2;
ELSE
--Statement3;
END CASE

```

###

If you don't specify an ELSE clause, Oracle puts:

```SQL
ELSE 
    RAISE CASE_NOT_FOUND;
```

## GOTO

When using a GOTO statement, you need to specify a label followed by at least one executable statement. That statement can be NULL; statement.

First, you cannot use a GOTO statement to transfer control into an IF, CASE or LOOP statement, the same for sub-block.

Third, you cannot use a GOTO statement to transfer control out of a subprogram or into an exception handler.

Fourth, you cannot use a GOTO statement to transfer control from an exception handler back into the current block.

You set up a label like:

```
<<lable_name>>
```

Use GOTO like:

```SQL
GOTO label_name;
```



