# **PL/SQL**

## _**`Stored Procedures and Functions`**_


Here you are going to see the detailed description on how to create and execute the named blocks (procedures and functions).

Procedures and Functions are the subprograms which can be created and saved in the database as database objects. They can be called or referred inside the other blocks also.

Apart from this, we will cover the major differences between these two subprograms. Also, we are going to discuss the Oracle built-in functions.

Here you will learn the following:

- Terminologies in PL/SQL Subprograms
- What is Procedure in PL/SQL?
- What is Function?
- Similarities between Procedure and Function
- Procedure Vs. Function: Key Differences
- Built-in Functions in PL/SQL

## _**`Terminologies in PL/SQL Subprograms`**_

Before we learn about PL/SQL subprograms, we will discuss the various terminologies that are the part of these subprograms. Below are the terminologies that we are going to discuss.

## **`Parameter:`**

The parameter is variable or placeholder of any valid PL/SQL datatype through which the PL/SQL subprogram exchange the values with the main code. This parameter allows to give input to the subprograms and to extract from these subprograms.

- These parameters should be defined along with the subprograms at the time of creation.
- These parameters are included n the calling statement of these subprograms to interact the values with the subprograms.
- The datatype of the parameter in the subprogram and the calling statement should be same.
- The size of the datatype should not mention at the time of parameter declaration, as the size is dynamic for this type.

Based on their purpose parameters are classified as:

- IN Parameter
- OUT Parameter
- IN OUT Parameter

## **`IN Parameter`**

- This parameter is used for giving input to the subprograms.
- It is a read-only variable inside the subprograms. Their values cannot be changed inside the subprogram.
- In the calling statement, these parameters can be a variable or a literal value or an expression, for example, it could be the           arithmetic expression like '5*8' or 'a/b' where 'a' and 'b' are variables.
- By default, the parameters are of IN type.

## **`OUT Parameter`**

- This parameter is used for getting output from the subprograms.
- It is a read-write variable inside the subprograms. Their values can be changed inside the subprograms.
- In the calling statement, these parameters should always be a variable to hold the value from the current subprograms.

## **`IN OUT Parameter`**

- This parameter is used for both giving input and for getting output from the subprograms.
- It is a read-write variable inside the subprograms. Their values can be changed inside the subprograms.
- In the calling statement, these parameters should always be a variable to hold the value from the subprograms.

These parameter type should be mentioned at the time of creating the subprograms.

## **`RETURN`**
RETURN is the keyword that instructs the compiler to switch the control from the subprogram to the calling statement. In subprogram RETURN simply means that the control needs to exit from the subprogram. Once the controller finds RETURN keyword in the subprogram, the code after this will be skipped.

Normally, parent or main block will call the subprograms, and then the control will shift from those parent block to the called subprograms. RETURN in the subprogram will return the control back to their parent block. In the case of functions RETURN statement also returns the value. The datatype of this value is always mentioned at the time of function declaration. The datatype can be of any valid PL/SQL data type.

# _**`What is Stored Procedure in PL/SQL ?`**_

A Procedure is a subprogram unit that consists of a group of PL/SQL statements. Each procedure in Oracle has its own unique name by which it can be referred. This subprogram unit is stored as a database object. Below are the characteristics of this subprogram unit.

**Note:** Subprogram is nothing but a procedure, and it needs to be created manually as per the requirement. Once created they will be stored as database objects.

- Procedures are standalone blocks of a program that can be stored in the database.
- Call to these procedures can be made by referring to their name, to execute the PL/SQL statements.
- It is mainly used to execute a process in PL/SQL.
- It can have nested blocks, or it can be defined and nested inside the other blocks or packages.
- It contains declaration part (optional), execution part, exception handling part (optional).
- The values can be passed into the procedure or fetched from the procedure through parameters.
- These parameters should be included in the calling statement.
- Procedure can have a RETURN statement to return the control to the calling block, but it cannot return any values through the RETURN -   statement.
- Procedures cannot be called directly from SELECT statements. They can be called from another block or through EXEC keyword.

## **`Syntax`**

```
CREATE OR REPLACE PROCEDURE 
<procedure_name>
	(
	<parameterl IN/OUT <datatype>
	..
	.
	)
[ IS | AS ]
	<declaration_part>
BEGIN
	<execution part>
EXCEPTION
	<exception handling part>
END;

```
- **CREATE PROCEDURE** instructs the compiler to create new procedure. Keyword '**OR REPLACE**' instructs the compile to replace the       existing procedure (if any) with the current one.
- Procedure name should be unique.
- Keyword '**IS**' will be used, when the procedure is nested into some other blocks. If the procedure is standalone then '**AS**' will   be used. Other than this coding standard, both have the same meaning.
 
## **`Example 1: Creating Procedure and calling it using EXEC`**

In this example, we are going to create a procedure that takes the name as input and prints the welcome message as output. We are going to use EXEC command to call procedure.

```
CREATE OR REPLACE PROCEDURE welcome_msg (p_name IN VARCHAR2) 
IS
BEGIN
dbms_output.put_line (‘Welcome '|| p_name);
END;
/
EXEC welcome_msg (‘Navin’);
```
## **`Code Explanation`** 

- **Code line 1**: Creating the procedure with name 'welcome_msg' and with one parameter 'p_name' of 'IN' type.
- **Code line 4**: Printing the welcome message by concatenating the input name.
                 Procedure is compiled successfully.
- **Code line 7**: Calling the procedure using EXEC command with the parameter 'Navin'. Procedure is executed, and the message is                          printed out as "Welcome Navin".

# _**`What is Stored Function in PL/SQL?`**_

Functions is a standalone PL/SQL subprogram. Like PL/SQL procedure, functions have a unique name by which it can be referred. These are stored as PL/SQL database objects. Below are some of the characteristics of functions.

- Functions are a standalone block that is mainly used for calculation purpose.
- Function use RETURN keyword to return the value, and the datatype of this is defined at the time of creation.
- A Function should either return a value or raise the exception, i.e. return is mandatory in functions.
- Function with no DML statements can be directly called in SELECT query whereas the function with DML operation can only be called from   other PL/SQL blocks.
- It can have nested blocks, or it can be defined and nested inside the other blocks or packages.
- It contains declaration part (optional), execution part, exception handling part (optional).
- The values can be passed into the function or fetched from the procedure through the parameters.
- These parameters should be included in the calling statement.
- Function can also return the value through OUT parameters other than using RETURN.
- Since it will always return the value, in calling statement it always accompanies with assignment operator to populate the variables.

```
CREATE OR REPLACE FUNCTION
<procedure_name>
  (
  <parameter1 IN/OUT <datatype>
  ..
  .
  )
  RETURN <datatype>
[IS|AS]
  <declaration_part>
BEGIN
  <execution part>
EXCEPTION
   <exception handling part>
END;
```
- **CREATE FUNCTION** instructs the compiler to create a new function. Keyword '**OR REPLACE**' instructs the compiler to replace the       existing function (if any) with the current one.
- The Function name should be unique.
- **RETURN** datatype should be mentioned.
- Keyword '**IS**' will be used, when the procedure is nested into some other blocks. If the procedure is standalone then '**AS**' will   be used. Other than this coding standard, both have the same meaning.

## **`Example 1: Creating Function and calling it using Anonymous Block`**

```
CREATE OR REPLACE FUNCTION welcome_msgJune ( p_name IN VARCHAR2) RETURN VAR.CHAR2
IS
BEGIN
RETURN (‘Welcome ‘|| p_name);
END;
/
```
OUTPUT: > _Function created_
```
DECLARE
lv_msg VARCHAR2(250);
BEGIN
lv_msg := welcome_msg_func (‘Navin’);
dbms_output.put_line(lv_msg);
END;
```
OUTPUT: >Welcome Navin
```
SELECT welcome_msg_func(‘Navin') FROM DUAL;
```
OUPUT: > Welcome Navin

## **`Code Explanation`**
- **Code line 1**: Creating the function with name 'welcome_msg_func' and with one parameter 'p_name' of 'IN' type.
- **Code line 2**: declaring the return type as VARCHAR2
- **Code line 5**: Returning the concatenated value 'Welcome' and the parameter value.
- **Code line 8**: Anonymous block to call the above function.
- **Code line 9**: Declaring the variable with datatype same as the return datatype of the function.
- **Code line 11**: Calling the function and populating the return value to the variable 'lv_msg'.
- **Code line 12**: Printing the variable value. The output you will get here is "Welcome Guru99"
- **Code line 14**: Calling the same function through SELECT statement. The return value is directed to the standard output directly.

## _**`Similarities between Procedure and Function`**_

- Both can be called from other PL/SQL blocks.
- If the exception raised in the subprogram is not handled in the subprogram exception handling section, then it will propagate to the -   calling block.
- Both can have as many parameters as required.
- Both are treated as database objects in PL/SQL.

## _**`Procedure Vs. Function: Key Differences`**_

 | Procedure | Function |
 |:---|:---|
 |- Used mainly to a execute certain process   |- Used mainly to perform some calculation   |
 |- Cannot call in SELECT statement |- A Function that contains no DML statements can be called in SELECT statement |
 |- Use OUT parameter to return the value |- Use RETURN to return the value |
 |- It is not mandatory to return the value |- It is mandatory to return the value |
 |- RETURN will simply exit the control from subprogram. |- RETURN will exit the control from subprogram and also returns the value |
 |- Return datatype will not be specified at the time of creation |- Return datatype is mandatory at the time of creation|
 
 ##_**`Built-in Functions in PL/SQL`**_
 PL/SQL contains various built-in functions to work with strings and date datatype. Here we are going to see the commonly used functions  and their usage.
 
 ### **Conversion Functions**
 
 These built-in functions are used to convert one datatype to another datatype.
 
 | Function Name | Usage | Example |
 |:---|:---|:---|
 | TO_CHAR | Converts the other datatype to character datatype | TO_CHAR(123); |
 | TO_DATE ( string, format ) | Converts the given string to date. The string should match with the format. | TO_DATE('2015-JAN-15', 'YYYY-MON-DD');
Output: 1/15/2015 |
