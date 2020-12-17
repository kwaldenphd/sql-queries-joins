# Lab #7: Joins

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

## Acknowledgements
The author consulted the following resources when building this tutorial:
- [W3 Schools "Syntax"](https://www.w3schools.com/sql/default.asp)
- [W3 Schools "SQL Syntax"](https://www.w3schools.com/sql/sql_syntax.asp)
- [Library Carpentry "Tidy Data for Librarians"](https://librarycarpentry.org/lc-spreadsheets/)
- [Library Carpentry "Database Design"](https://librarycarpentry.org/lc-sql/08-database-design/index.html)
- [Library Carpentry "Open Refine"](https://librarycarpentry.org/lc-open-refine/)
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

120- There are four main types of `JOIN` functions.
- `(INNER) JOIN` returns matching records in both tables
- `LEFT (OUTER) JOIN` returns all records from the left table and only matching records from the right table
- `RIGHT (OUTER) JOIN` returns all records from the right table and only matching records from the left table
- `FULL (OUTER) JOIN` returns all matching records from both the left and right tables

Learn more about `JOIN` functions at W3Schools' [SQL Joins page](https://www.w3schools.com/sql/sql_join.asp).

<blockquote>Q26: Where would you start in writing an SQL query that answers our question about the number of players born in Puerto Rico playing for teams located in Iowa?</blockquote>

<blockquote>Q27: How would you describe the affordances of relational databases to someone who hasn't been through this lab?</blockquote>

<blockquote>Q28: What questions or thoughts do you have about building and interacting with relational databases?</blockquote>

# Optional: Relational Databases in Excel Using PivotTables

121- We can also work within Microsoft Excel to connect our three tables so we can utilize some of the features and functionality of a relational database from within Excel.

122- Open the Excel workbook you created earlier in this lab.

123- Load the `Transactions` file in a new sheet. 

124- Now you should have three sheets in the same Excel workbook.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_33.png?raw=true" alt="Capture_2"  /></p>

125- Under the `Data` menu area, select the `Relationships` option.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_34.png?raw=true" alt="Capture_2"  /></p>

126- In the `Manage Relationships` window, select `New`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_35.png?raw=true" alt="Capture_2"  /></p>

127- Use the relational schema you built in Q19 to create relationships across the three tables.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_36.png?raw=true" alt="Capture_2"  /></p>

128- Once you've added relationships, close the `Manage Relationships` window.

129- Save your workbook.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_37.png?raw=true" alt="Capture_2"  /></p>

130- Select the `Manage Data Model` option under `Data`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_38.png?raw=true" alt="Capture_2"  /></p>

131- You can select the `Diagram View` option to see the relational schema you have built in Excel.

132- Close the Power Pivot window.

133- Create a new blank sheet.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_39.png?raw=true" alt="Capture_2"  /></p>

134- Select `PivotTable` under `Insert`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_40.png?raw=true" alt="Capture_2"  /></p>

135- In the `Create PivotTable` window, select the option to `Use this workbook's Data Model` and select the `Existing Worksheet` for the PivotTable location.

136- Click `OK`.

<p align="center"><img class=" size-full wp-image-55 aligncenter" src="https://github.com/kwaldenphd/databases/blob/master/screenshots/Image_41.png?raw=true" alt="Capture_2"  /></p>

137- You are now in the PivotTable interface where you can select data fields across tables using the relationships and data model.

<blockquote>From within the PivotTable, how could you select data fields to answer our question about the number of baseball players born in Puerto Rico who played for teams in Iowa? Describe your process and include a screenshot of the resulting PivotTable.</blockquote>

# Additional Resources

- [W3 Schools "Syntax"](https://www.w3schools.com/sql/default.asp)
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

