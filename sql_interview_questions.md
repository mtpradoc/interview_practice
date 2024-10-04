# Easy

1. What is the difference between a table and a view?
   A table is a preliminary storage for storing data in a relational database management system. A view is a virtual table and is subset of a table or tables and tipically does not take up as much space as a table.

2. How would you write a query that would only select unique records in a column?

```
SELECT DISTINCT(column)
FROM table
```

3. I have 2 columns called drug_name and drug_price. Each drug has different prices depending on where it is being sold. I want to see the drug name with the highest price it is being sold at. How would you write that query?

```
SELECT
  drug_name,
  MAX(drug_price)
FROM drugs
```

4. What does GROUP BY (statement) do in a query? And why would you use it?

   The Group By statement statement groups rows that have the same value into summary rows and are typically use with aggregate functions to look at specific data in the dataset in a more organized manner.

5. I have a column drug_name. I want to look at drugs that start with "Aspirin". How would you only return names that start with Aspirin?

```
   SELECT
     drug_name
   FROM drugs
   WHERE drug_name LIKE 'Aspriri%'
```
# Intermediate

1. What is a subquery and can you describe how would you write that?
   A subquery is a query nested inside of a larger query.

   ```
   SELECT *
   FROM table
   WHERE user_id IN
   (SELECT userid
   FROM table_2)
   ```

2. What is a JOIN and what data would be returned if you use an INNER JOIN?
   
  A join combines two tables into a single output. An INNER JOIN will return data that is intersects (or is common) between both tables. For example: if Table 1 has a, b and c and Table 2 has b and c. Only b and c will be returned because a is only in Table 1.

3. What is the difference between an INNER and OUTER JOIN?

   An inner join will return data that intersects (or is common) between both tables whereas an OUTER JOIN will return all of one table and the instersection of both tables or will return everything from both tables whethere they intersect or not.

4. What is a CASE statement? And how would you write it?
   The CASE statement goes through conditions and returns a value when the first condition is met (like an IF-THEN-ELSE statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the ELSE clause. 
It can be written like this:

  ```
  SELECT
    CASE
      WHEN column > 2 THEN 'output_1'
      ELSE 'output_2'
    END
  FROM table
  ```

5. What is UNION (operator)? And how would you write it?

   The UNION operator is used to combine the result-set of two or more SELECT statements.

   ```
   SELECT
     column1,
     column2
   FROM table1
   UNION
   SELECT
     column1,
     column2
   FROM table2
   ```

6. I have 2 tables. One table contains patient information and the other contains drug information. In the patient table we have patient_id, first_name, last_name, and disease. In the drug table we have patiend_id, dispensed_drug, date_dispensed. Can you create a query to return the patient_id, disease, and dispensed_drug?

   ```
   SELECT
     p.patient_id,
     p.disease,
     d.dispensed_drug
   FROM patient p
   JOIN drug d ON p.patient_id=d.patient_id;
   ```

# Difficult

1.	What are sys tables or System tables?

sys.tables is a system table and is used for maintaining information on tables in a database. For every table added to the database, a record is created in the sys.tables table. There is only one record for each table and it contains information such as table name, object id of table, created date, modified date, etc. Object ID is unique and we will use it to join this table with other system tables (sys.columns) in order to fetch column details.

2.	What does the ISNULL function do?

Example Answer: ISNULL returns the specified value IF the expression is NULL, otherwise return the expression.

3.	What is a temp table and how do you use it?

Example Answer: A temporary table in SQL Server, as the name suggests, is a database table that exists temporarily on the database server. A temporary table stores a subset of data from a normal table for a certain period of time.
You can use it by specifying the Table Name, Column Names, and Data Types of you Temp Table and then storing data into that table. You can then query the temp table to look at that data.


