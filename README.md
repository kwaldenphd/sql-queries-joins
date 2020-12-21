# SQL Queries and Joins

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements
The author consulted the following resources when building this tutorial:
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)

# Table of Contents

- [SQL Query Syntax](#sql-query-syntax)
  * [Selecting and Sorting](#selecting-and-sorting)
  * [Filtering](#filtering)
  * [Aggregating and Calculating](#aggregating-and-calculating)
  * [Joins](#joins)
- [Optional: Relational Databases in Excel Using PivotTables](#optional-relational-databases-in-excel-using-pivottables)
- [Additional Resources](#additional-resources)
- [Lab Notebook Questions](#lab-notebook-questions)

# Data

Database_Lab_Data.xlsx

Player_Birthplaces.csv

Team_Locations.csv

Combined_Transactions.csv

Zip in the GitHub

Google Drive link (ND users only) https://drive.google.com/drive/folders/1uzjZt4fxTa7qmAIfeTyKNtzT94rhZrf8?usp=sharing

# SQL Syntax

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Structured Query Language, or SQL (sometimes pronounced 'sequel'), is a powerful language used to interrogate and manipulate relational databases. It is not a general programming language that you can use to write an entire program."

When working in a relational database, we can use SQL to write queries.

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "a query is a question or request for data. For example, “How many journals does our library subscribe to?” When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria."

This section of the lab will introduce some basic elements of SQL syntax. 

BASIC SQL STATEMENT SYNTAX https://www.w3schools.com/sql/sql_syntax.asp

## Selecting
```SQL
SELECT [field]
FROM [table];
```

97- The `SELECT` query selects a specific field (column) from a specific table.

98- The semicolon `;` is required at the end of every SQL query.

99- Adding multiple columns after `SELECT` will return data from multiple columns.

```SQL
SELECT [field_1], [field_2], [field_3]
FROM [table];
```

<blockquote>Q20: Write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return?</blockquote>

100- We might want to write a query to return all the unique values in a particular field.

101- For example, selecting the entire `country` field in the `Player_Birthplaces` table would return many duplicate values.

```SQL
SELECT DISTINCT [field]
FROM [table];
```

102- `SELECT DISTINCT` returns a list of unique values.

<blockquote>Q21: Write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table? What data does this query return?</blockquote>

## SQL has a number of wildcard operators that (like regular expressions, or regex commands) can be useful to substitute one or more characters in a string.

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

103- We might also want to sort the results returned by a query.

```SQL
SELECT *
FROM [table]
ORDER BY [field] ASC;
```

104- The `*` wildcard operator selects all the fields in a specific table.

105- `ORDER BY` specifies a field to use in sorting the query results.

106- `ASC` returns ascending results. `DESC` would return descending results.

<blockquote>Q22: Write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order? What data does this query return?</blockquote>

```SQL
SELECT *
FROM [table]
ORDER BY [field_1] ASC, [field_2] DESC;
```

107- We can also sort on multiple fields.

108- In the query above, the `ORDER BY` statement sorts `[field_1]` first (ascending) and then sorts `[field_2]` (descending).

<blockquote>Q23: Write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country? What data does this query return?</blockquote>

## Filtering

109- Sometimes we may only want to return values that fall within a specific range or based on a particular set of conditions.

```SQL
SELECT *
FROM Player_Birthplaces
WHERE country='DO';
```

110- This query returns all columns from the `Player_Birthplaces` table where data in the `country` field is equal to `DO`.

111- The data returned by this query includes all the records for players born in the Dominican Republic.

Other comparison operators in SQL include:

Operator | Description
--- | ---
`=` | Equal to
`>` | Greater than
`<` | Less than
`>=` | Greater than or equal to
`<=` | less than or equal to
`<>` | Not equal to


<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_42.png?raw=true" alt="Capture_2"  /></p>

List of operators that can be used in a `WHERE` clause (from W3Schools [SQL Where Clause page](https://www.w3schools.com/sql/sql_where.asp)).

112- We can also use operators to specify a range for the `WHERE` clause.

```SQL
SELECT *
FROM [Player_Birthplaces]
WHERE dob>1996;
```

113- This query returns all columns from `Player_Birthplaces` where data in the `dob` field is greater than `1996`.

114- SQL query syntax requires single quotes around text values. Numeric fields do not need single quotes.

We can also write queries that test for or return values for multiple conditions, using SQL's logical operators.

These are called subqueries.

For example, what if we wanted to return all records for players born in the Dominican Republic, Venezuela, or Puerto Rico.
```SQL
SELECT *
FROM Player_Birthplaces
WHERE (country = 'DO') OR (country = 'VE') OR (country = 'PR);
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

<blockquote>Q24: Write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M? What data does this query return?</blockquote>

Learn more about operators at Beginner SQL's [Tutorial on SQL Comparison Keywords](https://beginner-sql-tutorial.com/sql-like-in-operators.htm).

## Aggregating and Calculating

SQL contains functions which allow you to make calculations on data in your database for reports. 

Some of the most common functions include:
- `MAX`: returns the maximum value in a field
- `MIN`: returns the minimum value in a field
- `AVG`: returns the average value of a field
- `COUNT`: counts the number of values in a field and returns the total
- `SUM`: adds the values in a field and returns the sum

Let's say we wanted to get the average birth year for players in our dataset.

We can use `AVG` in our query.
```SQL
SELECT AVG(DoB)
FROM Player_Birthplaces;
```

We could also get the average birth year grouped by birth country.
```SQL
SELECT AVG(DoB)
FROM Player_Birthpalces
GROUP BY Country;
```

<blockquote>QX: Write a query that gets average birth year for players in Latin America/Caribbean</blockquote>

We can filter the results of aggregate functions using the `HAVING` keyword.

Let's say we only wanted to see the average birth year for players born after 1990.
```SQL
SELECT AVG(DoB)
FROM Player_Birthplaces
HAVING DoB > 1990;
```

<blockquote> Check out W3Schools <a href="https://www.w3schools.com/sql/sql_operators.asp">"SQL Operators"</a> page to learn more about SQL Operators, including arithmetic, comparison, compound, and logical operators.</blockquote>

<blockquote>QX: Write a query that gets average birth year for players born in Latin America/Caribbean</blockquote>

In SQL, we can also perform calculations as part of a query.

We can use expressions on a column or multiple columns to get new values during our query.

The results of these calculations are known as computed columns.

SQL's arithmetic operators include:

Operator | Description
--- | ---
`+` | Add
`-` | Subtract
`*` | Multiply
`/` | Divide
`%` | Modulo

For example, let's say we had temperature data in Fahrenheit and needed those values in Celsius, rounded to two decimal places.

We could make this conversion using SQL's arithmetic operators.
```SQL
SELECT temp, round(5 * (temp_reading - 32) / 9, 2) as Celsius FROM Temp_Data WHERE quant = 'temp';
```

Additional resources:
- Library Carpentry's SQL tutorial, ["Aggregating & Calculating Values"](https://librarycarpentry.org/lc-sql/04-aggregating-calculating/index.html) 
- Software Carpentry's Databases and SQL tutorial, ["Calculating New Values"](https://swcarpentry.github.io/sql-novice-survey/)
- W3Schools' [SQL Tutorial](https://www.w3schools.com/sql/default.asp) pages for specific aggregating and calculating functions.

## Order of Execution

SQL queries have an order of execution.

SQL clauses are written in a fixed order:
1. `SELECT`
2. `FROM`
3. `WHERE`
4. `ORDER BY`

But the order in which we write these clauses is not the order in which SQL executes them.

SQL's order of execution:

Order | Clause | Function
--- | --- | ---
1 | `FROM` and `JOIN` | Choose and join tables to get base data
2 | `WHERE` | Filters the base data
3 | `GROUP BY` | Aggregates the base data
4 | `HAVING` | Filters the aggregated data
5 | `SELECT` | Returns the final data
6 | `ORDER BY` | Sorts the final data
7 | `LIMIT` | Limits the returned data based on row count

Why does order of execution matter?

If we know the computational pipeline for how SQL executes a query, we can write more effecient and concise queries.

## Comments

When the queries become more complex, it can be useful to add comments. 

In SQL, comments begin with `--` and end at the end of the line. 
```SQL
-- Select all columns
SELECT *

---From the Player_Birthplaces table
FROM Player_Birthplaces

--Select only records for players born in Canada
WHERE country = CA;
```

## Joins

115- The process of building a relational database in which you identify primary and foreign keys and build relationships across  tables does not change the underlying data structure.

116- We can accomplish this in SQL using `JOIN` functions.

117- According to W3Schools'[SQL Joins page](https://www.w3schools.com/sql/sql_join.asp), "A JOIN clause is used to combine rows from two or more tables, based on a related column between them."

FIGURE 1

Image credit: [Tweet by Hiroaki Yutani](https://twitter.com/yutannihilation/status/551572539697143808?s=20) @yutannihilation (3 January 2015)

120- There are four main types of `JOIN` functions.
- `(INNER) JOIN` returns matching records in both tables
- `LEFT (OUTER) JOIN` returns all records from the left table and only matching records from the right table
- `RIGHT (OUTER) JOIN` returns all records from the right table and only matching records from the left table
- `FULL (OUTER) JOIN` returns all matching records from both the left and right tables

We can express these `JOIN` functions programmatically in SQL.

FIGURE 2

Image credit: C.L. Moffatt, ["Visual  Representations of SQL Joins"](https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins) *Code Project* (3 February 2009).

Let's write a query that uses the `player_id` field to join the `Transactions` and `Player_Birthplaces` tables.

```SQL
SELECT *
FROM transactions
JOIN player_birthplaces
ON transactions.player_ids = player_birthplaces.player_ids;
```

118- This query uses the `player_id` field and a left join to join the `Transactions` and `Player_Birthplaces` tables.

119- The query returns all columns in the left join query.

We could also write this query with the `USING` keyword.
```SQL
SELECT *
FROM transactions
JOIN player_birthplaces
USING (player_ids);
```

<blockquote>Q25: Write an SQL query that joins the Transactions and Team_Locations tables and returns all columns. What kind of join is this? What data does this query return?</blockquote>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_43.gif?raw=true" alt="Capture_2"  /></p>

Additional resources:
- W3Schools, ["SQL Joins"](https://www.w3schools.com/sql/sql_join.asp)
- SQL Joins Explained, ["Basic SQL Join Types"](http://www.sql-join.com/sql-join-types)
- ChartIO Data School, "SQL Join Types Explained Visually"](https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/)

## Saving Queries

Let's say you have a query or operation you perform frequently or on a regular basis.

Having to remember and type out the full query syntax would be cumbersome.

SQL gives you the option to save queries in the databases.

These saved queries are called Views.

Let's say we wanted to create a view for a query that returns all data for teams located in Indiana.

```SQL
CREATE VIEW Indiana_Team_Locations AS
SELECT *
FROM Team_Locations
WHERE state = 'IN';
```

Now we have the `Indiana_Team_Locations` view we can access without having to type out the full query.

To access the results using the newly-created view:
```SQL
SELECT * 
FROM Indiana_Team_Locations;
```

# Final questions

<blockquote>Q26: Write an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Indiana</blockquote>

<blockquote>Q27: How would you describe the affordances of relational databases to someone who hasn't been through these labs?</blockquote>

<blockquote>Q28: What questions or thoughts do you have about building and interacting with relational databases?</blockquote>

# Thursday interactive prompt

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

# Project Prompts

dsfj kdasfjfdfk

# Additional Resources
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Tidy Data for Librarians"](https://librarycarpentry.org/lc-spreadsheets/)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "Open Refine"](https://librarycarpentry.org/lc-open-refine/)
- [Library Carpentry "SQL"](https://librarycarpentry.org/lc-sql/)
- [Lucid Chart "Database Design"](https://www.lucidchart.com/pages/database-diagram/database-design)
- [Lucid Chart "ER Diagrams"](https://www.lucidchart.com/pages/er-diagrams)

# Lab Notebook Questions

Q1: What questions do you have about these principles? Which ones are unclear are confusing?
   
Q2: What fields are represented in these datasets? Describe the data fields in your own words. Use the language of string, double, and integer to describe the data fields.
    
Q3: Provide 3 distinct examples from the sample datasets that do not conform to tidy data principles. Include the example as well as an explanation.

Q4: Discuss with a colleague what issues you are seeing in these datasetes. What commonalities or patterns are you seeing?

Q5: How would you address these pattern errors so the data conforms to tidy data principles? Describe what steps you would take to address at least 3 pattern errors. For each error, include the following elements: an example of the error, an explanation of your method to address the error, and the same example as tidy data.
    
Q6: Compare your experience working in OpenRefine to other experiences you have had in a text editor or spreadsheet program. In what ways do you understand, perceive, or relate to the data differently through working in OpenRefine? Describe your experience cleaning this data in OpenRefine.

Q7: Describe a past experience working with a spreadsheet program. What were you trying to do? How did it go? What was your overall feeling about working with data in a spreadsheet program?

Q8: Compare your experience working in Excel to your experience working in OpenRefine. In what ways do you understand, perceive, or relate to the data differently through working in Excel? Describe your experience cleaning this data in Excel.

Q9: For the baseball datasets we have been working with in this lab, what do you think may have contributed to or caused the pattern errors we needed to address? How could these pattern errors be addressed in the data entry process?

Q10: Describe how you would go about building a survey form or template for the `CSC_Database_Lab_PlayerBirthplaces.csv` file. You DO NOT need to actually create or submit a survey form. Describe what types of questions and pre-defined question or field options could you use to more effectively generate the data in this file.

Q11: Describe how you would go about using data validation to build a template for the `CSC_Database_Lab_PlayerBirthplaces.csv` file. You DO NOT need to actually create or submit a template. Describe what data validation options and pre-defined field options could you use to more effectively generate the data in this file.

Q12: What types of fields do you see in the Transactions table? What kinds of connections could you see across these three tables?

Q13: What entities are in the Player_Birthplaces, Team_Locations, and Transactions tables? List the entitites by table and include some explanation of your thought process. If you're getting stuck, try describing the data included in each table using a sentence. Where are the nouns in each sentence?

Q14: What attributes are in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these attributes describe? List the attributes by entity and table and include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. What non-entity information in each table might describe an entity?

Q15: What relationships do you see within and across entities in the Player_Birthplaces, Team_Locations, and Transactions tables? What entities do these relationships connect? Include some explanation of your thought process. If you're getting stuck, go back to your list of entities from Q13. How do these entities connect?

Q16: Include the cardinality for the relationships you identified in Q15. Include some explanation of your thought process.

Q17: Work with a colleague to build an ERD for the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.

Q18: What fields in our tables are functioning as keys? Which ones are primary keys and which ones are foreign keys? Include some explanation of your thought process.

Q19: Work with a colleague to build a relational schema for a relational database that includes the Player_Birthplaces, Team_Locations, and Transactions tables. Include your diagram as well as an explanation of your process.

Q20: How would you write an SQL query to select the list of player ids and birthplace countries from the Player_Birthplaces table? What data does this query return?

Q21: How would you write an SQL query to return the unique list of player birthplace countries from the Player_Birthplaces table? What data does this query return?
 
Q22: How would you write an SQL query to return the unique list of team names from the Team_Locations table, sorted in reverse alphabetical order? What data does this query return?
  
Q23: How would you write an SQL query to return the data from the Player_Birthplaces table, sorted in chronological order by birth year and reverse alphabetical order by country? What data does this query return?
   
Q24: How would you write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M? What data does this query return?
   
Q25: How would you write an SQL query that joins the Transactions and Team_Locations tables and returns all columns? What data does this query return?
    
Q26: Where would you start in writing an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Iowa?

Q27: How would you describe the affordances of relational databases to someone who hasn't been through this lab?

Q28: What questions or thoughts do you have about building and interacting with relational databases?

