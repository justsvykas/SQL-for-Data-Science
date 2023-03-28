
# Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

## Introduction 

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

We will be using Yelp dataset which ER diagram you can see below
![dataset](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_dataset_ER.png)



## Part 1: Yelp Dataset Profiling and Understanding

### 1. Profile the data by finding the total number of records for each of the tables below:
	
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
	


### 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

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
v. Review = 9581 with respect to user_id.\
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



### 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

Answer: NO
	
	
SQL code used to arrive at answer:
```SQL
SELECT *
FROM user
WHERE id is null or name is null or review_count is null
or yelping_since is null or useful is null
or funny is null or cool is null
or fans is null or average_stars is null
or compliment_hot is null or compliment_more is null
or compliment_profile is null or compliment_cute is null
or compliment_list is null or compliment_note is null
or compliment_plain is null or compliment_cool is null
or compliment_funny is null or compliment_writer is null
or compliment_photos is null
```
	

	
### 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

- i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082

	SQL code used to arrive at the solution
	```sql
	SELECT min(stars), max(stars), avg(stars)
	FROM review
	```
	Code is similar to following exercises
	
- ii. Table: Business, Column: Stars 
	
		min: 1		max: 5   	avg:  3.6549
		
	
- iii. Table: Tip, Column: Likes
	
		min: 0		max: 2		avg: 0.0144
		
	
- iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg: 1.9414
		
 - v. Table: User, Column: Review_count
	
		min: 0		max: 2000		avg: 24.2995
		


### 5. List the cities with the most reviews in descending order:

SQL code used to arrive at answer:
```SQL
SELECT city, sum(review_count) As review_count
FROM business
Group by city
ORDER BY review_count DESC
```
Output:

![ex5](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex5.png)
	 
	

	
### 6. Find the distribution of star ratings to the business in the following cities:

- i. Avon

	SQL code used to arrive at answer:
	```SQL
	SELECT stars, Count(*) as number_of_stars
	FROM business
	WHERE city = 'Avon'
	Group BY stars
	```
	Output:

	![ex6i](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex6i_up.png)


- ii. Beachwood

	SQL code used to arrive at answer:
	```SQL
	SELECT stars, COunt(*) as number_of_stars
	FROM business
	WHERE city = 'Beachwood'
	Group BY stars
	```
	Output:

	![ex6ii](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex6ii_up.png)


### 7. Find the top 3 users based on their total number of reviews:
		
SQL code used to arrive at answer:
```SQL
SELECT id, name, review_count
FROM user
ORDER BY review_count DESC
LIMIT 3
```
	
Output:

![ex7](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex7.png)
		


### 8. Does posing more reviews correlate with more fans?

Please explain your findings and interpretation of the results:

From calculations below we can easily notice that in general more reviews attracts more fans 

```SQL
SELECT COUNT(id) as number_of_users, 
avg(review_count) as avg_review_count,

-- I classify fans into boxes so we could investigate
-- the relationship between number of reviews and number of fans
-- i.e. (11,15) means user has between 11 and 15 fans

CASE WHEN fans BETWEEN 0 and 2 THEN '(0,2)'
WHEN fans BETWEEN 3 and 5 THEN '(3,5)'
WHEN fans BETWEEN 6 and 10 THEN '(6,10)'
WHEN fans BETWEEN 11 and 15 THEN '(11,15)'
WHEN fans BETWEEN 16 and 20 THEN '(16,20)'
WHEN fans BETWEEN 21 and 30 THEN '(21,30)'
WHEN fans BETWEEN 31 and 40 THEN '(31,40)'
WHEN fans BETWEEN 41 and 50 THEN '(41,50)'
WHEN fans BETWEEN 50 and 99 THEN '(50,99)'
WHEN fans BETWEEN 100 and 149 THEN '(100,149)'
WHEN fans BETWEEN 150 and 199 THEN '(150,199)'
WHEN fans BETWEEN 200 and 249 THEN '(200,249)'
WHEN fans BETWEEN 250 and 299 THEN '(250,299)'
WHEN fans BETWEEN 300 and 349 THEN '(350,349)'
WHEN fans BETWEEN 350 and 399 THEN '(350,399)'
ELSE '>= 400' END nr_of_fans

FROM user
GROUP BY nr_of_fans
ORDER BY avg_review_count
```
Output:

![ex8](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex8_up.png)

	
### 9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: There are more reviews with the word love

	
	SQL code used to arrive at answer:

```SQL
SELECT 
sum(CASE WHEN text LIKE '%love%' THEN 1
ELSE 0 END) as love_nr,
sum(CASE WHEN text LIKE '%hate%' THEN 1
ELSE 0 END) as hate_nr
FROM review
```
Output:

![ex9](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex9.png)
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:

```SQL
SELECT name, fans
FROM user
ORDER BY fans DESC
LIMIT 10
```
	Copy and Paste the Result Below:

![ex10](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex10.png)	
	

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

From doing a little bit of analysis I found out the top 5 cities in which there are most businesses. I picked Phoenix just because it sounds cool.

![ex1.2](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex1_2.png)
	
I picked restaurant category since Phoenix has most businesses in this area. There is 4 distinct restaurants with ratings 2-3 stars (McDonald's and Gallagher's) and 4-5 stars (Charlie D's and Bootleggers)

i. Do the two groups you chose to analyze have a different distribution of hours?

4-5 star restaurants start working at same time 11:00 where Bootleggers finish at 22:00 and Charlie's finish at 18:00
2-3 star restaurants start working a lot earlier comparitively and ends work a lot later.
The difference in rating between these groups definetly doesn't correlate with having more working hours higher accessability. I would hypothise the difference in rating must lie in the quality of food provided by restaurants.

ii. Do the two groups you chose to analyze have a different number of reviews?

4-5 star restaurants together has 438 reviews while 2-3 star ones has only 68. 
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

Neighborhood of these restaurants in mind is not provided,
While postal code and addresses differ from each restaurant. Thus I cant conclude anything from the data given.

SQL code used for analysis:
```SQL
SELECT
--b.city, 
b.name AS name_of_bussines, 
--c.category,

CASE WHEN b.stars BETWEEN 2 AND 3 THEN '2-3 stars'
WHEN b.stars BETWEEN 4 AND 5 THEN '4-5 stars'
ELSE 'other' END stars_category,

h.hours,
b.review_count,
b.address,
b.neighborhood,
b.postal_code

FROM (business b INNER JOIN category c 
ON b.id = c.business_id)

INNER JOIN hours h
ON b.id = h.business_id

WHERE b.city = 'Phoenix'
AND (stars_category = '2-3 stars' 
OR stars_category = '4-5 stars')
AND category = 'Restaurants'

ORDER BY name_of_bussines 
```

Output:
![ex2_1ii](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_2_1iii.png)

		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.

i. Difference 1:

Average number of reviews for closed businesses is around 23 which is significantly lower number than that of open businesses which is 32.
While also the average star rating is in favor for open businesses.
         
         
ii. Difference 2:

The number of businesses that are open is higher than number of closed ones.
         
```SQL         
SELECT is_open, COUNT(name) AS num_of_business,
AVG(review_count) AS average_review_num,
AVG(stars) AS average_star_num
FROM business
GROUP BY is_open
```

![ex2_2]()
	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:

Predicting the number of fans a user will have.
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

The most important data that I will need is review_count from user table. From the data we have analyzed, we can notice that number of reviews and number of fans follow a nice linear graph. This allows me to approximate number of fans.

Ofcourse, we can also look at how many useful, funny and cool the user has recieved. This can allows us to doublecheck our prognozis for fan number. Although the graph relating to number of fans and useful/funny/cool look a lot more skewed than that ofr number of reviews. Thus, giving less weight to these attributes would be best.
                           
                  
iii. Output of your finished dataset:

![ex2_3](https://github.com/justsvykas/SQL-for-Data-Science/blob/main/Final_assesment/Yelp_ex_2_3.png)
         
iv. Provide the SQL code you used to create your final dataset:

```SQL
SELECT 
CASE WHEN fans BETWEEN 0 and 2 THEN '(0,2)'
WHEN fans BETWEEN 3 and 5 THEN '(3,5)'
WHEN fans BETWEEN 6 and 10 THEN '(6,10)'
WHEN fans BETWEEN 11 and 15 THEN '(11,15)'
WHEN fans BETWEEN 16 and 20 THEN '(16,20)'
WHEN fans BETWEEN 21 and 25 THEN '(21,25)'
WHEN fans BETWEEN 25 and 30 THEN '(25,30)'
WHEN fans BETWEEN 31 and 40 THEN '(31,40)'
WHEN fans BETWEEN 41 and 50 THEN '(41,50)'
WHEN fans BETWEEN 51 and 65 THEN '(50,65)'
WHEN fans BETWEEN 66 and 99 THEN '(66,99)'
WHEN fans BETWEEN 100 and 149 THEN '(100,149)'
WHEN fans BETWEEN 150 and 199 THEN '(150,199)'
ELSE '>= 200' END nr_of_fans,

COUNT(id) as number_of_users, 
avg(review_count) as avg_review_count,
avg(useful),
avg(funny),
avg(cool)

FROM user
GROUP BY nr_of_fans
ORDER BY number_of_users DESC
```