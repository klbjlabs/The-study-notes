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



