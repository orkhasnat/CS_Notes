***Interactive Lesson for SQL: [SQLBolt](https://sqlbolt.com/)***
# Table of Contents

---
# Absolute Basics
```sql
SELECT column, another_column, … 
FROM mytable;
```
> [!info] Capitalization
> As you might have noticed by now, SQL doesn't _require_ you to write the keywords all capitalized, but as a convention, it helps people distinguish SQL keywords from column and tables names, and makes the query easier to read.

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