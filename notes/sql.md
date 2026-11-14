# SQL – Complete Practical Notes
## Data Analytics Course

---

# 1. Introduction to SQL

SQL stands for **Structured Query Language**.

SQL is used to communicate with relational databases.

It allows us to:
- Store data
- Retrieve data
- Insert new records
- Update existing records
- Delete records
- Filter and sort data
- Perform calculations
- Analyze large datasets
- Combine information from multiple tables

### Why SQL in Data Analytics?

Data analysts frequently work with databases containing thousands or millions of records.

SQL helps analysts extract meaningful information from these databases.

Examples:
- Find total sales of a company.
- Identify the top-selling products.
- Calculate monthly revenue.
- Find customers who haven't purchased anything.
- Compare sales between different regions.

### Popular SQL Databases

1. MySQL
2. PostgreSQL
3. Microsoft SQL Server
4. Oracle Database
5. SQLite

For this course, we will use MySQL.

---

# 2. Installing and Setting Up MySQL

### MySQL Installation

Download MySQL from:

https://dev.mysql.com/downloads/

You can use:
- MySQL Server
- MySQL Workbench

MySQL Workbench provides a graphical interface for writing and executing SQL queries.

Alternatively, you can use a terminal or command-line client.

### Connecting to MySQL

```bash
mysql -u root -p
```

Enter your password when prompted.

### Check MySQL Version

```sql
SELECT VERSION();
```

### Show Available Databases

```sql
SHOW DATABASES;
```

---

# 3. Understanding Databases and Tables

A database is an organized collection of data.

A table stores data in rows and columns.

Example: A Students table.

| student_id | name | age | city |
|---|---|---|---|
| 1 | Amit | 21 | Jaipur |
| 2 | Rahul | 22 | Delhi |
| 3 | Priya | 20 | Mumbai |

### Important Terminology

**Database:** Collection of related tables.

**Table:** Collection of related records.

**Row:** A single record.

**Column:** An attribute of a record.

**Primary Key:** A column that uniquely identifies each row.

**Foreign Key:** A column that references a key in another table.

---

# 4. Creating a Database

Syntax:

```sql
CREATE DATABASE database_name;
```

Example:

```sql
CREATE DATABASE analytics_db;
```

### Display Databases

```sql
SHOW DATABASES;
```

### Select a Database

```sql
USE analytics_db;
```

### Delete a Database

```sql
DROP DATABASE analytics_db;
```

Warning: DROP DATABASE permanently removes the database and its tables.

---

# 5. SQL Data Types

Data types define what kind of information a column can store.

| Data Type | Description |
|---|---|
| INT | Integer values |
| BIGINT | Large integer values |
| DECIMAL(p,s) | Exact decimal values |
| FLOAT | Approximate decimal values |
| DOUBLE | Double-precision decimal |
| VARCHAR(n) | Variable-length text |
| CHAR(n) | Fixed-length text |
| TEXT | Large text |
| DATE | Date |
| TIME | Time |
| DATETIME | Date and time |
| TIMESTAMP | Timestamp |
| BOOLEAN | Boolean-style value (stored as TINYINT in MySQL) |

### Example

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2),
    joining_date DATE
);
```

---

# 6. Creating Tables

Syntax:

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

Example:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    city VARCHAR(50),
    marks DECIMAL(5,2)
);
```

### View Tables

```sql
SHOW TABLES;
```

### Describe a Table

```sql
DESCRIBE students;
```

Or:

```sql
SHOW COLUMNS FROM students;
```

---

# 7. SQL Constraints

Constraints define rules for the data stored in a table.

## 7.1 PRIMARY KEY

Uniquely identifies each record.

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

## 7.2 NOT NULL

Prevents NULL values.

```sql
CREATE TABLE students (
    student_id INT,
    name VARCHAR(100) NOT NULL
);
```

## 7.3 UNIQUE

Prevents duplicate values.

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

## 7.4 DEFAULT

Assigns a default value.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50) DEFAULT 'General'
);
```

## 7.5 AUTO_INCREMENT

Automatically generates numerical IDs.

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

## 7.6 CHECK

Restricts values based on a condition.

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    age INT CHECK (age >= 18)
);
```

## 7.7 FOREIGN KEY

Establishes a relationship between two tables.

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

# 8. SQL Commands Classification

SQL commands are commonly classified into five categories.

| Category | Full Form | Purpose |
|---|---|---|
| DDL | Data Definition Language | Defines database structure |
| DML | Data Manipulation Language | Modifies data |
| DQL | Data Query Language | Retrieves data |
| DCL | Data Control Language | Controls permissions |
| TCL | Transaction Control Language | Manages transactions |

### DDL Commands

- CREATE
- ALTER
- DROP
- TRUNCATE
- RENAME

### DML Commands

- INSERT
- UPDATE
- DELETE

### DQL Commands

- SELECT

### DCL Commands

- GRANT
- REVOKE

### TCL Commands

- COMMIT
- ROLLBACK
- SAVEPOINT

---

# 9. Inserting Data into Tables

INSERT is used to add new records.

Syntax:

```sql
INSERT INTO table_name
(column1, column2)
VALUES
(value1, value2);
```

Example:

```sql
INSERT INTO students
(student_id, name, age, city, marks)
VALUES
(1, 'Amit', 21, 'Jaipur', 85);
```

### Insert Multiple Records

```sql
INSERT INTO students
(student_id, name, age, city, marks)
VALUES
(2, 'Rahul', 22, 'Delhi', 75),
(3, 'Priya', 20, 'Mumbai', 92),
(4, 'Neha', 21, 'Jaipur', 65),
(5, 'Karan', 23, 'Delhi', 80);
```

---

# 10. SELECT Statement

SELECT retrieves data from a table.

### Select All Columns

```sql
SELECT * FROM students;
```

### Select Specific Columns

```sql
SELECT name, city FROM students;
```

### Select a Single Column

```sql
SELECT name FROM students;
```

### Select Unique Values

```sql
SELECT DISTINCT city FROM students;
```

### Select Calculated Columns

```sql
SELECT
    name,
    marks,
    marks + 5 AS updated_marks
FROM students;
```

---

# 11. WHERE Clause

WHERE filters records based on conditions.

### Example

```sql
SELECT * FROM students
WHERE city = 'Jaipur';
```

### Find Students Above 80 Marks

```sql
SELECT * FROM students
WHERE marks > 80;
```

### Comparison Operators

| Operator | Meaning |
|---|---|
| = | Equal |
| != or <> | Not equal |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |

### Multiple Conditions

```sql
SELECT * FROM students
WHERE city = 'Jaipur'
AND marks > 70;
```

### OR Operator

```sql
SELECT * FROM students
WHERE city = 'Jaipur'
OR city = 'Delhi';
```

### NOT Operator

```sql
SELECT * FROM students
WHERE NOT city = 'Delhi';
```

---

# 12. BETWEEN Operator

BETWEEN selects values within a specified range, including both endpoints.

```sql
SELECT * FROM students
WHERE marks BETWEEN 70 AND 90;
```

### NOT BETWEEN

```sql
SELECT * FROM students
WHERE marks NOT BETWEEN 70 AND 90;
```

---

# 13. IN Operator

IN checks whether a value matches any value in a given list.

```sql
SELECT * FROM students
WHERE city IN ('Jaipur', 'Delhi', 'Mumbai');
```

### NOT IN

```sql
SELECT * FROM students
WHERE city NOT IN ('Delhi', 'Mumbai');
```

---

# 14. LIKE Operator

LIKE is used for pattern matching.

| Pattern | Meaning |
|---|---|
| 'A%' | Starts with A |
| '%a' | Ends with a |
| '%mit%' | Contains mit |
| '_a%' | Second character is a |
| 'A__' | Exactly three characters, starting with A |

### Examples

Find names starting with A:

```sql
SELECT * FROM students
WHERE name LIKE 'A%';
```

Find names ending with a:

```sql
SELECT * FROM students
WHERE name LIKE '%a';
```

Find names containing an:

```sql
SELECT * FROM students
WHERE name LIKE '%an%';
```

---

# 15. NULL Values

NULL represents missing or unknown data.

NULL is not the same as zero or an empty string.

### Find NULL Values

```sql
SELECT * FROM students
WHERE marks IS NULL;
```

### Find Non-NULL Values

```sql
SELECT * FROM students
WHERE marks IS NOT NULL;
```

### Replace NULL Using COALESCE

```sql
SELECT
    name,
    COALESCE(marks, 0) AS marks
FROM students;
```

---

# 16. ORDER BY

ORDER BY sorts records.

### Ascending Order

```sql
SELECT * FROM students
ORDER BY marks ASC;
```

### Descending Order

```sql
SELECT * FROM students
ORDER BY marks DESC;
```

### Sort by Multiple Columns

```sql
SELECT * FROM students
ORDER BY city ASC, marks DESC;
```

---

# 17. LIMIT

LIMIT restricts the number of returned records.

### Top 3 Students

```sql
SELECT * FROM students
ORDER BY marks DESC
LIMIT 3;
```

### Skip First Two Records

```sql
SELECT * FROM students
LIMIT 2, 3;
```

This skips two records and returns the next three.

The equivalent explicit syntax is:

```sql
SELECT * FROM students
LIMIT 3 OFFSET 2;
```

---

# 18. UPDATE Statement

UPDATE modifies existing records.

Syntax:

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

Example:

```sql
UPDATE students
SET marks = 90
WHERE student_id = 1;
```

### Update Multiple Columns

```sql
UPDATE students
SET
    city = 'Udaipur',
    marks = 95
WHERE student_id = 1;
```

**Important:** Always use an appropriate WHERE condition when updating specific records.

Without WHERE, all rows may be updated.

---

# 19. DELETE Statement

DELETE removes records from a table.

```sql
DELETE FROM students
WHERE student_id = 5;
```

### Delete All Records

```sql
DELETE FROM students;
```

This removes all rows but keeps the table structure.

### Difference Between DELETE, TRUNCATE and DROP

| Command | Purpose |
|---|---|
| DELETE | Removes selected or all rows |
| TRUNCATE | Removes all rows |
| DROP | Removes the entire table |

---

# 20. ALTER TABLE

ALTER modifies the structure of an existing table.

### Add a Column

```sql
ALTER TABLE students
ADD email VARCHAR(100);
```

### Modify a Column

```sql
ALTER TABLE students
MODIFY name VARCHAR(150);
```

### Rename a Column

```sql
ALTER TABLE students
RENAME COLUMN name TO student_name;
```

### Drop a Column

```sql
ALTER TABLE students
DROP COLUMN email;
```

### Rename a Table

```sql
RENAME TABLE students TO student_details;
```

---

# 21. Aggregate Functions

Aggregate functions perform calculations on multiple records and return a single result.

| Function | Purpose |
|---|---|
| COUNT() | Counts records or non-NULL values |
| SUM() | Calculates total |
| AVG() | Calculates average |
| MIN() | Finds minimum |
| MAX() | Finds maximum |

### COUNT

```sql
SELECT COUNT(*) FROM students;
```

### SUM

```sql
SELECT SUM(marks) FROM students;
```

### AVG

```sql
SELECT AVG(marks) FROM students;
```

### MIN

```sql
SELECT MIN(marks) FROM students;
```

### MAX

```sql
SELECT MAX(marks) FROM students;
```

### Multiple Aggregate Functions

```sql
SELECT
    COUNT(*) AS total_students,
    SUM(marks) AS total_marks,
    AVG(marks) AS average_marks,
    MIN(marks) AS minimum_marks,
    MAX(marks) AS maximum_marks
FROM students;
```

---

# 22. GROUP BY

GROUP BY groups records with matching values.

### Count Students by City

```sql
SELECT
    city,
    COUNT(*) AS total_students
FROM students
GROUP BY city;
```

### Average Marks by City

```sql
SELECT
    city,
    AVG(marks) AS average_marks
FROM students
GROUP BY city;
```

### Maximum Marks by City

```sql
SELECT
    city,
    MAX(marks) AS highest_marks
FROM students
GROUP BY city;
```

### Group by Multiple Columns

```sql
SELECT
    city,
    age,
    COUNT(*) AS total_students
FROM students
GROUP BY city, age;
```

---

# 23. HAVING Clause

HAVING filters grouped records.

WHERE filters individual rows before grouping.

HAVING filters groups after grouping.

### Example

Find cities with more than one student.

```sql
SELECT
    city,
    COUNT(*) AS total_students
FROM students
GROUP BY city
HAVING COUNT(*) > 1;
```

### WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters rows | Filters groups |
| Used before GROUP BY logically | Used after GROUP BY logically |
| Can be used without GROUP BY | Usually used with grouped results |
| Cannot directly filter aggregate results | Can filter aggregate results |

---

# 24. SQL Joins

Joins combine related data from multiple tables.

Consider two tables:

### Departments

| department_id | department_name |
|---|---|
| 1 | IT |
| 2 | HR |
| 3 | Sales |
| 4 | Finance |

### Employees

| employee_id | name | department_id |
|---|---|---|
| 101 | Amit | 1 |
| 102 | Rahul | 2 |
| 103 | Priya | 1 |
| 104 | Neha | 3 |
| 105 | Karan | NULL |

Create these tables:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Insert sample data:

```sql
INSERT INTO departments VALUES
(1, 'IT'),
(2, 'HR'),
(3, 'Sales'),
(4, 'Finance');

INSERT INTO employees VALUES
(101, 'Amit', 1),
(102, 'Rahul', 2),
(103, 'Priya', 1),
(104, 'Neha', 3),
(105, 'Karan', NULL);
```

## 24.1 INNER JOIN

Returns only matching records.

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```

## 24.2 LEFT JOIN

Returns all records from the left table and matching records from the right table.

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```

Karan will also appear, with NULL for department_name.

## 24.3 RIGHT JOIN

Returns all records from the right table and matching records from the left table.

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```

Finance will also appear, even though no employee belongs to it.

## 24.4 CROSS JOIN

Returns every possible combination of records from both tables.

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
CROSS JOIN departments;
```

## 24.5 FULL OUTER JOIN

Returns all matching and non-matching records from both tables.

MySQL does not directly support FULL OUTER JOIN.

It can be simulated using LEFT JOIN and RIGHT JOIN with UNION.

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id

UNION

SELECT
    employees.name,
    departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```

---

# 25. UNION and UNION ALL

UNION combines the results of multiple SELECT statements.

### UNION

Removes duplicate rows.

```sql
SELECT city FROM students
UNION
SELECT city FROM customers;
```

### UNION ALL

Keeps duplicate rows.

```sql
SELECT city FROM students
UNION ALL
SELECT city FROM customers;
```

Both queries must return the same number of columns with compatible data types.

---

# 26. Subqueries

A subquery is a query inside another SQL query.

### Find Students Scoring Above Average

```sql
SELECT *
FROM students
WHERE marks > (
    SELECT AVG(marks)
    FROM students
);
```

### Find Students with Maximum Marks

```sql
SELECT *
FROM students
WHERE marks = (
    SELECT MAX(marks)
    FROM students
);
```

### Subquery with IN

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('IT', 'Sales')
);
```

### Subquery with EXISTS

```sql
SELECT *
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

EXISTS checks whether the subquery returns at least one row.

---

# 27. CASE Statement

CASE is used for conditional logic.

### Example: Assign Grades

```sql
SELECT
    name,
    marks,
    CASE
        WHEN marks >= 90 THEN 'A+'
        WHEN marks >= 80 THEN 'A'
        WHEN marks >= 70 THEN 'B'
        WHEN marks >= 60 THEN 'C'
        WHEN marks >= 40 THEN 'D'
        ELSE 'F'
    END AS grade
FROM students;
```

### Example: Categorize Salary

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 40000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 28. String Functions

String functions manipulate text values.

| Function | Purpose |
|---|---|
| UPPER() | Converts to uppercase |
| LOWER() | Converts to lowercase |
| LENGTH() | Returns byte length |
| CHAR_LENGTH() | Returns character count |
| CONCAT() | Joins strings |
| SUBSTRING() | Extracts part of a string |
| TRIM() | Removes surrounding spaces |
| REPLACE() | Replaces text |
| LEFT() | Extracts left characters |
| RIGHT() | Extracts right characters |

### Examples

```sql
SELECT UPPER(name) FROM students;
```

```sql
SELECT LOWER(name) FROM students;
```

```sql
SELECT CONCAT(name, ' - ', city)
FROM students;
```

```sql
SELECT SUBSTRING(name, 1, 3)
FROM students;
```

```sql
SELECT TRIM('  Hello SQL  ');
```

```sql
SELECT REPLACE('Data Analytics', 'Data', 'Business');
```

---

# 29. Numeric Functions

| Function | Purpose |
|---|---|
| ROUND() | Rounds a number |
| CEIL() | Rounds upward |
| FLOOR() | Rounds downward |
| ABS() | Absolute value |
| MOD() | Remainder |
| POWER() | Exponentiation |
| SQRT() | Square root |

### Examples

```sql
SELECT ROUND(45.678, 2);
```

```sql
SELECT CEIL(45.2);
```

```sql
SELECT FLOOR(45.9);
```

```sql
SELECT ABS(-100);
```

```sql
SELECT MOD(10, 3);
```

```sql
SELECT POWER(5, 2);
```

```sql
SELECT SQRT(144);
```

---

# 30. Date and Time Functions

Date functions are very useful for business analytics.

| Function | Purpose |
|---|---|
| CURDATE() | Current date |
| CURTIME() | Current time |
| NOW() | Current date and time |
| YEAR() | Extract year |
| MONTH() | Extract month |
| DAY() | Extract day |
| DAYNAME() | Name of weekday |
| MONTHNAME() | Name of month |
| DATEDIFF() | Difference between dates |
| DATE_ADD() | Add interval |
| DATE_SUB() | Subtract interval |
| DATE_FORMAT() | Format a date |

### Examples

```sql
SELECT CURDATE();
```

```sql
SELECT NOW();
```

```sql
SELECT YEAR('2026-11-14');
```

```sql
SELECT MONTHNAME('2026-11-14');
```

```sql
SELECT DAYNAME('2026-11-14');
```

```sql
SELECT DATEDIFF('2026-12-01', '2026-11-01');
```

### Add Days to a Date

```sql
SELECT DATE_ADD(
    '2026-11-14',
    INTERVAL 7 DAY
);
```

### Extract Month and Year from Orders

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    COUNT(*) AS total_orders
FROM orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date);
```

---

# 31. Window Functions

Window functions perform calculations across related rows without combining them into a single grouped row.

They are important for advanced data analytics.

## 31.1 ROW_NUMBER()

Assigns a unique sequential number to each row within a window.

```sql
SELECT
    name,
    marks,
    ROW_NUMBER() OVER (
        ORDER BY marks DESC
    ) AS row_num
FROM students;
```

## 31.2 RANK()

Assigns ranks, leaving gaps when values are tied.

```sql
SELECT
    name,
    marks,
    RANK() OVER (
        ORDER BY marks DESC
    ) AS student_rank
FROM students;
```

## 31.3 DENSE_RANK()

Assigns ranks without gaps.

```
