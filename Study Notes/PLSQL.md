
- [Procedural Language Extensions to the Structured Query Language (PL/SQL)](#procedural-language-extensions-to-the-structured-query-language-plsql)
  - [PL/SQL Blocks](#plsql-blocks)
  - [Anonymous Block](#anonymous-block)
  - [Actions](#actions)
- [Notes](#notes)
  - [char(5)](#char5)
- [Important notes](#important-notes)
- [Section 1. Intro](#section-1-intro)
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
- [Section 3. Iterative processing with loops](#section-3-iterative-processing-with-loops)
  - [LOOP](#loop)
    - [Notes](#notes-1)
    - [Keywords](#keywords)
  - [FOR LOOP](#for-loop)
    - [Notes](#notes-2)
  - [WHILE loop](#while-loop)
    - [Notes](#notes-3)
  - [CONTINUE; and CONTINUE WHEN;](#continue-and-continue-when)
    - [Notes](#notes-4)
- [Section 4. SELECT INTO](#section-4-select-into)
    - [Notes](#notes-5)
- [Section 5. Exception handlers](#section-5-exception-handlers)
  - [Notes](#notes-6)
  - [Declaring exceptions and creating user-defined exceptions](#declaring-exceptions-and-creating-user-defined-exceptions)
  - [Rasing exceptions](#rasing-exceptions)
    - [raise_application_error procedure](#raiseapplicationerror-procedure)
    - [Handling others exceptions](#handling-others-exceptions)
- [Section 6. Records](#section-6-records)
  - [Notes](#notes-7)

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

* PLS_INTEGER values require less storage than NUMBER. Hence, you should always use PLS_INTEGER values for all calculation in its range to increase the efficiency of programs.

* The BOOLEAN datatype has three data values: TRUE, FALSE, and NULL.

* SQL does not have the BOOLEAN data type, therefore, you cannot

* Note that PL/SQL treats a zero-length string as a NULL value.

* You can put an anonymous block inside of another anonymous block.

* When an exception occurs or raise_application_error procedures executes, note that the changes made to the global data structure such as packaged variables, and database objects like tables will not be rolled back. Therefore, you must explicitly execute the ROLLBACK statement to reverse the effect of the DML.

---

# Section 1. Intro

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

# Section 3. Iterative processing with loops

## LOOP

### Notes

* It is possible to nest a LOOP statement inside of a LOOP statement

* Specify a <\<lable>> to EXIT to that label like: EXIT label;

* Exit; and Exit label; are equivalent to break; and break label; in other lenguages.

* This is like a DO WHILE loop, since it executes at least one no matter what.

### Keywords
  * Exit
  * Exit when

```SQL
DECLARE
l_count NUMBER := 0;
BEGIN

LOOP

    EXIT WHEN l_count > 4;

    l_count := l_count + 1;

END LOOP;

DBMS_OUTPUT.PUT_LINE('The count is: ' || l_count);

END;

---------

DECLARE
l_count NUMBER := 0;
BEGIN

<<loop_label>> LOOP

    EXIT loop_label WHEN l_count > 4;
    
    l_count := l_count + 1;

END LOOP;

DBMS_OUTPUT.PUT_LINE('The count is: ' || l_count);

END;


```

## FOR LOOP

### Notes

* The 'index' variable in the FOR LOOP is inmutable inside of the lOOP. It changes automatically so changes done to it manually will not have effects.

* A variable with the same name as the 'index' will not have effect inside of the LOOP.

* To make an outer variable with the same name as the 'index' have effect inside of the LOOP, then add a <\<outer>> lable outside DECLARE and use it like 'outer.variable_with_same_name_as_index inside of the LOOP.

* Referencing the 'index' outside of the FOR LOOP results in an error.

* To count down in the loop, use the REVERSE keyword: FOR index IN REVERSE 1:5

```SQL
<<outer_label>>
DECLARE
l_count NUMBER := 0;
my_index NUMBER := 1;
BEGIN

FOR my_index IN 1..5
LOOP

DBMS_OUTPUT.PUT_LINE('my_index: ' || my_index); -- yields 1,2,3,4,5

DBMS_OUTPUT.PUT_LINE('outer_label.my_index: ' || outer_label.my_index); -- yields 1,1,1,1

END LOOP;

DBMS_OUTPUT.PUT_LINE('my_index out ' || my_index); -- yields 1,1,1,1

END;
```

## WHILE loop

### Notes

* When the boolean condition is FALSE or NULL the WHILE loop will stop.

* Use the EXIT or EXIT WHEN keywords to terminate the loop at any moment.

* Has the rules of a regular while loop of other languages.

```SQL
DECLARE
l_count NUMBER := 0;
BEGIN

WHILE l_count < 5
LOOP

    DBMS_OUTPUT.PUT_LINE(l_count);

    l_count := l_count + 1;

END LOOP;

END;
```

## CONTINUE; and CONTINUE WHEN;

### Notes

* Use can used CONTINUE and CONTINUE WHEN with all other loops, LOOP, FOR LOOP, WHILE LOOP.

* CONTINUE is used exactly the same way as other languages.

* CONTINUE WHEN is used with a condition.

```SQL
BEGIN
  FOR n_index IN 1 .. 10
  LOOP
    -- skip even numbers
    CONTINUE
  WHEN MOD( n_index, 2 ) = 0;
    DBMS_OUTPUT.PUT_LINE( n_index );
  END LOOP;
END;
```

# Section 4. SELECT INTO

### Notes

* Works to get data from a single row into variables.
  
* If the SELECT statement returns more than one row, Oracle will raise the **TOO_MANY_ROWS** exception.
  
* If the SELECT statement does not return any row, Oracle will raise the **NO_DATA_FOUND** exception.

* You can put a whole row into a variable with the %ROWTYPE.

```SQL

DECLARE

l_order ORDERS%ROWTYPE;

BEGIN

SELECT * 
INTO l_order
FROM ORDERS 
WHERE ORDERID =  '123abc';

DBMS_OUTPUT.PUT_LINE('ORDERID: ' || l_order.ORDERID || ', ORDER NUMBER: ' || l_order.ORDERNUMBER);

END;

```

# Section 5. Exception handlers

|Exception|Oracle Error|SQLCODE Value|
|---|---|---|
|ACCESS_INTO_NULL|ORA-06530|-6530|
|CASE_NOT_FOUND|ORA-06592|-6592|
|COLLECTION_IS_NULL|ORA-06531|-6531|
|CURSOR_ALREADY_OPEN|ORA-06511|-6511|
|DUP_VAL_ON_INDEX|ORA-00001|-1|
|INVALID_CURSOR|ORA-01001|-1001|
|INVALID_NUMBER|ORA-01722|-1722|
|LOGIN_DENIED|ORA-01017|-1017|
|NO_DATA_FOUND|ORA-01403|100|
|NOT_LOGGED_ON|ORA-01012|-1012|
|PROGRAM_ERROR|ORA-06501|-6501|
|ROWTYPE_MISMATCH|ORA-06504|-6504|
|SELF_IS_NULL|ORA-30625|-30625|
|STORAGE_ERROR|ORA-06500|-6500|
|SUBSCRIPT_BEYOND_COUNT|ORA-06533|-6533|
|SUBSCRIPT_OUTSIDE_LIMIT|ORA-06532|-6532|
|SYS_INVALID_ROWID|ORA-01410|-1410|
|TIMEOUT_ON_RESOURCE|ORA-00051|-51|
|TOO_MANY_ROWS|ORA-01422|-1422|
|VALUE_ERROR|ORA-06502|-6502|
|ZERO_DIVIDE|ORA-01476|-1476|

## Notes

* When an error occur, Oracle looks for the Exception block for handlers.

* The exception handling has a syntax like this: 'WHEN EXCEPTION_NAME THEN'

* PL/SQL has three exception categories:
    1) Internally defined (no name, an error like 'ORA-27102')
    2) Predefined exceptions, with a name like NO_DATA_FOUND
    3) User-defined exceptions

* You can reraise an exception inside of an EXCEPTION block. You just have to **RAISE;** without specifying the exception.

```SQL

DECLARE
    l_name customers.name%TYPE;
    l_customer_id customers.customer_id%TYPE := &customer_id;
BEGIN
    -- get the customer
    SELECT name INTO l_name
    FROM customers
    WHERE customer_id <= l_customer_id;
    
    -- show the customer name   
    dbms_output.put_line('Customer name is ' || l_name);
 
    EXCEPTION 
        WHEN NO_DATA_FOUND THEN -- Here the declaration of the exception we are expecting
            dbms_output.put_line('Customer ' || l_customer_id ||  ' does not exist');
        WHEN ZERO_DIVIDE THEN -- More handlers like this
             dbms_output.put_line('Other handler');
END;
/

```

## Declaring exceptions and creating user-defined exceptions

* Declaring and Creating a user-defiened exception
* 
```SQL
DECLARE
    exception_name EXCEPTION; -- Like a normal variable
    PRIGMA EXCEPTION_INIT (exception_name, 20001); -- Error code from 20,000 to 20,999, mandatory
BEGIN
    NULL;
END;
```

## Rasing exceptions

```SQL

IF TRUE THEN
    RAISE exception_name;
END IF;

IF condition THEN
    raise_application_error(-20001,'Credit is too high'); -- To show a message like ORA-20001: Credit is too high
END IF;

```

### raise_application_error procedure

```SQl
raise_application_error(
    error_number, 
    message 
    [, {TRUE | FALSE}] -- TRUE show stack trace, FALSE don't show stack trace, just this exception information.
);

```

### Handling others exceptions

* Use the WHEN OTHER at the end of the exception list

```SQL

    EXCEPTION
        WHEN e1 THEN
            -- Handle e1
        WHEN OTHERS
            -- Handle any other exceptions
            l_error_code := SQLCODE; -- SQLCODE prints the most recent exception code inside of the EXCEPTION block. Outside of it it returns 0. Should be used inside here.
            -- print error
            l_error_message := SQLERRM(error_number); -- SQLERRM gets an error code and gets the message associated with it. Only use it inside of an EXCEPTION block.
            -- print error message

```

# Section 6. Records

## Notes

* There are 3 types of records
  1) table-based
  2) cursor-based
  3) programmer-defined

* Use the **dot notation** to access the fields in a record.
* You cannot compare to records like 'record1 = record2', you would need to compare each one if their fields like 'record1.name = record2.name'
* You can assign values to records like 'record1.name "Jeremy"'

* To create a programer-defined record definition and use it:

```SQL

TYPE address IS RECORD(
    field1 VARCHAR2(50),
    field2 NUMBER,
    --etc
);

my_address_record address;

-- Now I can use the my_address_record record.

```

* You can SELECT INTO a whole record or individual fields:

```SQL

SELECT
  first_name, last_name, phone
INTO
  r_contact -- is a record of type contacts
FROM
  contacts
WHERE
  contact_id = 100;


-- fetch from a cursor a whole record and put it into the r_contact record
FETCH cur_contacts INTO r_contact;
 
-- fetch from a cursor individual fields
FETCH
  cur_contacts
INTO
  r_contact.first_name, 
  r_contact.last_name, 
  r_contact.phone;

```

* Insert a new record into a table:

```SQL
DECLARE
  r_person persons%ROWTYPE;
 
BEGIN
  -- assign values to person record
  r_person.person_id  := 1;
  r_person.first_name := 'John';
  r_person.last_name  := 'Doe';
 
  -- insert a new person
  INSERT INTO persons VALUES r_person;
END;
```

* To update a row from a %ROWTYPE record, you use the SET ROW keywords as shown in the following example:

```SQL
DECLARE
  r_person persons%ROWTYPE;
 
BEGIN
  -- get person data of person id 1
  SELECT * INTO r_person 
  FROM persons 
  WHERE person_id = 1;
 
  -- change the person's last name
  r_person.last_name  := 'Smith';
 
  -- update the person
  UPDATE persons
  SET ROW = r_person -- Mind the = sign
  WHERE person_id = r_person.person_id;
END;
```

* Nested record

```SQL

DECLARE
  TYPE address IS RECORD (
    street_name VARCHAR2(255),
    city VARCHAR2(100),
    state VARCHAR2(100),
    postal_code VARCHAR(10),
    country VARCHAR2(100)
  );
  TYPE customer IS RECORD(
      customer_name VARCHAR2(100),
      ship_to address, -- Here, the 'address' record is being used to created a nested record.
      bill_to address -- Here too
  );
  r_one_time_customer customer;
BEGIN
 
  r_one_time_customer.customer_name := 'John Doe';
  -- assign address
  r_one_time_customer.ship_to.street_name := '4000 North 1st street';
  r_one_time_customer.ship_to.city := 'San Jose';
  r_one_time_customer.ship_to.state := 'CA';
  r_one_time_customer.ship_to.postal_code := '95134';
  r_one_time_customer.ship_to.country := 'USA';
  -- bill-to address is same as ship-to address
  r_one_time_customer.bill_to := one_time_customer.ship_to;
END;

```