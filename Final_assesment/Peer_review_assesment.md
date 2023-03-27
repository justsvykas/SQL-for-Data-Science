# Introduction
Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

We will be using Yelp dataset which ER diagram you can see below
![dataset](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_dataset_ER.png)



# Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table = 10000
```SQL
SELECT *
FROM attribute
```
ii. Business table = 10000
```SQL
SELECT *
FROM business
```
iii. Category table = 10000
```SQL
SELECT *
FROM category
```
iv. Checkin table = 10000
```SQL
SELECT *
FROM category
```
v. elite_years table = 10000
```SQL
SELECT *
FROM elite_years
```
vi. friend table = 10000
```SQL
SELECT *
FROM friend
```
vii. hours table = 10000
```SQL
SELECT *
FROM hours
```
viii. photo table = 10000
```SQL
SELECT *
FROM photo
```
ix. review table = 10000
```SQL
SELECT *
FROM review
```
x. tip table = 10000
```SQL
SELECT *
FROM tip
```
xi. user table = 10000
```SQL
SELECT *
FROM user
```
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10000
```SQL
SELECT Distinct id
FROM business
```
ii. Hours = 1562
```SQL
SELECT Distinct business_id
FROM hours
```
iii. Category = 2643
```SQL
SELECT Distinct business_id
FROM category
```
iv. Attribute = 1115
```SQL
SELECT Distinct business_id
FROM attribute
```
v. Review = 9581 with respect to user_id
This means there are 9581 distinct users who has written at least 1 review. I avoided using primary key ```id```, because we already know the information from exercise 1 (primary key can't have the same value)
```SQL
SELECT Distinct user_id
FROM review
```
vi. Checkin = 493
```SQL
SELECT Distinct business_id
FROM checkin
```
vii. Photo = 6493 w.r.t. business_id (Similar argument as in 2)v.)
```SQL
SELECT Distinct business_id
FROM checkin
```
viii. Tip = 537 w.r.t. user_id
```SQL
SELECT Distinct user_id
FROM tip
```
ix. User = 10000
```SQL
SELECT Distinct id
FROM user
```
x. Friend = 11
```SQL
SELECT count(Distinct user_id)
FROM friend
```
xi. Elite_years = 2780
```SQL
SELECT distinct user_id
FROM elite_years
```


Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: NO
	
	
	SQL code used to arrive at answer:
```SQL
SELECT *
FROM user
WHERE id is null or name is null or review_count is null
or yelping_since is null or useful is null
or funny is null or cool is null or fans is null or average_stars is null
or compliment_hot is null or compliment_more is null
or compliment_profile is null or compliment_cute is null
or compliment_list is null or compliment_note is null
or compliment_plain is null or compliment_cool is null
or compliment_funny is null or compliment_writer is null
or compliment_photos is null
```
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082
	
	```sql
	SELECT min(stars), max(stars), avg(stars)
	FROM review
	```
	Code is similar to following exercises
	
	ii. Table: Business, Column: Stars 
	
		min: 1		max: 5   	avg:  3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min: 0		max: 2		avg: 0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg: 1.9414
		
	
	v. Table: User, Column: Review_count
	
		min: 0		max: 2000		avg: 24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	```SQL
	SELECT city, sum(review_count) As review_count
	FROM business
	Group by city
	ORDER BY review_count DESC
	```
	Output:
	![ex5](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex5.png)
	 
	

	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
```SQL
SELECT stars, Count(*) as number_of_stars
FROM business
WHERE city = 'Avon'
Group BY stars
```
Output:
![ex6i](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex6i_up.png)


ii. Beachwood

SQL code used to arrive at answer:
```SQL
SELECT stars, COunt(*) as number_of_stars
FROM business
WHERE city = 'Beachwood'
Group BY stars
```
Output:
![ex6ii](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex6ii_up.png)


7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	
		
	Copy and Paste the Result Below:
		


8. Does posing more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:
	

	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:

	
	SQL code used to arrive at answer:

	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	
	
	Copy and Paste the Result Below:

	
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?


ii. Do the two groups you chose to analyze have a different number of reviews?
         
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

SQL code used for analysis:

		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
         
         
ii. Difference 2:
         
         
         
SQL code used for analysis:

	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
                           
                  
iii. Output of your finished dataset:
         
         
iv. Provide the SQL code you used to create your final dataset:
