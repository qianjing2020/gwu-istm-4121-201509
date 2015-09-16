# Single-table SQL

Students need not understand relational database concepts to use a database as an alternative tool for data processing and analysis.

This document details clauses, functions, and considerations for performing analysis with SQL on a single database table.

## Clauses

### SELECT

The `SELECT` clause specifies the attributes to be included in the resulting dataset.

```` sql
SELECT "fun times"
````

```` sql
SELECT 2
````

```` sql
SELECT 2+2
````

Selecting multiple attributes into a single resulting dataset.

```` sql
SELECT
  "fun times",
  2,
  2 + 2
````

Alias each attribute for clarity.

```` sql
SELECT
  "fun times" AS new_attribute_name
  ,2 AS original_count
  ,2 + 2 AS revised_count
````

### FROM

The `FROM` clause is mandatory except for non-table-related selections and functions.
 It specifies the database table from which to select results.

```` sql
SELECT attribute_name
FROM table_name
````

```` sql
SELECT
  attribute_a
  ,attribute_b
FROM table_x
````

To select all attributes from a given table,
 use a star (`*`) to denote all attributes instead of listing each attribute by name.

```` sql
SELECT *
FROM table_x
````

> NOTE: `SELECT *` is slower than selecting each attribute by name.

### WHERE

The `WHERE` clause is optionally used to
 filter the set of returned results according to one or more logical operations.

Follow the different kind of logical operations in each of the queries below:

```` sql
SELECT
 attribute_a
 ,attribute_b
FROM table_x
WHERE attribute_b = "some specific value" -- equal to
````

```` sql
SELECT
 attribute_a
 ,attribute_b
FROM table_x
WHERE attribute_b <> "some specific value" -- not equal to
````

```` sql
SELECT
 attribute_a
 ,attribute_b
FROM table_x
WHERE attribute_b > "some numeric value" -- greater than, less than, etc.
````

```` sql
SELECT
 attribute_a
 ,attribute_b
FROM table_x
WHERE attribute_b >= "some numeric value" -- greater than or equal to, less than or equal to, etc.
````

```` sql
SELECT
  attribute_a
  ,attribute_b
FROM table_x
WHERE attribute_b LIKE "%some partial value%" -- string matching using `LIKE` and `%`
````

```` sql
SELECT
  attribute_a
  ,attribute_b
FROM table_x
WHERE attribute_b IN ("specific value 1", "specific value 2") -- inclusion in a list
````

```` sql
SELECT *
FROM my_table
WHERE attribute_a IS NULL -- lack of any value
````

```` sql
SELECT *
FROM my_table
WHERE attribute_a IS NOT NULL -- presence of any value
````

### ORDER BY

The `ORDER BY` clause is optionally used to
 specify the attributes and method for sorting the resulting data set.

```` sql
SELECT *
FROM my_table
ORDER BY attribute_a -- sort in ascending order (ASC) by default
````

```` sql
SELECT *
FROM my_table
ORDER BY attribute_a DESC -- sort in descending order
````

```` sql
SELECT
 attribute_a
 ,attribute_b
FROM table_x
WHERE attribute_b = "some specific value"
ORDER BY attribute_a
````

### LIMIT

The `LIMIT` clause is optionally used to restrict the total number of results returned.

```` sql
SELECT *
FROM table_a
LIMIT 200
````

```` sql
SELECT *
FROM table_a
ORDER BY attribute_a DESC
LIMIT 10
````

## Functions

Here are a few important functions to know. Consult SQL documentation as well as DBMS documentation for a comprehensive list of functions and instructions on how to use them.

### IF

```` sql
SELECT
  IF(courses.registration_name LIKE "%ISTM%", "Information Systems Department", "Other Department") AS department
FROM (
  SELECT "ISTM-4121-10" AS registration_name -- change this value and see what happens ...
) courses
````

### CASE

```` sql
SELECT
  CASE
     WHEN courses.registration_name LIKE '%ISTM%' THEN 'Information Systems Department'
     WHEN courses.registration_name LIKE '%BADM%' THEN 'Business Administration Department'
     WHEN courses.registration_name LIKE '%MKTG%' THEN 'Marketing Department'
     ELSE 'Other Department'
  END department
FROM (
  SELECT "ISTM-4121-10" AS registration_name
) courses
````

### String Functions

Consult SQL and DBMS documentation for comprehensive list of string functions, including `CAST`, `CONCAT`, `SUBSTRING_INDEX` and more.

```` sql
SELECT
  cast('2016-11-06' AS DATETIME) AS scheduled_at
  ,cast('2016-11-06' AS DATE) AS scheduled_on
````

### Date Functions

Consult SQL and DBMS documentation for comprehensive list of date functions.