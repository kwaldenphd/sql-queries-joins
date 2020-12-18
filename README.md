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

# SQL Query Syntax

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "Structured Query Language, or SQL (sometimes pronounced 'sequel'), is a powerful language used to interrogate and manipulate relational databases. It is not a general programming language that you can use to write an entire program."

When working in a relational database, we can use SQL to write queries.

As described in Library Carpentry's [Introduction to SQL tutorial](https://librarycarpentry.org/lc-sql/01-introduction/index.html), "a query is a question or request for data. For example, “How many journals does our library subscribe to?” When we query a database, we can ask the same question using a common language called Structured Query Language or SQL in what is called a statement. Some of the most useful queries - the ones we are introducing in this first section - are used to return results from a table that match specific criteria."

This section of the lab will introduce some basic elements of SQL syntax. 

## Selecting and Sorting
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
FROM [Player_Birthplaces]
WHERE country='DO';
```

110- This query returns all columns from the `Player_Birthplaces` table where data in the `country` field is equal to `DO`.

111- The data returned by this query includes all the records for players born in the Dominican Republic.

112- We can also use operators to specify a range for the `WHERE` clause.

```SQL
SELECT *
FROM [Player_Birthplaces]
WHERE dob>1996;
```

113- This query returns all columns from `Player_Birthplaces` where data in the `dob` field is greater than `1996`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_42.png?raw=true" alt="Capture_2"  /></p>

List of operators that can be used in a `WHERE` clause (from W3Schools [SQL Where Clause page](https://www.w3schools.com/sql/sql_where.asp)).

114- SQL query syntax requires single quotes around text values. Numeric fields do not need single quotes.

<blockquote>Q24: Write an SQL query to return the data from the Team_Locations table for teams located in states that start with the letter M? What data does this query return?</blockquote>

Learn more about operators at Beginner SQL's [Tutorial on SQL Comparison Keywords](https://beginner-sql-tutorial.com/sql-like-in-operators.htm).

## Aggregating and Calculating

We won't cover these functions in this lab, but SQL syntax includes functions that can group query results by particular fields and perform basic arithmetic functions on values in a database.

To learn more, visit Library Carpentry's [Aggregating & calculating values page](https://librarycarpentry.org/lc-sql/04-aggregating-calculating/index.html) and W3Schools' [SQL Tutorial](https://www.w3schools.com/sql/default.asp) pages for specific aggregating and calculating functions.

## Joins

115- The process of building a relational database in which you identify primary and foreign keys and build relationships across  tables does not change the underlying data structure.

116- We can accomplish this in SQL using `JOIN` functions.

117- According to W3Schools'[SQL Joins page](https://www.w3schools.com/sql/sql_join.asp), "A JOIN clause is used to combine rows from two or more tables, based on a related column between them."

```SQL
SELECT *
FROM [transactions]
JOIN [player_birthplaces]
ON transactions.player_ids = player_birthplaces.player_ids;
```

118- This query uses the `player_id` field to join the `Transactions` and `Player_Birthplaces` tables.

119- The query returns all columns in the joined query.

<blockquote>Q25: How would you write an SQL query that joins the Transactions and Team_Locations tables and returns all columns?  What data does this query return?</blockquote>

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_43.gif?raw=true" alt="Capture_2"  /></p>

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

SOME EXCERCISES THAT JOIN OUR TABLES

Learn more about `JOIN` functions at W3Schools' [SQL Joins page](https://www.w3schools.com/sql/sql_join.asp).

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

