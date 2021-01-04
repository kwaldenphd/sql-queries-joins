# SQL Queries and Joins

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab covers the basics of SQL syntax using DB Browser for SQLite. It covers operations like selecting, sorting, filtering, aggregating, and calculating. It also provides an overview of joins, including common join types. 

## Acknowledgements
The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

# Table of Contents

- [Data](#data)
- [SQL Syntax](#sql-syntax)
  * [Selecting](#selecting)
  * [Wildcard Operators](#wildcard-operators)
  * [Sorting](#sorting)
  * [Filtering](#filtering)
  * [Aggregating and Calculating](#aggregating-and-calculating)
  * [Order of Execution](#order-of-execution)
  * [Comments](#comments)
  * [Joins](#joins)
  * [Saving Queries](#saving-queries)
- [Final Questions](#final-questions)
- [Additional Resources](#additional-resources)
- [Project Prompts](#project-prompts)
- [Lab Notebook Questions](#lab-notebook-questions)

# Data

1. The following data files are used in this tutorial:
- `Database_Lab_Data.xlsx`
- `Player_Birthplaces.csv`
- `Team_Locations.csv`
- `Combined_Transactions.csv`

2. They can be downloaded as a `zip` folder in this GitHub repo.

3. [Link to access via Google Drive link (ND users only)](https://drive.google.com/drive/folders/1uzjZt4fxTa7qmAIfeTyKNtzT94rhZrf8?usp=sharing)

4. You will need to load this data as a relational database in DB Browser for this lab.

5. Consult [Getting Started with SQLite](https://github.com/kwaldenphd/sqlite-intro) for detailed instructions on creating this database. 

# SQL Syntax

6. As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Structured Query Language, or SQL (sometimes pronounced 'sequel'), is a powerful language used to interrogate and manipulate relational databases. It is not a general programming language that you can use to write an entire program."

7. When working in a relational database, we can use SQL to write queries.

8. As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "a query is a question or request for data. For example, “How many journals does our library subscribe to?” When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria."

9. This section of the lab will introduce some basic elements of SQL syntax. 

## Selecting
```SQL
SELECT [field]
FROM [table];
```

10. The `SELECT` query selects a specific field (column) from a specific table.

11. The semicolon `;` is required at the end of every SQL query.

12. Adding multiple columns after `SELECT` will return data from multiple columns.

```SQL
SELECT [field_1], [field_2], [field_3]
FROM [table];
```

<blockquote>Q1: Write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

13. We might want to write a query to return all the unique values in a particular field.

14. For example, selecting the entire `country` field in the `Player_Birthplaces` table would return many duplicate values.

```SQL
SELECT DISTINCT [field]
FROM [table];
```

15. `SELECT DISTINCT` returns a list of unique values.

<blockquote>Q2: Write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

## Wildcard Operators

16. SQL has a number of wildcard operators that (like regular expressions, or regex commands) can be useful to substitute one or more characters in a string.

Symbol | Description | Example
--- | --- |---
`*` | Represents zero or more characters | `bl*` returns bl, black, blue, and blob
`?` | Represents a single character | `h?t` returns hot, hat, and hit
`[]` | Represents any single character within the brackets | `h[oa]t` returns hot and hat, but not hit
`?` | Represents any character not in the brackets | `h[?oa]t` returns hit, but not hot and hat
`-` | Represents a range of characters | `c[a-b]t` finds cat and cbt
`#` | Represents any single numeric character | `2#5` returns 205, 215, 225, 235, 245, 255, 265, 275, 285, and 295

<blockquote>Check out W3Schools <a href="https://www.w3schools.com/sql/sql_wildcards.asp">"SQL Wildcards"</a> for more on wildcard characters in SQL.</blockquote>

## Sorting

17. We might also want to sort the results returned by a query.

```SQL
SELECT *
FROM [table]
ORDER BY [field] ASC;
```

18. The `*` wildcard operator selects all the fields in a specific table.

19. `ORDER BY` specifies a field to use in sorting the query results.

20. `ASC` returns ascending results. `DESC` would return descending results.

<blockquote>Q3: Write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

```SQL
SELECT *
FROM [table]
ORDER BY [field_1] ASC, [field_2] DESC;
```

21. We can also sort on multiple fields.

22. In the query above, the `ORDER BY` statement sorts `[field_1]` first (ascending) and then sorts `[field_2]` (descending).

<blockquote>Q4: Write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

## Filtering

23. Sometimes we may only want to return values that fall within a specific range or based on a particular set of conditions.

```SQL
SELECT *
FROM Player_Birthplaces
WHERE country='DO';
```

24. This query returns all columns from the `Player_Birthplaces` table where data in the `country` field is equal to `DO`.

25. The data returned by this query includes all the records for players born in the Dominican Republic.

26. Other comparison operators in SQL include:

Operator | Description
--- | ---
`=` | Equal to
`>` | Greater than
`<` | Less than
`>=` | Greater than or equal to
`<=` | less than or equal to
`<>` | Not equal to


<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_42.png?raw=true" alt="Capture_2"  /></p>

27. List of operators that can be used in a `WHERE` clause (from W3Schools [SQL Where Clause page](https://www.w3schools.com/sql/sql_where.asp)).

28. We can also use operators to specify a range for the `WHERE` clause.

```SQL
SELECT *
FROM [Player_Birthplaces]
WHERE dob>1996;
```

29. This query returns all columns from `Player_Birthplaces` where data in the `dob` field is greater than `1996`.

30. SQL query syntax requires single quotes around text values. Numeric fields do not need single quotes.

31. We can also write queries that test for or return values for multiple conditions, using SQL's logical operators.

32. These are called subqueries.

33. For example, what if we wanted to return all records for players born in the Dominican Republic, Venezuela, or Puerto Rico.
```SQL
SELECT *
FROM Player_Birthplaces
WHERE (country = 'DO') OR (country = 'VE') OR (country = 'PR);
```

34. Other SQL operators include:

Operator | Description
--- | ---
`ALL` | TRUE if all subquery values meet the condition
`AND` | TRUE if all the conditions separated by AND is TRUE
`ANY` | TRUE if any of the subquery values meet the condition
`BETWEEN` | TRUE if the operand is within the range of comparisons
`EXISTS` | TRUE if the subquery returns one or more records
`IN` | True if the operand is equal to one of a list of expressions
`LIKE` |  TRUE if the operand matches a pattern
`NOT` | Displays a record if the condition(s) is NOT TRUE
`OR` | TRUE if any of the conditions separated by OR is TRUE
`SOME` | TRUE if any of the subquery values meet the condition

<blockquote>Q5: Write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

35. Learn more about operators at Beginner SQL's [Tutorial on SQL Comparison Keywords](https://beginner-sql-tutorial.com/sql-like-in-operators.htm).

## Aggregating and Calculating

36. SQL contains functions which allow you to make calculations on data in your database for reports. 

37. Some of the most common functions include:
- `MAX`: returns the maximum value in a field
- `MIN`: returns the minimum value in a field
- `AVG`: returns the average value of a field
- `COUNT`: counts the number of values in a field and returns the total
- `SUM`: adds the values in a field and returns the sum

38. Let's say we wanted to get the average birth year for players in our dataset.

39. We can use `AVG` in our query.
```SQL
SELECT AVG(DoB)
FROM Player_Birthplaces;
```

40. We could also get the average birth year grouped by birth country.
```SQL
SELECT AVG(DoB)
FROM Player_Birthpalces
GROUP BY Country;
```

<blockquote>Q6: Write a query that gets average birth year for players in Latin America/Caribbean. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

41. We can filter the results of aggregate functions using the `HAVING` keyword.

42. Let's say we only wanted to see the average birth year for players born after 1990.
```SQL
SELECT AVG(DoB)
FROM Player_Birthplaces
HAVING DoB > 1990;
```

<blockquote>Check out W3Schools <a href="https://www.w3schools.com/sql/sql_operators.asp">"SQL Operators"</a> page to learn more about SQL Operators, including arithmetic, comparison, compound, and logical operators.</blockquote>

<blockquote>Q7: Write a query that gets average birth year for players born after a specific year. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

43. In SQL, we can also perform calculations as part of a query.

44. We can use expressions on a column or multiple columns to get new values during our query.

45. The results of these calculations are known as computed columns.

46. SQL's arithmetic operators include:

Operator | Description
--- | ---
`+` | Add
`-` | Subtract
`*` | Multiply
`/` | Divide
`%` | Modulo

47. For example, let's say we had temperature data in Fahrenheit and needed those values in Celsius, rounded to two decimal places.

48. We could make this conversion using SQL's arithmetic operators.
```SQL
SELECT temp, round(5 * (temp_reading - 32) / 9, 2) as Celsius FROM Temp_Data WHERE quant = 'temp';
```

49. Additional resources:
- Library Carpentry's SQL tutorial, ["Aggregating & Calculating Values"](https://librarycarpentry.org/lc-sql/04-aggregating-calculating/index.html) 
- Software Carpentry's Databases and SQL tutorial, ["Calculating New Values"](https://swcarpentry.github.io/sql-novice-survey/)
- W3Schools' [SQL Tutorial](https://www.w3schools.com/sql/default.asp) pages for specific aggregating and calculating functions.

## Order of Execution

50. SQL queries have an order of execution.

51. SQL clauses are written in a fixed order:
  i. `SELECT`
  ii. `FROM`
  iii. `WHERE`
  iv. `ORDER BY`

52. But the order in which we write these clauses is not the order in which SQL executes them.

53. SQL's order of execution:

Order | Clause | Function
--- | --- | ---
1 | `FROM` and `JOIN` | Choose and join tables to get base data
2 | `WHERE` | Filters the base data
3 | `GROUP BY` | Aggregates the base data
4 | `HAVING` | Filters the aggregated data
5 | `SELECT` | Returns the final data
6 | `ORDER BY` | Sorts the final data
7 | `LIMIT` | Limits the returned data based on row count

54. Why does order of execution matter?

55. If we know the computational pipeline for how SQL executes a query, we can write more effecient and concise queries.

## Comments

56. When the queries become more complex, it can be useful to add comments. 

57. In SQL, comments begin with `--` and end at the end of the line. 
```SQL
-- Select all columns
SELECT *

---From the Player_Birthplaces table
FROM Player_Birthplaces

--Select only records for players born in Canada
WHERE country = CA;
```

## Joins

58. The process of building a relational database in which you identify primary and foreign keys and build relationships across  tables does not change the underlying data structure.

59. We can accomplish this in SQL using `JOIN` functions.

60. According to W3Schools'[SQL Joins page](https://www.w3schools.com/sql/sql_join.asp), "A JOIN clause is used to combine rows from two or more tables, based on a related column between them."

FIGURE 1

Image credit: [Tweet by Hiroaki Yutani](https://twitter.com/yutannihilation/status/551572539697143808?s=20) @yutannihilation (3 January 2015)

61. There are four main types of `JOIN` functions.
- `(INNER) JOIN` returns matching records in both tables
- `LEFT (OUTER) JOIN` returns all records from the left table and only matching records from the right table
- `RIGHT (OUTER) JOIN` returns all records from the right table and only matching records from the left table
- `FULL (OUTER) JOIN` returns all matching records from both the left and right tables

62. We can express these `JOIN` functions programmatically in SQL.

FIGURE 2

Image credit: C.L. Moffatt, ["Visual  Representations of SQL Joins"](https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins) *Code Project* (3 February 2009).

63. Let's write a query that uses the `player_id` field to join the `Transactions` and `Player_Birthplaces` tables.

```SQL
SELECT *
FROM transactions
JOIN player_birthplaces
ON transactions.player_ids = player_birthplaces.player_ids;
```

64. This query uses the `player_id` field and a left join to join the `Transactions` and `Player_Birthplaces` tables.

65. The query returns all columns in the left join query.

66. We could also write this query with the `USING` keyword.
```SQL
SELECT *
FROM transactions
JOIN player_birthplaces
USING (player_ids);
```

<blockquote>Q8: Write an SQL query that joins the Transactions and Team_Locations tables and returns all columns. What kind of join is this? What data does this query return?Test your query using DB Browser. Include code + comments.</blockquote>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_43.gif?raw=true" alt="Capture_2"  /></p>

67. Additional resources:
- W3Schools, ["SQL Joins"](https://www.w3schools.com/sql/sql_join.asp)
- SQL Joins Explained, ["Basic SQL Join Types"](http://www.sql-join.com/sql-join-types)
- ChartIO Data School, "SQL Join Types Explained Visually"](https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/)

## Saving Queries

68. Let's say you have a query or operation you perform frequently or on a regular basis.

69. Having to remember and type out the full query syntax would be cumbersome.

70. SQL gives you the option to save queries in the databases.

71. These saved queries are called Views.

72. Let's say we wanted to create a view for a query that returns all data for teams located in Indiana.

```SQL
CREATE VIEW Indiana_Team_Locations AS
SELECT *
FROM Team_Locations
WHERE state = 'IN';
```

73. Now we have the `Indiana_Team_Locations` view we can access without having to type out the full query.

74. To access the results using the newly-created view:
```SQL
SELECT * 
FROM Indiana_Team_Locations;
```

# Final questions

<blockquote>Q9: Write an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Indiana. Test your query using DB Browser. Include code + comments.</blockquote>

<blockquote>Q10: How would you describe the affordances of relational databases to someone who hasn't been through these labs?</blockquote>

<blockquote>Q11: What questions or thoughts do you have about building and interacting with relational databases?</blockquote>

# Additional Resources
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Tidy Data for Librarians"](https://librarycarpentry.org/lc-spreadsheets/)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "Open Refine"](https://librarycarpentry.org/lc-open-refine/)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)
- [Lucid Chart "Database Design"](https://www.lucidchart.com/pages/database-diagram/database-design)
- [Lucid Chart "ER Diagrams"](https://www.lucidchart.com/pages/er-diagrams)


# Project Prompts

Select one of the following SQL statements:
- `AND/OR`
- `ALTER TABLE`
- `BETWEEN`
- `CREATE`
- `DELETE`
- `DROP`
- `EXISTS`
- `GROUP BY`
- `HAVING`
- `IN`
- `INSERT`
- `JOIN`
- `ORDER BY`
- `SELECT`
- `WHERE`

Write a brief explanation for what the statement will do.

Include an example of how you would use the statement in an SQL query.

Resources:
- https://www.w3schools.com/sql/sql_quickref.asp
- https://www.w3schools.com/sql/sql_syntax.asp

# Lab Notebook Questions

Q1: Write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return? Test your query using DB Browser. Include code + comments.

Q2: Write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table. What data does this query return? Test your query using DB Browser. Include code + comments.

Q3: Write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order. What data does this query return? Test your query using DB Browser. Include code + comments.

Q4: Write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country. What data does this query return? Test your query using DB Browser. Include code + comments.

Q5: Write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M. What data does this query return? Test your query using DB Browser. Include code + comments.

Q6: Write a query that gets average birth year for players in Latin America/Caribbean. What data does this query return? Test your query using DB Browser. Include code + comments.

Q7: Write a query that gets average birth year for players born after a specific year. What data does this query return? Test your query using DB Browser. Include code + comments.

Q8: Write an SQL query that joins the Transactions and Team_Locations tables and returns all columns. What kind of join is this? What data does this query return?Test your query using DB Browser. Include code + comments.

Q9: Write an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Indiana. Test your query using DB Browser. Include code + comments.

Q10: How would you describe the affordances of relational databases to someone who hasn't been through these labs?

Q11: What questions or thoughts do you have about building and interacting with relational database?
