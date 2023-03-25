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

### SQL for Data Science Languages
Some supplementary recources I liked
 - [Python-SQL Package Documentation](https://pypi.org/project/python-sql/)
 

