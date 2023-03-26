# SQL-for-Data-Science

## Table of Contents
- [**Section 1: Selecting and Retrieving data**]




## Section 1: Selecting and Retrieving data
### What is SQL is Anyway?
- The acronym SQL stand for Structured Query language
- SQL is the standard language for relational database management and for data manipulation
- SQL is used to Read/retrieve, Write and Update data
- Database administrator governs entire database
- Data Scientist basically the end user of database
- Data Scientists do little analysis using SQL, but the main thing SQL is used to retrieve data.
- There are various Relational Database Management Systems in this class We will be using SQLite.
- Notice syntax might differ when using MySQL or etc.

### Data Models, Part 1
- Think why you need the data.
- Database is a container to store organized data
- Tables a structured list of data of specific type
- Column is a single field in a table
- row is a record in a table

### Data models, Part 2, Evolution of data modelling
- Data modeling is what we use to organize information for multiple tables and how they relate with each other
- Data model scheme of organization should represent real world as closely as possible
- Relational Data model simplifies connections between data
- NoSQL is a mechanism for retrieval fo unstructured data. It is non-relational database

### Data models, Part 3, Relational vs, Transactional models
 - in Transactional database information is not stored in a way thats conducive to quering and analysis
 - Data Model is built from Entities, Attributes and Relationships
 - Relationships:
    - One to many i.e. customer to invoices
    - Many to many i.e. student to classes
    - one to one i.e. manager to store
 - To understand Relationships we use Entity-Relationship(ER) diagrams
 - To join tables in ER diagrams we use keys:
    - Primary key is a column whose values uniquely identify every row in a table
    - Foreign key is one or more columns use together to identify single row in another table
 - There 3 ER diagram Notations:
    - [Chen](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Chen-notation.png?raw=true)
    - [Crow-Foot](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Crow-foot-notation.png?raw=true)
    - [UML](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/UML-notation.png?raw=true)

### Retreiving Data With SELECT

- SELECT statment retrieves all(*) or particular columns from a table
- FROM tells which table to look at

```SQL
SELECT prod_name,
From Products;
```
Output:
```SQL
*prod_name*
Shampoo
Toothpaste
Deodorant
```
**Main concept**
```
SELECT columns you wish to see
FROM specific table
LIMIT number of records;
```
### Creating Tables
 - Tables allow creating dashboards and visualising data

```
CREATE TABLE Shoes
(
    Id      char(10)        PRIMARY KEY,
    Brand   char(250)       NOT NULL,
    Price   decimal(8,2)    NOT NULL,
    Desc    Varchar(750)    NULL
);
```
 - NULL Value is absence of everything.
 - Primary Keys must have a value

Adding data to the table:
```
INSERT INTO Shoes
(Id,Brand,Type,Color,Price,Desc)
VALUES
('14325423','Gucci','Slippers','Pink','711.01',NULL);
```
### Creating Temporary Tables

 - Temporary tables will be deleted when current session will be terminated
 - Benefits of creating Temporary tables:
    - Fatser than creating a real table
    - Allows simplifying complex queries
```SQL
CREATE TEMPORARY TABLE Sandals AS
(
    SELECT *
    FROM shoes
    WHERE shoe_type = 'sandals'
)
```
### Adding Comments to SQL

 - Comments help yo remember what you were doing and why
 - Comments can also mute the code
Two ways to add comments:
 - Single line
 ```SQL
 SELECT shoe_id
 - -, brand_id
 ,shoe_name
 from shoes
 ```
 - Section
 ```SQL
 SELECT shoe_id
 /*, brand_id
 ,shoe_name
 */
 from shoes
 ```
 - Enviroment seperate from database where you can write and edit code i.e. Notepad++

### Pactice Simple Select Queries

I put here only few examples, since most of them are fairly easy queries.

Ex-1
Retrieve all the data from the tracks table. Who is the composer for track 18?
 ```SQL
Select composer
From Tracks
LIMIT 18;
 ```

Ex-3
Retrieve all data from the invoices table. What is the billing address for customer 31?
```SQL
Select CustomerId, BillingAddress
From Invoices;
```
### Overview of Section 1

 The following are supplementary recources I liked:
  - [NTC Hosting: Structured Query Language (it's worth exploring this site, not just this singular posting)](https://www.ntchosting.com/encyclopedia/databases/structured-query-language/)
  - [SQLite Tutorial](https://www.tutorialspoint.com/sqlite/index.htm)
  - [Norwalk Aberdeen: Entity-Relationship Diagrams](https://www.youtube.com/watch?v=c0_9Y8QAstg)
  - [Dataconomy: SQL vs. NoSQL - What You Need to Know](http://dataconomy.com/2014/07/sql-vs-nosql-need-know/)
  Example: Instead of storing data in rows and columns in a table, data is stored in documents, and these documents are grouped together in collections. Each document can have a completely different structure.
  *Certainly, SQL is not dead yet.*
  - [TechRepublic: NoSQL keeps rising, but relational databases still dominate big data](https://www.techrepublic.com/article/nosql-keeps-rising-but-relational-databases-still-dominate-big-data/)

## Section 2: Filtering of Data

### Basics of Filtering in SQL

 - Filtering benefits:
    - reduces number of records when retrieving
    - increse query performence
    - ensures you get data you want

  ```SQL
  SELECT column_name, column_name
  FROM table_name
  WHERE column_name operator value;
  ```
  Where operator values are: =,>,<.>=,<=, BETWEEN, IS NULL, <> (not equal or !=)

  i.e
  ```SQL
  SELECT ProductName, UnitPrice, SupplierID
  FROM Products
  WHERE UnitPrice >= 75;
  ```
 or
  ```SQL
  SELECT ProductName, UnitPrice, SupplierID
  FROM Products
  WHERE UnitPrice BETWEEN 15 AND 80;
  ```
### Advance Filtering: operators In, Or, and Not

 ```SQL
  SELECT ProductID, UnitPrice, SupplierID
  FROM Products
  WHERE SupplierID IN (9,10,11);
  ```
  ```SQL
  SELECT ProductID, SupplierID, ProductName
  FROM Products
  WHERE ProductName = 'Tofu' OR 'Konbu';
  ```
  Benefits of IN:
   - IN executes faster than OR
   - Dont have to think about order with IN
   - Can contain another SELECT
 
 Or with AND
  ```SQL
  SELECT ProductID, SupplierID, UnitPrice
  FROM Products
  WHERE (SupplierID = 9 OR SupplierID = 11)
  AND UnitPrice > 15;
  ```
  Notice SQL excecutes AND first and then OR. Thats why using () is very important

```SQL
  SELECT *
  FROM Employees
  WHERE NOT City = 'London' AND NOT City = 'Seattle';
  ```

### Using Wildcards in SQL

 - Wildcard is a special character used to match parts of a value.
 - Wildcard is used as Like operator
 - Wildcards can only used with strings

 | Wildcard | Action |
 | -------- | ------ |
 |'%Pizza' |Grabs anything ending with word pizza|
 |'Pizza%' |Grabs anything after word pizza|
 |'%Pizza%'|Grabs anything before and after word pizza|
 |'S%E' | Grabs anything that starts with 'S' and ends with 'E' (Sadie)|
 |'t%@gmail.com'|Grabs gmail addresses that start with 't'|

 ```SQL
  WHERE size LIKE '%pizza'
  Output: spizza, mpizaa
  ```
 - In SQLite we can use _ instead of %
 - Downsides fo Wildcards is that it takes longer to run. If possible use different operator

### Sorting with ORDER BY
 - Sorting data helps to keep information you want on top
 - ORDER BY should be the last in select statement
 - ORDER BY can sort by column position or column names
  ```SQL
  ORDER BY 2,3
  ```
  - Sort direction:
     - Descending order DESC
     - Ascending order ASC

 ```SQL
 SELECT Biweekly_low_Rate
 From salary_range_by_job_classification
 ORDER BY Biweekly_low_Rate ASC
```

### Math Operations
 | Operator | Description |
 | -------- | ----------- |
 | + | Addition|
 | - | Substraction|
 | * | Multiplication|
 | / | Division |

  ```SQL
  SELECT ProductID, UnitsOnOrder, UnitPrice, UnitsOnOrder * UnitPrice AS Total_Order_Cost
  FROM Products;
  ```
### Aggregate Functions
| Function | Description |
| -------- | ----------- |
| AVG() | Averages column values |
| COUNT() | Counts number of values |
| MIN() | Finds minimum value |
| Max() | Finds maximum value |
| SUM() | Sums column values |

  ```SQL
  SELECT AVG(UnitPrice) AS avg_price
  FROM Products
  ```
  ```SQL
  SELECT Count(CustomerID) AS total_customers
  FROM Customers
  ```
  ```SQL
  SELECT SUM(UnitPrice*UnitsInStock) AS total_price
  FROM Products
  WHERE SupplierID = 23;
  ```
 - If DISTINCT is not specified, all is assumed
  ```SQL
  SELECT COUNT(DISTINCT CustomerID)
  FROM Customers
  ```
### Grouping Data with SQL

 - New Clauses GROUP BY; HAVING

  ```SQL
  SELECT Region, 
  COUNT(DISTINCT CustomerID) as total_customers
  FROM Customers
  GROUP BY Region;
  ```
  - Every column in your SELECT statement must be present in a GROUP BY clause, except for aggregated calculations
  - NULLS will be grouped together

 Having Clause - Filtering for Groups
  - WHERE does not work for groups so we use HAVING
  - WHERE filters on rows
 
  ```SQL
  SELECT CustomerID, COUNT(*) AS orders
  FROM Orders
  GROUP BY CustomerID
  HAVING COUNT (*) >=2;
  ```
  - WHERE filters before data is grouped
  - HAVING filters after data is grouped
  - Rows eliminated by WHERE clause will not be included in group
  - ORDER BY sorts data
  - GROUP BY does not sort data

### Overview of Section 2
| Clause | Description | Required |
| ------ | ----------- | -------- |
| SELECT | Columns to be returned | Yes |
| FROM | Table from which to retrieve data | Only if selecting data from a table |
| WHERE | Row-level filtering | No |
| GROUP BY | Group specification | Only if calculating aggregates by group |
| HAVING | Group-level filter | No|
| ORDER BY | Output sort order | No |

 - Clauses should be written in this order

### Practice filtering data

What is the Biweekly High Rate minus the Biweekly Low Rate for job Code 0170?

``` SQL
SELECT
 Biweekly_low_Rate,
 Biweekly_high_Rate,
 job_Code,
 Biweekly_high_Rate - Biweekly_low_Rate AS difference
FROM salary_range_by_job_classification
WHERE job_Code = '0170';
```
What is the pay type for all the job codes that start with '03'? 

```SQL
Select
job_code,
pay_type
From salary_range_by_job_classification
WHERE job_code LIKE '03%'
```

What is the step for Union Code 990 and a Set ID of SFMTA or COMMN? 
```SQL
SELECT step, Union_Code, SetID
FROM salary_range_by_job_classification
WHERE Union_Code = '990' AND (SetID = 'SFMTA' OR SetID = 'COMMN')
```
Find all the invoices for customer 56 and 58 where the total was between $1.00 and $5.00.
```SQL
SELECT InvoiceID, customerID, total, InvoiceDate
From Invoices
WHERE (total between 1 and 5) AND (customerID IN (56,58))
```
Find all the invoices from the billing city Brasília, Edmonton, and Vancouver and sort in descending order by invoice ID. What is the total invoice amount of the first record returned? 
```SQL
SELECT InvoiceId, BillingCity
From Invoices
Where BillingCity IN ('Brasília', 'Edmonton', 'Vancouver')
Order By InvoiceId DESC
```
Show the number of orders placed by each customer and sort the result by the number of orders in descending order.
```SQL
Select CustomerID, count(InvoiceID) AS number_of_orders
From Invoices
Group By CustomerID
Order by number_of_orders DESC
```
Find the albums with 12 or more tracks.
```SQL
SELECT AlbumId, count(trackId) AS number_of_tracks 
From Tracks
Group BY AlbumId
HAVING number_of_tracks >= 12
```
### SQL for Data Science Languages
Some supplementary recources I liked
 - [Python-SQL Package Documentation](https://pypi.org/project/python-sql/)
 
## Subqueries and Joins with SQL
### Using Subqueries
 - Subqueries are queries embedded into other queries
 - Subqueries merge data from multiple sources together
 - Subqueries allows to add additional filtering options
 - Subqueries makes retrieving data more efficient
Example:
Need to know the region each customer is from who has had an order with freight over 100
Solution without subquery: 
  - Retrieve all customer IDs for orders with freight over 100
  - Retrieve customer information
  - Combine the two queries
```SQL
SELECT Distinct customerID
From Orders
Where Freight > 100
```
```SQL
SELECT CustomerID, CompanyName, Region
From Customers
Where cusomerID IN ('RICSU','ERNSH', 'FRANK', 'WARTH')
```
Solution with subquery:
```SQL 
SELECT CustomerID, CompanyName, Region
From Customers
WHERE CustomerID in (
  SELECT CustomerID 
  From Orders
  Where Freight >100 );
```
 - When working with subquery always perform the innermost SELECT portion first

### Subquery Best Practices and Considerations
 - There is no limit to the number of subqueries you can have
 - Performance slows when you nest too deeply
 - Subquery selects can only retrieve a single column

Subqueries can be used for calculations
```SQL 
SELECT customer_name, customer_state, (
  SELECT COUNT (*)
  FROM Orders
  WHERE Orders.customer_id = Customer.customer_id) AS orders
FROM customers
ORDER BY Customer_name
```
So Subqueries can be used in WHERE clause and in SELECT statement

### Joining Tables: An Introduction
The benifits of segmenting data in different tables:
 - Logically models a process within a business, this helps to understand the way business works in the real world
 - Easier to manipulate data
 - Efficient storage, no duplicates
 - Greater scalability

  - Joins associate correct records from each table on the fly
  - Joins allows data retrieval from multiple tables in one query
  - Joins are not physical entities

### Cartesian (Cross) Joins
[CROSS JOINs](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Cross_join.png): each row from the first table joins with all the rows of another table

```SQL
SELECT product_name, unit_price, company_name
FROM suppliers CROSS JOIN products;
```
Output of a CROSS JOIN will be the number of joins in the 1st table multiplied by number of rows in the 2nd table

  - Cross Joins not frequently used because they are computationally taxing

### Inner Joins
The INNER JOIN keyword selects records that have matching values in both tables
```SQL
SELECT suppliers.CompanyName, ProductName, UnitPrice
FROM Suppliers INNER JOIN Products
ON Suppliers.supplierid = Products.supplierid
```
 - Join condition is in the FROM clause and uses the ON clause
 - Joining more tables together affects overall database performance
 - You can join multiple tables
```SQL
SELECT o.OrderID, c.CompanyName, e.LastName
FROM ((Orders o INNER JOIN Customers c
ON o.CustomerID = c.CustomerID)
INNER JOIN Employees e
ON o.EmployeeID = e.EmployeeID);
```

### Aliases and Self Joins
SQL aliases give a table or a column a temporary name which exits for the duration of the query
```SQL
SELECT column_name
FROM table_name AS alias_name
```
Some examples of Joins with Alias
```SQL
SELECT vendor_name, product_name, product_price
FROM Vendors, Products
WHERE Vendors.vendor_id = Products.vendor_id;
```
```SQL
SELECT vendor_name, product_name, product_price
FROM Vendors AS v, Products AS p
WHERE v.vendor_id = p.vendor_id;
```
Self Joins the original table to itself
The following example matches customers that are from the same city
```SQL
SELECT A.CustomerName AS CustomerName1,
B.CustomerName AS CustomerName2, A.City
FROM Customers (AS) A, Customers (AS) B
WHERE A.CustomerID = B.CustomerID
AND A.City = B.City
ORDER BY A.City
```
 - When using Alias we can ommit AS part

### Advanced Joins, Left, Right and Full Outer Joins
 - SQL Lite uses only Left Joins
 - [Left Join](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Left_join.png) Returns all records from the left table (table1), and the matched records from the right table (table2)
 - Right Join Returns all records from the right table (table2), and the matcherd records from the left table
 - The result is NULL if there is no match
 - Full Outer Join Returns all records when there is a match either left or right table records

```SQL 
SELECT C.CustomerName, O.OrderID
FROM Customer C
LEFT JOIN Orders O ON C.CustomerID = O.CustomerID
ORDER BY C.CustomerName;
```
```SQL
SELECT Orders.OrderID, Employees.name
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID =Employees.EmployeeID
ORDER BY Orders.OrderID;
```
```SQL
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```
### Unions
 - The UNION operator is used to combine result-set of two or SELECT statements
 - Each SELECT statement within UNION must have the same number of columns
 - Columns must have similar data types
 - The columns in each SELECT must be in the same order
 - Union basically stacks tables together
 ```SQL
 SELECT column_name(s)
 FROM table1
 UNION
 SELECT column_name(s)
 FROM table2;
 ```
 ```SQL
 SELECT City, Country FROM Customers
 WHERE Country = 'Germany'
 UNION
 SELECT City, Country FROM Suppliers
 WHERE Country = 'Germany'
 ORDER BY City;
 ```
 ### Practise
For the following examples I will refer to this [ER diagram](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/SQL_Lite_tutorial_ER_diagram.png)

How many albums does the artist Led Zeppelin
have? 
```SQL
SELECT ArtistId, name, (
    SELECT COUNT(*) 
    FROM albums
    WHERE albums.artistId = artists.artistId)
    AS number_of_albums
FROM artists
WHERE name = 'Led Zeppelin'
```
Create a list of album titles and the unit prices for the artist "Audioslave".
```SQL
SELECT artists.name,albums.title, tracks.name AS track_name, tracks.UnitPrice
FROM ((artists INNER JOIN albums
ON artists.ArtistId = albums.ArtistId)
INNER JOIN tracks 
ON albums.AlbumId = tracks.AlbumId)
WHERE artists.name = 'Audioslave'
```

Find the first and last name of any customer who
does not have an invoice. Are there any customers returned from the query? 
```SQL 
SELECT c.FirstName, c.LastName, i.invoiceId
FROM customers c INNER JOIN invoices i
ON c.customerId = i.customerId
WHERE i.invoiceID IS NULL
```
Find the total price for each album. What is the total price for the album “Big Ones”?
```SQL
SELECT t.name, t.UnitPrice, a.title, (
    SELECT  SUM(t.UnitPrice)
    FROM tracks t
    WHERE t.albumId = a.albumId) AS album_price
FROM tracks t INNER JOIN albums a
ON t.albumId = a.albumId
WHERE a.title = 'Big Ones'
```
In the following exercises please refer to this [ER](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/ChinookDatabaseSchema.png)

Find the names of all the tracks for the album "Californication".
```SQL
SELECT tracks.Name, albums.title
FROM tracks LEFT JOIN albums
ON tracks.albumId = albums.albumId
WHERE albums.title = 'Californication'
```
We can get the same data with subqueries
```SQL
SELECT Name
FROM tracks
WHERE albumid IN (
    SELECT albumid
    FROM albums
    WHERE title = 'Californication')
```
Find the total number of invoices for each customer along with the customer's full name, city and email.
```SQL
SELECT FirstName, LastName, city, email, (
    SELECT Count(InvoiceId)
    FROM Invoices
    WHERE Invoices.customerId = Customers.customerId
    ) AS Number_of_invoices
FROM Customers
--ORDER BY FirstName
```
Retrieve the track name, album, artistID, and trackID for all the albums.
What is the song title of trackID 12 from the "For Those About To Rock We Salute You" album?
```SQL
SELECT t.name, a.title, a.artistId, t.trackId
FROM tracks t LEFT JOIN albums a
ON t.albumId = a.albumId
WHERE t.trackId = 12 AND a.title = 'For Those About To Rock We Salute You'
```
Use a UNION to create a list of all the employee's and customer's first names and last names ordered by the last name in descending order.
```SQL
SELECT FirstName, LastName
FROM Employees
UNION
SELECT FirstName, LastName
FROM Customers
Order By LastName DESC
```


### Overview of Section 3
Some methods to check whether we got the right data
 - If you're doing a Cartesian join, check the number of
records in the first table and the second table and multiply them to make sure it's the intended outcome.  
 - Check the number of records each time you make a new join  
 - Start small
 - Take only data you need this will improve performance
 - Stop and think about what you are trying to do before you
start writing queries.
 - [Summary of different kind of Joins](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/SQL_Joins_Summary.png)
 - [Thinking in SQL vs Thinking in Python](https://mode.com/blog/learning-python-sql/) I really liked this link. *and it's not like anyone, truly, fully understands what on earth  GROUP BY really does*
 - [Difference Between Union and Union All - Optimal Performance Comparison](https://blog.sqlauthority.com/2009/03/11/sql-server-difference-between-union-vs-union-all-optimal-performance-comparison/)
 - Joins are usually faster, but subqueries can be more reliable

## Section 4: Modifying and Analyzing Data with SQL
### Working with Text Strings

Modifying Data is important to retrieve data in the format you need
 - String Functions:
    - Concatenate (linking together or adds together)
    - Substring: Returns the specified number of characters from particular position of given string. ```SUBSTR```
    - Trim: trims the leading or trailling space from a string. Functions: ```TRIM```, ```RTRIM```, ```LTRIM```(R - right, L - left side of string rsp.)
    - ```UPPER()```, ```LOWER()``` functions make all strings in the column in upper or lower case

Concatenations || (SQL server supports + instead ||)
```SQL
SELECT CompanyName, ContactName, CompanyName || '('|| ContactName ||')'
FROM customers
```
Trim
```SQL
SELECT TRIM ("    You the best.   ") AS TrimmedString;
```
Substring
```SQL
SUBSTR(string name, string position, 
number of characters to be returned)
```
```SQL
SELECT first_name,
SUBSTR(first_name, 3,4)
FROM employees
WHERE department_id=100;
```
```SQL
SELECT UPPER(LOWER)(column_name) FROM table_name;
```
### Working with Date and Time Strings
There is a lot of different formats for Date and time variables
If you query a ```DATETIME``` with:
```SQL WHERE PurchaseDate = '2016-12-12'```
You will get no results
SQLite supports 5 date and time functions:
```SQL
DATE(timestring, modifier, modifier, ...)
TIME(timestring, mod, mod, ...)
DATETIME(timestring, mod, mod, ...)
JULIANDAY(timestring, mod, mod, ...)
STRFTIME(format, timestring, mod, mod, ...)
```
timestrings:
```SQL
YYYY-MM-DD
YYYY-MM-DD HH:MM:SS
HH:MM
```
Modifiers:
NNN days, NNN hours, NNN years etc

### Date and Time String Examples
```SQL
SELECT Birthdate,
STRFTIME ('%Y', Birthdate) AS Year,
STRFTIME ('%m', Birthdate) AS Month,
STRFTIME ('%d', Birthdate) AS Day,
DATE(('now') - Birthdate) AS Age
From employees
```
Compute Current Date:
```SQL
SELECT DATE('now')
```
```SQL
SELECT STRFTIME('%Y %m %d','now')
```
### Case Statements
Case statement mimics if-else statement found in other programming languages. Can Be used in SELECT, INSERT, UPDATE, DELETE statements
```SQL
CASE
WHEN C1 THEN E1
WHEN C2 THEN E2
...
ELSE result else
END
```
```SQL
SELECT employeeid, city, CASE city
WHEN 'Calgary' Then 'Calgary'
ELSE 'Other' END calgary
FROM Employees
```
### Views
A View is a stored query. It can add or remove columns without changing shcema. They help to simplify the queries that you write. View is an illusion of a ```Table```.
```SQL
CREATE [TEMP] VIEW [IF NOT EXISTS]
view_name(column-name-list) AS select-statement;
```
```SQL
CREATE VIEW my_view
AS SELECT r.regiondesc, tterritorydesc
FROM Region r INNER JOIN Territories t ON r.regionid = t.refionid
```
To View data
```SQL
SELECT *
FROM my_view
```
To Drop view
```SQL 
DROP VIEW my_view;
```
### Data Governcance and Profiling
Data Profiling is looking at descriptive statistics or object data infromation - examining data for completeness and accuracy
i.e. Getting to know:
  - Number of rows
  - Table size
  - When the object was last updated
  - Column data type
  - Number of distinct values
  - Number of rows with NULL values
  - Descriptive statistics: max, average, standart deviation.

### Using SQL for Data Science, Part 1
Working through a Problem from Beginning to End:
  - Data understanding/Bussiness Understanding:
    - Null values
    - String values
    - Dates and times
    - Understanding where data joins are
    - Differianting integers from strings
    - Investing time to understand your subject will help later during data analysis
    - We want to predict whether or not a customer will buy our product
    - Which customers? What product? What is excluded? What is counted from the past?

### Using SQL for Data Science, Part 2
  - Profiling Data
    - Get into the details of your data
    - Create data model and map the fieds and tables you need (draw with pencil on paper!)
    - Consider Joins and calculations
    - Understand any data quality or format issues
  - Start with SELECT
    - Start simple i.e. take few collumns
    - Add in special formatting
    - Use subqueries
  - Test and Troubleshoot
    - Do not wait until the end to test queries
    - Test after each join or filter
    - Are you getting the results you excpect?
    - Start small and go step-by-step when troubleshooting a query
  - Format and Comment
    - Use correct formatting and indentation
    - Comment strategically
    - Clean code and comments help when you revisit or hand off code
  - Review
    - Review old queries
    - Business rules
    - Date changes
    - Date indicators
    - Work the problem for beginning to end
