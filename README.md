# SQL Queries and Joins

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab covers the basics of SQL syntax using DB Browser for SQLite. It covers operations like selecting, sorting, filtering, aggregating, and calculating. It also provides an overview of joins, including common join types. 

By the end of this lab, students will be able to:
- Describe the basic syntax of an SQL query, including comments, order of operations, subqueries, and wildcard operators
- Write basic SQL queries that use common operations like SELECT, SORT, and WHERE
- Write basic SQL queries that involve basic aggregation and calculation
- Understand the core concepts of database joins
- Write basic JOIN operations in SQL syntax

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=80085ef5-e5ec-44a1-ac44-ae31012ed0ae">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements
The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

Peer review and editing was provided by Spring 2021 graduate teaching assistant [Eric Tsai Sahoo](https://github.com/milktea292).

# Table of Contents

- [Lecture & Live Coding](#lecture--live-coding)
- [Lab notebook template](#lab-notebook-template)
- [Data](#data)
- [SQL Syntax](#sql-syntax)
  * [Comments](#comments)
  * [Selecting](#selecting)
  * [Sorting](#sorting)
  * [Filtering](#filtering)
    * [Wildcard Operators](#wildcard-operators)
  * [Aggregating and Calculating](#aggregating-and-calculating)
  * [Order of Execution](#order-of-execution)
  * [Joins](#joins)
  * [Saving Queries](#saving-queries)
- [Final Questions](#final-questions)
- [Additional Resources](#additional-resources)
- [Lab Notebook Questions](#lab-notebook-questions)

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=80085ef5-e5ec-44a1-ac44-ae31012ed0ae">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Lab notebook template

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=878a40f7-71bb-4d7f-9809-ae310005db9a">Overview</a></td>
  </tr>
  </table>

[Link to lab notebook template (Google Doc)](https://docs.google.com/document/d/1J6rWJ-KM4dHHKTX8t5veJZRsLpUrfoveY1Mh7L-U8ic/copy)
- DB Browser screenshots are HIGHLY recommended.
  * Windows ([Snipping Tool](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b) for folks running older versions of Windows; [Snip & Sketch](https://www.lifewire.com/snip-and-sketch-windows-10-4774799) for folks running updated versions)
  * [Mac](https://support.apple.com/en-us/HT201361)
  * [Google Chromebook](https://support.google.com/chromebook/answer/10474268?hl=en)
- [Tutorial for adding images/tables/drawings to a Google Doc](https://www.techrepublic.com/article/how-to-add-images-tables-and-drawings-to-a-google-doc-file/)

# Data

In the previous lab, we created a relational database from three `.csv` files.
- [`Player_Birthplaces.csv`](https://drive.google.com/file/d/1qthm3HSN5FaEFusC1_Zk-0qL0A6LIEB-/view?usp=sharing)
- [`Team_Locations.csv`](https://drive.google.com/file/d/1fttQhzoAwYOJC-mB17RATaqD4mfUTIV_/view?usp=sharing)
- [`Combined_Transactions.csv`](https://drive.google.com/file/d/17Z9C7snAMjARTQYoRXufwaO2j9ssl0g8/view?usp=sharing)

Consult the [previous lab's procedure/documentation](https://github.com/kwaldenphd/data-models#getting-started-with-db-browser-for-sqlite) if you need to re-create this database.

You will need to be able to load this relational database in DB Browser for this lab.

If needed, you can download the relational database [from Google Drive](https://drive.google.com/file/d/1uQHOIeMdCZOyXsIdDgfimUE-63I33pIm/view?usp=sharing).

# SQL Syntax

What is SQL? As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Structured Query Language, or SQL (sometimes pronounced 'sequel'), is a powerful language used to interrogate and manipulate relational databases. It is not a general programming language that you can use to write an entire program."

When working with relational database systems, we can use SQL to write queries. As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "a query is a question or request for data. For example, “How many journals does our library subscribe to?” When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria."

## DB Browser Setup

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=369821cf-7dcd-49c0-a516-ae3100068170">DB Browser Setup</a></td>
  </tr>
  </table>

In this lab, we'll be using DB Browser for SQLite (a program we installed in a previous lab) to run SQL statements and queries.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_4.jpg?raw=true" /></p>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_5.jpg?raw=true" /></p>

Open the DB Browser program and select the `Open Database` icon. Open the `.db` file you created in the previous lab (or downloaded at the start of this lab).

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_6.jpg?raw=true" /></p>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_7.jpg?raw=true" /></p>

Click the `Execute SQL` tab. The top text-box on the left-hand pane in the program (immediately below `SQL 1`) is where we will type SQL statements.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_8.jpg?raw=true" /></p>

Once we start adding SQL syntax, we can run all (or a selection) using the single arrow icon (left of the two arrows, immediate right of print). 
- We can use the other arrow (right of the two arrows) to run a single line.

## Comments

We can add single-line comments to our SQL statements using a double dash `--`.

```SQL
-- this is my single-line comment
```

## Selecting

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=157321b3-9c29-44df-984e-ae3100090781">Selecting</a></td>
  </tr>
  </table>

The `SELECT` query selects a specific field (column) from a specific table. The semicolon `;` is required at the end of every SQL query.

```SQL
-- sample syntax for select
SELECT [field]
FROM [table];
```

Adding multiple columns after `SELECT` will return data from multiple columns.

```SQL
-- sample syntax for selecting multiple fields
SELECT [field_1], [field_2], [field_3]
FROM [table];
```

<blockquote>Q1: Write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

We might want to write a query to return all the unique values in a particular field. For example, selecting the entire `country` field in the `Player_Birthplaces` table would return many duplicate values.

```SQL
-- sample syntax for selecting unique values
SELECT DISTINCT [field]
FROM [table];
```

`SELECT DISTINCT` returns a list of unique values.

<blockquote>Q2: Write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

## Sorting

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b09fcbc9-9ad7-4e41-b1cc-ae3100f7a94b">Sorting</a></td>
  </tr>
  </table>

We might also want to sort the results returned by a query.

```SQL
-- sample syntax that selects all values from a table and orders by specific file
SELECT *
FROM [table]
ORDER BY [field] ASC;
```

The `*` wildcard operator selects all the fields in a specific table. `ORDER BY` specifies a field to use in sorting the query results. `ASC` returns ascending results. `DESC` would return descending results.

<blockquote>Q3: Write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

We can also sort on multiple fields.

```SQL
-- sample syntax that selects all values from a table and orders by two fields
SELECT *
FROM [table]
ORDER BY [field_1] ASC, [field_2] DESC;
```

In the query above, the `ORDER BY` statement sorts `[field_1]` first (ascending) and then sorts `[field_2]` (descending).

<blockquote>Q4: Write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

## Filtering

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=f8f38f59-49fa-4413-87ca-ae3100f9903d">Filtering</a></td>
  </tr>
  </table>

Sometimes we may only want to return values that fall within a specific range or based on a particular set of conditions.

```SQL
-- select all values where country = "DO"
SELECT *
FROM Player_Birthplaces
WHERE country='DO';
```

This query returns all columns from the `Player_Birthplaces` table where data in the `country` field is equal to `DO`. The data returned by this query includes all the records for players born in the Dominican Republic.

Other comparison operators in SQL include:

Operator | Description
--- | ---
`=` | Equal to
`>` | Greater than
`<` | Less than
`>=` | Greater than or equal to
`<=` | less than or equal to
`<>` | Not equal to
`BETWEEN` | Between a specified range
`LIKE` | Searches for a pattern based on similarity
`IN` | Specifies multiple possible values for a column

For more on operators  that can be used in a `WHERE` clause (from W3Schools [SQL Where Clause page](https://www.w3schools.com/sql/sql_where.asp)).

We can also use operators to specify a range for the `WHERE` clause.

```SQL
-- select values where dob is greater than 1996
SELECT *
FROM Player_Birthplaces
WHERE dob>1996;
```

This query returns all columns from `Player_Birthplaces` where data in the `dob` field is greater than `1996`. SQL query syntax requires single quotes around text values. Numeric fields do not need single quotes.

We can also write queries that test for or return values for multiple conditions, using SQL's logical operators. These are called **subqueries**. For example, what if we wanted to return all records for players born in the Dominican Republic, Venezuela, or Puerto Rico.

```SQL
-- select all values from table where country equals any of three values
SELECT *
FROM Player_Birthplaces
WHERE (country = 'DO') OR (country = 'VE') OR (country = 'PR');
```

Other SQL operators include:

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

<blockquote>Q5: Write an SQL query to return the data from the Player_Birthplaces table for players before 1985. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

<blockquote>Learn more about operators at Beginner SQL's <a href="https://beginner-sql-tutorial.com/sql-like-in-operators.htm">Tutorial on SQL Comparison Keywords</a>.</blockquote>

### Wildcard Operators

SQL has a number of wildcard operators that (like regular expressions, or regex commands) can be useful to substitute one or more characters in a string.

Symbol | Description | Example
--- | --- |---
`%` | Represents zero or more characters | `bl%` returns bl, black, blue, and blob
`_` | Represents a single character | `h_t` returns hot, hat, and hit
`[]` | Represents any single character within the brackets | `h[oa]t` returns hot and hat, but not hit
`^` | Represents any character not in the brackets | `h[^oa]t` returns hit, but not hot and hat
`-` | Represents a range of characters | `c[a-b]t` finds cat and cbt

When using wildcard characters to search or match a string, we use the `LIKE` operator in combination with the `WHERE` clause.

For example:
```SQL
-- sample syntax for WHERE and LIKE
SELECT *
FROM TABLE
WHERE FIELD LIKE 'WILDCARD EXPRESSION';
```

<blockquote>Check out W3Schools <a href="https://www.w3schools.com/sql/sql_wildcards.asp">"SQL Wildcards"</a> for more on wildcard characters in SQL.</blockquote>

We can use `WHERE` and `LIKE` in combination with wildcard operators to filter records based on string character patterns.

<blockquote>Q6: Write an SQL query to return the data from the Player_Birthplaces table for players born in cities that start with the letter “S”. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

## Aggregating and Calculating

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=f2c6dd4d-2932-4849-87d9-ae3100ff6251">Aggregating & Calculating</a></td>
  </tr>
  </table>

SQL contains functions which allow you to make calculations on data in your database for reports. 

Some of the most common functions include:
- `MAX`: returns the maximum value in a field
- `MIN`: returns the minimum value in a field
- `AVG`: returns the average value of a field
- `COUNT`: counts the number of values in a field and returns the total
- `SUM`: adds the values in a field and returns the sum

Let's say we wanted to get the average birth year for players in our dataset. We can use `AVG` in our query.

```SQL
-- get average DoB from specific table
SELECT AVG(DoB)
FROM Player_Birthplaces;
```

We could also get the average birth year grouped by birth country.

```SQL
-- get average DoB from specific table and group by another field
SELECT AVG(DoB), Country
FROM Player_Birthplaces
GROUP BY Country;
```

<blockquote>Q7: Write a query that gets average birth year for players born in South America or the Caribbean (Region). What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

We can filter the results of aggregate functions using the `HAVING` keyword.
  * NOTE: The `HAVING` keyword has to be used in combination with `GROUP BY`.

Let's say we only wanted to see the average birth year for players born after 1990.

```SQL
-- get average DoB from specific table only for records that meet a specific condition
SELECT AVG(DoB), Country
FROM Player_Birthplaces
GROUP BY Country
HAVING DoB > 1990;
```

<blockquote>Check out W3Schools <a href="https://www.w3schools.com/sql/sql_operators.asp">"SQL Operators"</a> page to learn more about SQL Operators, including arithmetic, comparison, compound, and logical operators.</blockquote>

<blockquote>Q8: Write a query that gets average birth year for players born after a specific year. What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

In SQL, we can also perform calculations as part of a query. We can use expressions on a column or multiple columns to get new values during our query. The results of these calculations are known as **computed columns**.

SQL's arithmetic operators include:

Operator | Description
--- | ---
`+` | Add
`-` | Subtract
`*` | Multiply
`/` | Divide
`%` | Modulo

For example, let's say we had temperature data in Fahrenheit and needed those values in Celsius, rounded to two decimal places. We could make this conversion using SQL's arithmetic operators.

```SQL
-- sample syntax for temperature conversion formula
SELECT temp, round(5 * (temp_reading - 32) / 9, 2) as Celsius FROM Temp_Data WHERE quant = 'temp';
```

Additional resources:
- Library Carpentry's SQL tutorial, ["Aggregating & Calculating Values"](https://librarycarpentry.org/lc-sql/04-aggregating-calculating/index.html) 
- Software Carpentry's Databases and SQL tutorial, ["Calculating New Values"](https://swcarpentry.github.io/sql-novice-survey/)
- W3Schools' [SQL Tutorial](https://www.w3schools.com/sql/default.asp) pages for specific aggregating and calculating functions.

## Order of Execution

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=fba7d1dd-46d5-492d-889e-ae31011d9560">Order of Execution</a></td>
  </tr>
  </table>

SQL clauses are written in a fixed order:
<ol type="i">
<li><code>SELECT</code></li>
<li><code>FROM</code></li>
<li><code>WHERE</code></li>
<li><code>ORDER BY</code></li>
</ol>

But the order in which we write these clauses is not the order in which SQL executes them. SQL's order of execution:

Order | Clause | Function
--- | --- | ---
1 | `FROM` and `JOIN` | Choose and join tables to get base data
2 | `WHERE` | Filters the base data
3 | `GROUP BY` | Aggregates the base data
4 | `HAVING` | Filters the aggregated data
5 | `SELECT` | Returns the final data
6 | `ORDER BY` | Sorts the final data
7 | `LIMIT` | Limits the returned data based on row count

Why does order of execution matter? If we know the computational pipeline for how SQL executes a query, we can write more effecient and concise queries.

## Joins

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=fba7d1dd-46d5-492d-889e-ae31011d9560">Joins</a></td>
  </tr>
  </table>

The process of building a relational database in which you identify primary and foreign keys and build relationships across tables does not change the underlying data structure. We can accomplish this in SQL using `JOIN` functions.

According to W3Schools'[SQL Joins page](https://www.w3schools.com/sql/sql_join.asp), "A JOIN clause is used to combine rows from two or more tables, based on a related column between them."

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_3.jpg?raw=true" /></p>

Image credit: W3 Schools, ["Different Types of SQL Joins"](https://www.w3schools.com/sql/sql_join.asp) (n.d.)

There are four main types of `JOIN` functions.
- `(INNER) JOIN` returns matching records in both tables
- `LEFT (OUTER) JOIN` returns all records from the left table and only matching records from the right table
- `RIGHT (OUTER) JOIN` returns all records from the right table and only matching records from the left table
- `FULL (OUTER) JOIN` returns all matching records from both the left and right tables

We can express these `JOIN` functions programmatically in SQL.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/sql-queries-joins/blob/main/screenshots/Figure_2.png?raw=true"/></p>

Image credit: C.L. Moffatt, ["Visual  Representations of SQL Joins"](https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins) *Code Project* (3 February 2009).

Sample syntax for these examples:

```SQL
-- left join example
SELECT [FIELD(S)]
FROM [TABLE 1]
LEFT JOIN [TABLE 2]
ON table1.field = table2.field;
```

```SQL
-- right join example
SELECT [FIELD(S)]
FROM [TABLE 1]
RIGHT JOIN [TABLE 2]
ON table1.field = table2.field;
```

```SQL
-- inner join example
SELECT [FIELD(S)]
FROM [TABLE 1]
INNER JOIN [TABLE 2]
ON table1.field = table2.field;
```

```SQL
-- full or outer join example
SELECT [FIELD(S)]
FROM [TABLE 1]
FULL OUTER JOIN [TABLE 2]
ON table1.field = table2.field;
```

Let's write a SQL statement that uses the `player_id` field to join the `Transactions` and `Player_Birthplaces` tables.

```SQL
-- left join that joins matching records from player_birthplaces table
SELECT *
FROM combined_transactions
LEFT JOIN player_birthplaces
ON combined_transactions.id_person = player_birthplaces.id_person;
```

This query uses the `player_id` field and a left join to join the `Transactions` and `Player_Birthplaces` tables. The query returns all columns in the left join query.

We could also write this query with the `USING` keyword.

```SQL
-- alternate syntax for left join that joins matching records from player_birthplaces table
SELECT *
FROM combined_transactions
LEFT JOIN player_birthplaces
USING (id_person);
```

<blockquote>Q9: Write an SQL query that joins the Transactions and Team_Locations tables and returns all matching columns from the Transactions table. What kind of join is this? What data does this query return? Test your query using DB Browser. Include code + comments.</blockquote>

Additional resources:
- W3Schools, ["SQL Joins"](https://www.w3schools.com/sql/sql_join.asp)
- SQL Joins Explained, ["Basic SQL Join Types"](http://www.sql-join.com/sql-join-types)
- ChartIO Data School, ["SQL Join Types Explained Visually"](https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/)

## Saving Queries

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5eca72de-d303-4778-9fe0-ae310120d0da">Saving Queries</a></td>
  </tr>
  </table>

Let's say you have a query or operation you perform frequently or on a regular basis. Having to remember and type out the full query syntax would be cumbersome. SQL gives you the option to save queries in the databases. These saved queries are called **Views**.

Let's say we wanted to create a view for a query that returns all data for players born in Puerto Rico.

```SQL
-- syntax for saving a query
CREATE VIEW PR_Players AS
SELECT *
FROM Player_Birthplaces
WHERE country = 'PR';
```

Now we have the `PR_Players` view we can access without having to type out the full query. To access the results using the newly-created view:

```SQL
-- syntax for accessing a saved query
SELECT * 
FROM PR_Players;
```

# Final questions

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=5eca72de-d303-4778-9fe0-ae310120d0da">Final Lab Notebook Questions</a></td>
  </tr>
  </table>

Q10: Write an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Indiana. Test your query using DB Browser. Include code + comments.

Q11: How would you describe the affordances of relational databases to someone who hasn't been through these labs?

Q12: What questions or thoughts do you have about building and interacting with relational databases?

Q13A: Select one of the following SQL statements:
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

Q13B: Write a brief explanation for what the statement will do.

Q13C: Include an example of how you would use the statement in an SQL query.

Resources:
- https://www.w3schools.com/sql/sql_quickref.asp
- https://www.w3schools.com/sql/sql_syntax.asp

# Additional Resources

- [W3 Schools "SQL Tutorial"](https://www.w3schools.com/sql/default.asp)
- [Library Carpentry "SQL Tutorial"](https://librarycarpentry.org/lc-sql/)

# Lab Notebook Questions

[Link to lab notebook template (Google Doc)](https://docs.google.com/document/d/1J6rWJ-KM4dHHKTX8t5veJZRsLpUrfoveY1Mh7L-U8ic/copy)
- DB Browser screenshots are HIGHLY recommended.
  * Windows ([Snipping Tool](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b) for folks running older versions of Windows; [Snip & Sketch](https://www.lifewire.com/snip-and-sketch-windows-10-4774799) for folks running updated versions)
  * [Mac](https://support.apple.com/en-us/HT201361)
  * [Google Chromebook](https://support.google.com/chromebook/answer/10474268?hl=en)
- [Tutorial for adding images/tables/drawings to a Google Doc](https://www.techrepublic.com/article/how-to-add-images-tables-and-drawings-to-a-google-doc-file/)

Q1: Write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return? Test your query using DB Browser. Include code + comments.

Q2: Write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table. What data does this query return? Test your query using DB Browser. Include code + comments.

Q3: Write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order. What data does this query return? Test your query using DB Browser. Include code + comments.

Q4: Write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country. What data does this query return? Test your query using DB Browser. Include code + comments.

Q5: Write an SQL query to return the data from the Player_Birthplaces table for players before 1985. What data does this query return? Test your query using DB Browser. Include code + comments.

Q6: Write an SQL query to return the data from the Player_Birthplaces table for players born in cities that start with the letter “S”. What data does this query return? Test your query using DB Browser. Include code + comments.

Q7: Write a query that gets average birth year for players born in South America or the Caribbean (`Region`). What data does this query return? Test your query using DB Browser. Include code + comments.

Q8: Write a query that gets average birth year for players born after a specific year. What data does this query return? Test your query using DB Browser. Include code + comments.

Q9: Write an SQL query that joins the Transactions and Team_Locations tables and returns all matching columns from the Transactions table. What kind of join is this? What data does this query return? Test your query using DB Browser. Include code + comments.

Q10: Write an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Indiana. Test your query using DB Browser. Include code + comments.

Q11: How would you describe the affordances of relational databases to someone who hasn't been through these labs?

Q12: What questions or thoughts do you have about building and interacting with relational database?

Q13A: Select one of the following SQL statements:
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

Q13B: Write a brief explanation for what the statement will do.

Q13C: Include an example of how you would use the statement in an SQL query.

Resources:
- https://www.w3schools.com/sql/sql_quickref.asp
- https://www.w3schools.com/sql/sql_syntax.asp
