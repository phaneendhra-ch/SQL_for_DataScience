"""

Title : SQL for Data Science

Description: This is a part of Coursera's (SQL for Data Science) Peer Graded Assignment.

Author : Phaneendhra

Date : 12 Oct 2020

"""



Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:

i. Attribute table = 10000  select count(*)from attribute;
ii. Business table = 10000  select count(*)from business;
iii. Category table = 10000 select count(*)from category;
iv. Checkin table = 10000 select count(*) from checkin;
v. elite_years table = 10000 select count(*) from elite_years;
vi. friend table = 10000 select count(*) from friend;
vii. hours table = 10000 select count(*) from hours;
viii. photo table = 10000 select count(*) from photo;
ix. review table = 10000 select count(*) from review;
x. tip table = 10000 select count(*) from tip;
xi. user table = 10000 select count(*) from user;



2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10000 select count(distinct id) from business;
ii. Hours = 1562  select count(distinct business_id) from hours;
iii. Category =  2643 select count(distinct business_id) from category;
iv. Attribute = 1115 select count(distinct business_id) from attribute;
v. Review = 10000,8090,9581 select count(distinct id), count(distinct business_id), count(distinct user_id) from review;
vi. Checkin = 493 select count(distinct business_id) from checkin;
vii. Photo = 10000,6493 select count(distinct id), count(distinct business_id) from photo;
viii. Tip = 3979,537 select count(distinct business_id), count(distinct user_id) from tip;
ix. User = 10000 select count(distinct id) from user;
x. Friend = 11 select count(distinct user_id) from friend;
xi. Elite_years = 2780 select count(distinct user_id) from elite_years;

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer:


	SQL code used to arrive at answer:

	SELECT count(*) - count(id),
     	count(*) - count(name),
   	count(*) - count(review_count),
   	count(*) - count(yelping_since),
   	count(*) - count(useful),
   	count(*) - count(cool),
   	count(*) - count(fans),
   	count(*) - count(average_stars),
   	count(*) - count(compliment_hot),
   	count(*) - count(compliment_more),
   	count(*) - count(compliment_profile),
   	count(*) - count(compliment_cute),
   	count(*) - count(compliment_list),
   	count(*) - count(compliment_note),
   	count(*) - count(compliment_plain),
   	count(*) - count(compliment_cool),
   	count(*) - count(compliment_funny),
   	count(*) - count(compliment_writer),
   	count(*) - count(compliment_photos)
	from user;




4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars

		min:1		max:5		avg:3.7082
		select min(stars), max(stars), avg(stars) from review;


	ii. Table: Business, Column: Stars

		min:1		max:5		avg:3.6549
		select min(stars), max(stars), avg(stars) from business;


	iii. Table: Tip, Column: Likes

		min:0		max:2		avg:0.0144
		select min(likes), max(likes), avg(likes) from tip;

	iv. Table: Checkin, Column: Count

		min:1		max:53		avg:1.9414
		select min(count), max(count), avg(count) from checkin;


	v. Table: User, Column: Review_count

		min:0		max:2000	avg:24.2995
		select min(review_count), max(review_count), avg(review_count) from user;


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	select sum(review_count) as total_reviews, city
	from business
	group by city
	order by total_reviews desc;

	Copy and Paste the Result Below:
	+---------------+-----------------+
	| total_reviews | city            |
	+---------------+-----------------+
	|         82854 | Las Vegas       |
	|         34503 | Phoenix         |
	|         24113 | Toronto         |
	|         20614 | Scottsdale      |
	|         12523 | Charlotte       |
	|         10871 | Henderson       |
	|         10504 | Tempe           |
	|          9798 | Pittsburgh      |
	|          9448 | MontrÃ©al        |
	|          8112 | Chandler        |
	|          6875 | Mesa            |
	|          6380 | Gilbert         |
	|          5593 | Cleveland       |
	|          5265 | Madison         |
	|          4406 | Glendale        |
	|          3814 | Mississauga     |
	|          2792 | Edinburgh       |
	|          2624 | Peoria          |
	|          2438 | North Las Vegas |
	|          2352 | Markham         |
	|          2029 | Champaign       |
	|          1849 | Stuttgart       |
	|          1520 | Surprise        |
	|          1465 | Lakewood        |
	|          1155 | Goodyear        |
	+---------------+-----------------+
	(Output limit exceeded, 25 of 362 total rows shown)



6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
select stars as star_rating, count(stars) as count
from business
where city='Avon'
group by stars;


Copy and Paste the Resulting Table Below (2 columns Ã¢â‚¬â€œ star rating and count):
+-------------+-------+
| star_rating | count |
+-------------+-------+
|         1.5 |     1 |
|         2.5 |     2 |
|         3.5 |     3 |
|         4.0 |     2 |
|         4.5 |     1 |
|         5.0 |     1 |
+-------------+-------+

ii. Beachwood

SQL code used to arrive at answer:
select stars as star_rating, count(stars) as count
from business
where city='Beachwood'
group by stars;

Copy and Paste the Resulting Table Below (2 columns Ã¢â‚¬â€œ star rating and count):
+-------------+-------+
| star_rating | count |
+-------------+-------+
|         2.0 |     1 |
|         2.5 |     1 |
|         3.0 |     2 |
|         3.5 |     2 |
|         4.0 |     1 |
|         4.5 |     2 |
|         5.0 |     5 |
+-------------+-------+


7. Find the top 3 users based on their total number of reviews:

	SQL code used to arrive at answer:
	select name, sum(review_count) as total_count
	from user
	group by id
	order by total_count desc
	limit 3;

	Copy and Paste the Result Below:
	+--------+-------------+
	| name   | total_count |
	+--------+-------------+
	| Gerald |        2000 |
	| Sara   |        1629 |
	| Yuri   |        1339 |
	+--------+-------------+


8. Does posing more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:

Yes the correlation factor impacts huge relation b/w reviews and fans.
Clearly we can related the mathematical standards of correlation coefficicent for instance,
"Gerald has a postive correlation, as the increase in reviews results  more number of fans", whereas,
"Eric has a negative correlation, as the increase in reviews results less number of fans".


	select name,review_count,fans
        from user
        order by review_count desc;

	+-----------+--------------+------+
	| name      | review_count | fans |
	+-----------+--------------+------+
	| Gerald    |         2000 |  253 |
	| Sara      |         1629 |   50 |
	| Yuri      |         1339 |   76 |
	| .Hon      |         1246 |  101 |
	| William   |         1215 |  126 |
	| Harald    |         1153 |  311 |
	| eric      |         1116 |   16 |
	| Roanna    |         1039 |  104 |
	| Mimi      |          968 |  497 |
	| Christine |          930 |  173 |
	| Ed        |          904 |   38 |
	| Nicole    |          864 |   43 |
	| Fran      |          862 |  124 |
	| Mark      |          861 |  115 |
	| Christina |          842 |   85 |
	| Dominic   |          836 |   37 |
	| Lissa     |          834 |  120 |
	| Lisa      |          813 |  159 |
	| Alison    |          775 |   61 |
	| Sui       |          754 |   78 |
	| Tim       |          702 |   35 |
	| L         |          696 |   10 |
	| Angela    |          694 |  101 |
	| Crissy    |          676 |   25 |
	| Lyn       |          675 |   45 |
	+-----------+--------------+------+
	(Output limit exceeded, 25 of 10000 total rows shown)



9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:


	SQL code used to arrive at answer:



10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer: LOVE

        select count(*)
	from review
	where text like '%love%';

        select count(*)
	from review
	where text like '%hate%'


	Copy and Paste the Result Below:

	+----------+
	| count(*) |  (LOVE)
	+----------+
	|     1780 |
	+----------+

	+----------+
	| count(*) | (HATE)
	+----------+
	|      232 |
	+----------+



Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

i. Do the two groups you chose to analyze have a different distribution of hours?

	As there is a single review available, there's nothing much different found in distribution of hours

ii. Do the two groups you chose to analyze have a different number of reviews?

	There's only single group of review available ! Reviews has not put much impact on these specific review of the group

iii. Are you able to infer anything from the location data provided between these two groups? Explain.

	Yes for the rating ranging between 4 and 5, we can spot an address/location
SQL code used for analysis:

		i)	SELECT CASE WHEN stars >= 4.0 THEN '4-5 stars'
            		WHEN stars >= 2.0 THEN '2-3 stars'
            		ELSE 'below 2' END AS 'STARS',
       			COUNT(DISTINCT business.id) AS 'Total Id',
       			COUNT(hours) AS 'Total days Open',   -- number of openning days
       			COUNT(hours)*1.0 / COUNT(DISTINCT business.id)  AS 'Avgerge open days'
			FROM ((business INNER JOIN hours ON business.id = hours.business_id)
     				INNER JOIN category ON business.id = category.business_id)
			WHERE city = 'Cleveland' AND category.category ='Fruits & Veggies'
			GROUP BY STARS;

			+-----------+----------+-----------------+-------------------+
			| STARS     | Total Id | Total days Open | Avgerge open days |
			+-----------+----------+-----------------+-------------------+
			| 4-5 stars |        1 |               5 |               5.0 |
			+-----------+----------+-----------------+-------------------+

		ii)	SELECT CASE WHEN stars >= 4.0 THEN '4-5 stars'
            		WHEN stars >= 2.0 THEN '2-3 stars'
            		ELSE 'below 2' END AS 'STARS',
       			COUNT(DISTINCT business.id) AS id_count,
       			SUM(review_count) AS "Total Review",
       			SUM(review_count)*1.0/COUNT(DISTINCT business.id)  AS "Average Review Count"
      			FROM business INNER JOIN category ON business.id = category.business_id
      			WHERE city = 'Cleveland' AND category.category ='Fruits & Veggies'
      			GROUP BY STARS;

			+-----------+----------+--------------+----------------------+
			| STARS     | id_count | Total Review | Average Review Count |
			+-----------+----------+--------------+----------------------+
			| 4-5 stars |        1 |          723 |                723.0 |
			+-----------+----------+--------------+----------------------+


		iii)	SELECT CASE WHEN stars >= 4.0 THEN '4-5 stars'
            		WHEN stars >= 2.0 THEN '2-3 stars'
            		ELSE 'below 2' END AS 'STARS',
            		business.neighborhood,
            		business.address,
            		business.postal_code
      			FROM business INNER JOIN category ON business.id = category.business_id
     		 	WHERE city = 'Cleveland' AND category.category ='Fruits & Veggies'
      			GROUP BY STARS;

			+-----------+--------------+----------------+-------------+
			| STARS     | neighborhood | address        | postal_code |
			+-----------+--------------+----------------+-------------+
			| 4-5 stars | Ohio City    | 1979 W 25th St | 44113       |
			+-----------+--------------+----------------+-------------+



2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.

i. Difference 1:

	The average stars for stars under open are higher than the closed ones.

ii. Difference 2:

	Though the  difference between review_count of open and closed is huge but still came close in Average Rating of the stars.


SQL code used for analysis:

	SELECT COUNT(DISTINCT(id)),AVG(review_count),SUM(review_count),AVG(stars),is_open
	FROM business
	GROUP BY is_open

	+---------------------+-------------------+-------------------+---------------+---------+
	| COUNT(DISTINCT(id)) | AVG(review_count) | SUM(review_count) |    AVG(stars) | is_open |
	+---------------------+-------------------+-------------------+---------------+---------+
	|                1520 |     23.1980263158 |             35261 | 3.52039473684 |       0 |
	|                8480 |     31.7570754717 |            269300 | 3.67900943396 |       1 |
	+---------------------+-------------------+-------------------+---------------+---------+

3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:

i. Indicate the type of analysis you chose to do:

				 I've chosen an analysis city which has more occurrence among rating-wise and on a specific Category.

ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

				The main criteria behind the selection of below data is to locate a city which has a better rating irrespective of the category or in
				few cases we might consider the category depending upon individual interest.

				If a person want to start a business in the cities which has more ratings or the occurrence, he can get an overview of the cities which compete more
				and can enter into the booming business.

iii. Output of your finished dataset:

					+-----------------+------------+--------------+-------+
					| City Occurrence | City       | category     | stars |
					+-----------------+------------+--------------+-------+
					|              23 | Cleveland  | Restaurants  |     5 |
					|              14 | Las Vegas  | Asian Fusion |     5 |
					|              25 | Phoenix    | Barbeque     |     5 |
					|               2 | Pittsburgh | Food         |     5 |
					|               3 | Aurora     | Restaurants  |     4 |
					|               3 | Toronto    | Parks        |     4 |
					+-----------------+------------+--------------+-------+

iv. Provide the SQL code you used to create your final dataset:

					select count(city) as "City Occurrence",city as "City",category.category,review.stars
					from business inner join review on business.id = review.business_id
 				  	inner join category on business.id=category.business_id
 					where review.stars>3
 					group by city
					order by review.stars desc;