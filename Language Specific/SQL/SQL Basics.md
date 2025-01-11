***Interactive Lesson for SQL: [SQLBolt](https://sqlbolt.com/)***
# Table of Contents
- [[SQL Basics#Absolute Basics|Absolute Basics]]
	- [[SQL Basics#Aliases|Aliases]]
	- [[SQL Basics#Wildcard  Characters|Wildcard  Characters]]
	- [[SQL Basics#`Where` Clause|Where Clause]]
	- [[SQL Basics#`DISTINCT` keyword|DISTINCT keyword]]
	- [[SQL Basics#`ORDER BY` keyword|ORDER BY keyword]]
	- [[SQL Basics#`LIMIT` & `OFFSET` keyword|LIMIT & OFFSET keyword]]
- [[SQL Basics#Database Normalization|Database Normalization]]
- [[SQL Basics#Joins|Joins]]
	- [[SQL Basics#`INNER JOIN`|INNER JOIN]]
	- [[SQL Basics#`OUTER JOIN`|OUTER JOIN]]
- [[SQL Basics#`NULL` Check|NULL Check]]
- [[SQL Basics#Aggregate Functions|Aggregate Functions]]

---
# Absolute Basics
```sql
SELECT column, another_column, … 
FROM mytable;
```
> [!info] Capitalization
> As you might have noticed by now, SQL doesn't _require_ you to write the keywords all capitalized, but as a convention, it helps people distinguish SQL keywords from column and tables names, and makes the query easier to read.
### Aliases
SQL aliases are used to give a table, or a column in a table, a temporary name. Aliases are often used to make column names more readable. An alias only exists for the duration of that query. **An alias is created with the `AS` keyword.**
```sql
SELECT CustomerID AS ID FROM Customers;
```
Actually, in most database languages, `AS` is optional
```sql
SELECT CustomerID ID FROM Customers;
```
### Wildcard  Characters

| Symbol | Description                                                    |
| ------ | -------------------------------------------------------------- |
| %      | Represents zero or more characters                             |
| _      | Represents a single character                                  |
| []     | Represents any single character within the brackets _*_        |
| ^      | Represents any character not in the brackets _*_               |
| -      | Represents any single character within the specified range _*_ |
| {}     | Represents any escaped character __**__                        |
_* Not supported in PostgreSQL and MySQL databases._
__** Supported only in Oracle databases.__

### `Where` Clause
```sql
SELECT column, another_column, … 
FROM mytable 
WHERE condition AND/OR another_condition AND/OR …;
```

| Operator            | Condition                                            | SQL Example|
| ------------------- | ---------------------------------------------------- | ----------------------------- |
| =, !=, < <=, >, >=  | Standard numerical operators                         | col_name != 4                 |
| BETWEEN … AND …     | Number is within range of two values (inclusive)     | col_name BETWEEN 1.5 AND 10.5 |
| NOT BETWEEN … AND … | Number is not within range of two values (inclusive) | col_name NOT BETWEEN 1 AND 10 |
| IN (…)              | Number exists in a list                              | col_name IN (2, 4, 6)         |
| NOT IN (…)          | Number does not exist in a list                      | col_name NOT IN (1, 3, 5)     |

When writing `WHERE` clauses with columns containing text data, SQL supports a number of useful operators to do things like case-insensitive string comparison and wildcard pattern matching.

| Operator   | Condition                                                                                             | Example                                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| =          | Case sensitive exact string comparison (_notice the single equals_)                                   | col_name = "abc"                                                        |
| != or <>   | Case sensitive exact string inequality comparison                                                     | col_name != "abcd"                                                      |
| LIKE       | Case insensitive exact string comparison                                                              | col_name LIKE "ABC"                                                     |
| NOT LIKE   | Case insensitive exact string inequality comparison                                                   | col_name NOT LIKE "ABCD"                                                |
| %          | Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) | col_name LIKE "%AT%"  <br>(matches "AT", "ATTIC", "CAT" or even "BATS") |
| _          | Used anywhere in a string to match a single character (only with LIKE or NOT LIKE)                    | col_name LIKE "AN\_"  <br>(matches "AND", but not "AN")                 |
| IN (…)     | String exists in a list                                                                               | col_name IN ("A", "B", "C")                                             |
| NOT IN (…) | String does not exist in a list                                                                       | col_name NOT IN ("D", "E", "F")                                         |
### `DISTINCT` keyword
SQL provides a convenient way to discard rows that have a duplicate column value by using the `DISTINCT` keyword.

> [!fail] `DISTINCT` keyword will blindly remove duplicate rows.
> Better to discard duplicates based on specific columns using grouping and the `GROUP BY` clause.
### `ORDER BY` keyword
Most data in real databases are added in no particular column order. As a result, it can be difficult to read through and understand the results of a query as the size of a table increases to thousands or even millions rows. SQL provides a way to sort results by a given column in ascending or descending order using the `ORDER BY` clause.
```sql
SELECT column, another_column, … 
FROM mytable 
WHERE condition(s) 
ORDER BY column ASC/DESC;
```
Each row is sorted **alpha-numerically** based on the specified column's value.
### `LIMIT` & `OFFSET` keyword
Another clause which is commonly used with the `ORDER BY` clause are the `LIMIT` and `OFFSET` clauses, which are a useful optimization to indicate to the database the subset of the results you care about.  
**The `LIMIT` will reduce the number of rows to return, and the optional `OFFSET` will specify where to begin counting the number rows from.**
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

# Database Normalization
Database normalization is useful because it minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other (ie. Types of car engines can grow independent of each type of car). As a trade-off, queries get slightly more complex since they have to be able to find data from different parts of the database, and performance issues can arise when working with many large tables.
In order to answer questions about an entity that has data spanning multiple tables in a normalized database, we need to learn how to write a query that can combine all that data and pull out exactly the information we need.
Tables that share information about a single entity need to have a _primary key_ that identifies that entity _uniquely_ across the database. One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique.
# Joins
Using the `JOIN` clause in a query, we can combine row data across two separate tables using this unique key.

Here are the different types of the `JOIN` in SQL:
- `(INNER) JOIN`: Returns records that have matching values in both tables
- `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table
- `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
- `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table
### `INNER JOIN`
The `INNER JOIN` is a process that matches rows from the first table and the second table which have the same key (as defined by the `ON` constraint) to create a result row with the combined columns from both tables. After the tables are joined, the other clauses we learned previously are then applied.
```sql
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
> [!danger] You might see queries where the `INNER JOIN` is written simply as a `JOIN`.
> These two are equivalent, but we will continue to refer to these joins as inner-joins because they make the query easier to read once you start using other types of joins, which will be introduced in the following lesson.
### `OUTER JOIN`
If the two tables have asymmetric data, which can easily happen when data is entered in different stages, then we would have to use a `LEFT JOIN`, `RIGHT JOIN` or `FULL JOIN` instead to ensure that the data you need is not left out of the results.
```sql
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
# `NULL` Check
It's always good to reduce the possibility of `NULL` values in databases because they require special attention when constructing queries, constraints (certain functions behave differently with null values) and when processing the results.
An alternative to `NULL` values in your database is to have _data-type appropriate default values_, like 0 for numerical data, empty strings for text data, etc. But if your database needs to store incomplete data, then `NULL` values can be appropriate if the default values will skew later analysis (for example, when taking averages of numerical data).

Sometimes, it's also not possible to avoid `NULL` values. In these cases, you can test a column for `NULL` values in a `WHERE` clause by using either the `IS NULL` or `IS NOT NULL` constraint.
```sql
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```
# Aggregate Functions
Here are some common aggregate functions:

| Function                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **COUNT(**\***)**, **COUNT(**column**)** | A common function used to counts the number of rows in the group if no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column.                                                                                                                                                                                                                                      |
| **MIN(**column**)**                     | Finds the smallest numerical value in the specified column for all rows in the group.                                                                                                                                                                                                                                                                                                                                                |
| **MAX(**column**)**                     | Finds the largest numerical value in the specified column for all rows in the group.                                                                                                                                                                                                                                                                                                                                                 |
| **AVG(**column**)**                         | Finds the average numerical value in the specified column for all rows in the group.                                                                                                                                                                                                                                                                                                                                                 |
| **SUM(**column**)**                     | Finds the sum of all numerical values in the specified column for the rows in the group.                                                                                                                                                                                                                                                                                                                                             |
|                                         | Docs: [MySQL](https://dev.mysql.com/doc/refman/5.6/en/group-by-functions.html "MySQL Aggregate Functions"), [Postgres](http://www.postgresql.org/docs/9.4/static/functions-aggregate.html "Postgres Aggregate Functions"), [SQLite](http://www.sqlite.org/lang_aggfunc.html "SQLite Aggregate Functions"), [Microsoft SQL Server](https://msdn.microsoft.com/en-us/library/ms173454.aspx "Microsoft SQL Server Aggregate Functions") |
