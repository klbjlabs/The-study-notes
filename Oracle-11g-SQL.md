SQL(Structured query language)
==============================

SQL Statements
--------------

### Data manipulation language (DML)
* `SELECT` 
* `INSERT`
* `UPDATE`
* `DELETE`
* `MERGE`

### Data definition language (DDL)
* `CREATE`
* `ALTER`
* `DROP`
* `RENAME`
* `TRUNCATE`
* `COMMENT`

### Data control language (DCL)
* `GRANT`
* `REVOKE`

### Transaction control
* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`

## Development Environments for SQL
* Oracle SQL Developer
* SQL\*PLUS

-------------------------------------------------------------------
##SELECT
### Capabilities of SQL SELECT Statements
* Projection
* Selection
* Join

### Basic SELECT Statement
* SELECT
* FROM


	Select *
	FROM departments;
	---
	Select department_id, location_id
	FROM departments;

### Column Heading Defaults
* SQL\*Plus
 * Character and Date column headings are left-aligned.
 * Number column headings are right-aligned.
 * Default heading display: Uppercase.

### Arithmetic Expressions
* `+` Add
* `-` Subtract
* `*` Multiply
* `/` Divide


	SELECT last_name, salary, salary + 300
	FROM employees;
	---
	SELECT last_name, salary, 12*salary+100
	FROM employees;
	---
	SELECT last_name, salary, 12*(salary+100)
	FROM employees;

### Defining a Null Value
* Null is value that is unavailable, unassigned, unknown, or inapplicable.
* Null is not the same as zero or a blank space.
* Arithmentic expressions containing a null value evaluate to null. 


	SELECT last_name, job_id, salary, commission_pct
	FROM employees;

### Defining a Column Alias
* Renames a column heading
* Is useful with calculations
* Immediately follow the column name(There can also be the optional `AS` Keyword between the column name and alias.
* Requires double quotation marks if it contains spaces or special characters, or if it is case-sensitive.


	SELECT last_name AS name, commission_pct comm
	FROM employees;
	---
	SELECT last_name AS "Name", salary*12 "Annual Salary"
	FROM employees;

### Concatenation Operator
* Links columns or character strings to other columns
* Is represented by two vertical bars (||)
* Creates a resultant column that is a character expression


	SELECT last_name || job_id AS "Employees" FROM employees;

### Literal Character Strings
* A literal is a character, a number, or a date that is included is the SELECT statement.
* Date and character literal values must be enclosed within single quotation marks.
* Each character string is output once for each row returned.


	SELECT last_name || '-->' || job_id AS "Employees" FROM employees;

### Alternative Quote(q) Operator
* Specify your own quotation mark delimiter.
* Select any delimiter.
* Increase readability and usability.


	SELECT department_name || ' Department' ||
		q'['s Manager Id: ]'
		|| manager_id
		AS "Department and Manager"
	FROM deparments;

### Duplicate Rows
* The default display queries is all rows, including duplicate rows.


	SELECT DISTINCT department_id
	FROM employees;

### Displaying the Table Structure
* Use the DESCRIBE command to display the structure of a table.
* Or, select the table in the Connections tree and use the Columns tab to view the table structure.


	DESC[RIBE] tablename

### Summary

	SELECT *|{[DISTINCT] colum|expression [alias],...}
	FROM table;

-------------------------------------------------------------------
### Limiting the Rows that Are Selected
* Restrict the rows that are returned by using the `WHERE` clause:
* The `WHERE` clause follows the FROM clause.


	SELECT employee_id, last_name, job_id, department_id
	FROM employees
	WHERE department_id = 90;

### Character Strings and Dates
* Character strings and date vlaues are enclosed with single quotation marks.
* Character values are case-sensitive and date values are format-sensitive.
* The default date display format is `DD-MON-RR`.


	SELECT last_name, job_id, department_id
	FROM employees
	WHERE last_name = 'Whalen';
	---
		WHERE UPPER(last_name) = 'WHALEN';
		WHERE LOWER(last_name) = 'whalen';
	---
	SELECT last_name
	FROM employees
	WHERE hire_date = '17-FEB-96';

### Comparison Operators

     Operator	Meaning
     ------------------------------
	=	Equal to
	>	Greater than
	>=	Greater than or equal to
	<	Less than
	<=	Less than or equal to
	<>	Not equal to (!=  ^=)
     ------------------------------
     BETWEEN..AND..	Between two values(inclusive)
     IN(set)		Match any of a list of values
     LIKE		Match a character pattern
     IS NULL		Is null value

### Use Comparison Operators

	WHERE salary >= 2500 AND salary <= 3500;
	WHERE salary BETWEEN 2500 AND 3500;
	WHERE salary <= 3000;
	WHERE last_name BETWEEN 'King' AND 'Smith';
	WHERE manager_id IN (100, 101, 201);

### Pattern Matching Using the LIKE Operators
* Use the `LIKE` opertor to perform wildcard searches of valid search string values.
* Search conditions can contain either literal characters of numbers:
 * `%` denotes zero or many characters.
 * `_` denotes one character.

 	SELECT first_name
	FROM employees
	WHERE first_name LIKE 'S%';

 * You can use the `ESCAPE` indentifier to searvh for the actual % and \_symbols.

	WHERE job_id LIKE '%SA\%%' ESCAPE '\';

###  Using the Null Confitions
* Test for nulls with the IS NULL operator.

	
	WHERE manager_id IS NULL;

### Defining Conditions Using the Logical Operators

	Operator Meaning
	----------------
	AND	Returns TURE if both component conditions
	OR	Returns TURE if either component condition is true
	NOT	Returns TURE if the condition is false

### Using the `AND` `OR` `NOT` Opertors

	WHERE salary >= 10000
	AND job_id LIKE '%MAN%';
	---
	WHERE salary >= 10000
	OR job_id LIKE '%MAN%';
	---
	WHERE job_id
		NOT IN ('IT_PROG', 'ST_SLERK', 'SA_REP');
	
### Rules of Precedence

	Arithmetic operators
	Concatenation operator
	Comparison conditions
	IS [Not] NULL, LIKE, [NOT] IN
	[NOT] BETWEEN
	NOT equal to
	NOT logical condition
	AND logical condition
	OR logical condition

### Rules of Precedence
	
	SELECT last_name, job_id, salary
	FROM employees
	WHERE (job_id = 'SA_REP'
	OR    job_id = 'AD_PRES')
	AND   salary > 15000;

----------------------------------------------------------------
### Using the ORDER BY Clause
* Sort retrieved rows with the `RDER BY` clause:
 * ASC: Ascending order, default
 * DESC: Descending order
* The `ORDER BY` clause comes last in the SELECT statement


	SELECT	last_name, job_id, department_id, hire_date
	FROM	employees
	ORDER BY hire_date;

### Sorting
* Sorting in descending order:


	SELECT	last_name, job_id, department_id, hire_date
	FROM	employees
	ORDER BY hire_date DESC;  // 降序

* Sorting by column alias:


	SELECT	employee_id, last_name, salary*12 ansal
	FROM	employees
	ORDER BY annsal;   // 可以使用别名

* Sorting by using the column's numeric positions:


	SELECT	last_name, job_id, department_id, hire_date
	FROM	employees
	ORDER BY 3;   // department_id

* Sorting by multiple columns:


	SELECT	last_name, department_id, salary
	FROM	employees
	ORDER BY department_id, salary DESC;
	---
	ORDER BY department_id, salary DESC NULLS FIRST;
	---
	ORDER BY department_id, salary DESC NULLS LAST;

* Substitution Variables


	WHERE employee_id = &employee_num;
	---
	WHERE job_id = '&job_title';

### Using the Double-Ampersand Substitution Variable
* Use double ampersand(&&) if you want to reuse the variable value without prompting the user each time:


	SELECT	employee_id, last_name, job_id, &&column_name
	FROM	employees
	ORDER BY &column_name;

### Using the DEFINE Command
* Use the `DEFINE` command to create and assign a value to a variable.
* Use the `UNDEFINE` command to remove a variable.


	DEFINE	employee_num = 200

	SELECT	employee_id, last_name, salary, department_id
	FROM	employees
	WHERE	employee_id = &employee_num;

	UNDEFINE employee_num

---------------------------------------------------------------------
## SQL Functions
* Single-row functions
* Multiple-row functions

### Single-Row Functions
 * Manipulate data items
 * Accept arguments and return onw value
 * Act on each row that is returned
 * Return one result per row
 * May medify the data type
 * Can be nested
 * Accept arguments that can be a column or an expression


	function_name [(arg1, arg2,.....)]

### Single-Row Functions
* Number
* Characoter
* Date
* Conversion
* General


### Character Functions
* Case-conversion functions
 * LOWER('SQL Course')		`sql course`
 * UPPER('SQL Course')		`SQL COURSE`
 * INITCAP('SQL course')	`Sql Course`


	WHERE LOWER(last_name) = 'higgins';	

* Character-manipulation functions
 * CONCAT('Hello','World')	`HelloWorld`
 * SUBSTR('HelloWorld',1,5)	`Hello`
 * LENGTH('HelloWorld')		`10`
 * INSTR('HelloWorld','W')	`6`
 * LPAD(salary,10,'\*')		`*****24000`
 * RPAD(salary,10,'\*')		`24000*****`
 * REPLACE
   ('JACL and JUE','J','BL')	`BLACK and BLUE`
 * TRIM('H' FROM 'HelloWorld')	`elloWorld`

 	
	SELECT	employee_id, CONCAT(first_name, last_name) NAME,
		job_id, LENGTH (last_name),
		INSTR(last_name, 'a') "Contains 'a'?"
	FROM	employees
	WHERE	SUBSTR(job_id, 4) = 'REP';


### Number Funcyions
* ROUND: Rounds values to a specified decimal
* TRUNC: Truncates value to a specified decimal
* MOD: Returns remainder of division

	Fuction		Result
	----------------------
	ROUND(45.926, 2) 45.93
	TRUNC(45.926, 2) 45.92
	MOD(1600, 300)	 100

### Using the ROUND Function

	SELECT ROUND(45.923, 2), ROUND(45.923, 0),
	ROUND(45.923, -1)
	FROM dual;

	45.92	46	50

### Using the TRUNC Function

	SELECT TRUNC(45.923, 2), TRUNC(45.923, 0),
	TRUNC(45.923, -1)
	FROM dual;

	45.92	45	40

### Using the MOD Function

	SELECT last_name, salary, MOD(salary, 5000)
	FROM employees
	WHERE job_id = 'SA_REP'


### Working with Dates
* The Oracle database stores dates in a internal numeric format: century, year, month, day, hours, minutes, and seconds.
* The default date display format is DD-MON-RR.
 - Enables you to store 21st-century dates in the 20th century by specifying only the last two digits of the year
 - Rnables you to store 20th-century dates in the 21st century in the same way


	SELECT last_name, hire_date
	FROM employees
	WHERE hire_date < '01-FEB-88';

### Using the SYSDATE Function
* SYSDATE is a function that returns:
 - Date
 - Time


	SELECT sysdate
	FROM dual;

### Arithmetic With Dates
* Add or subtract a number to or from a date for a resultant date value.
* Subtract two dates to find the number of days between those dates.
* Add hours to a date by dividing the number of hours by 24.

### Using Arithmetic Operators with Dates

	SEECT last_name, (SYSDATE-hire_date)/7 AS WEEKS
	FROM employees
	WHERE department_id = 90;

### Date-Manipulation Functions

	Function	Result
	---------------+----------------------------------+
	MONTHS_BETWEEN	Number of months between two dates
	ADD_MONTHS	Add calendar months to date
	NEXT_DAY	Next day of the date specified
	LAST_DAY	Last day of the month
	ROUND		Round date
	TRUNC		Truncate date

### Using Date Functions

	Function			Result
	-------------------------------+----------------------------------+
	MONTHS_BETWEEN
	    ('01-SEP-95','11-JAN-94)	19.6775194
	-------------------------------+----------------------------------+
	ADD_MONTHS ('31-JAN-96',1)	'29-FEB-96'
	-------------------------------+----------------------------------+
	NEXT_DAY ('01-SEP-95','FRIDAY')	'08-SEP-95'	
	-------------------------------+----------------------------------+
	LAST_DAY ('01-FEB-95')		'28-FEB-95'

### Using ROUND and TRUNC Functions with Dates
Assume `SYSDATE` = '25-JUL-03':

	Function			Result
	-------------------------------+---------+
	ROUND(SYSDATE, 'MONTH')		01-AUG-03
	ROUND(SYSDATE, 'YEAR')		01-JAN-04
	TRUNC(SYSDATE, 'MONTH')		01-JUL-03
	TRUNC(SYSDATE, 'YEAR')		01-JAN-03

----------------------------------------------------------------------------
## Using Conversion Functions and Conditional Expressions
### Conversion Functions
* Implicit
* Explicit
 - TO_CHAR
  + `TO_CHAR(hire_date, 'MM/YY')`
  + `TO_CHAR(hire_date, 'fmYYYY-MM-DD')`   去除前导0
  + `HH24:MI:SS`
  + `TO_CHAR(salary, '$99,999.00')`
 - TO_NUMBER and TO_DATE
  + `TO_DATE('July 4,2007','Month DD,YYYY')`

### Nesting Functions
* Single-row functions can be nested to any level.
* Nested functions are evaluated from the deepest level to the least deep level. - `F3(F2(F1(col,arg1),arg2),arg3)`


	SELECT last_name,
		UPPER(CONCAT(SUBSTR (LAST_NAME, 1, 8), '_US'))
	FROM employees
	WHERE department_if = 60;

### General Functions
* The following functions work with any data type and pertain to using nulls:
 - NVL
 - NVL2
 - NULLIF
 - COALESCE

#### NVL Function

	NVL(commission_pct, 0)  如果commission_pct 为 Null  返回0
	NVL(job_id, 'No job yet')
#### Using the COALESCE Function

	从左向右 返回第一个非NULL值
	
#### CASE Expression

	CASE job_id WHEN 'IT_PROG' THEN 1.10*salary
		WHEN 'ST_CLEARK' THEN 1.15*salary
		WHEN 'SA_REP' THEN 1.20*salary
	ELSE salary END "REVISED_SALARY"

#### DECODE Function

	DECODE(job_id, 'IT_PROG', 1.10*salary,
			'ST_CLEARK', 1,15*salary,
			'SA_REP', 1.20*salary,
		salary)
	REVISED_SALARY

----------------------------------------------------------------------

### Types of Group Functions
* AVG
* COUNT 
* MAX
* MIN
* STDDEV
* SUM
* VARIANCE

### Group Functions:Syntax

	SELECT AVG(salary),MAX(salary),
		MIN(salary),SUM(salary)
	FROM employees
	WHERE job_id LIKE '%REP%';

### Count Function

	COUNT(1)
	COUNT(department_id)
	COUNT(DISTINCT department_id)

### GROUP BY Clause

	SELECT department_id, AVG(salary)
	FROM employees
	GROUP BY department_id;

### Illegall Queries Using Group Functions
* Any column or expression in the SELECT list taht is not an aggregate function must be in the GROUP BY clause:


	SELECT department_id, COUNT(last_name)
	FROM employees
	GROUP BY department_id;

### Using the HAVING Clause

	SELECT job_id, SUM(salary) PAYROLL
	FROM employees
	WHERE job_id NOT LIKE '%REP%'
	GROUP BY job_id
	HAVING SUM(salary) > 13000
	ORDER BY SUM(salary);

------------------------------------------------------------------------
## Displaying Data ftom Multiple Tables

Obtaining Data from Multiple Tables

