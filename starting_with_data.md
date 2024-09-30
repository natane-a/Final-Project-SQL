Question 1: 
Which countries feel the most intensely about the products they purchased?

SQL Queries:
>`` SQL
SELECT al.country AS country, AVG(p.sentiment_magnitude) AS average_sentiment_magnitude
FROM all_sessions al JOIN products p ON al.product_sku = p.product_sku 
GROUP BY country
ORDER BY average_sentiment_magnitude DESC
LIMIT 5
>``
Answer: 
The countries that feel most passionate about their products are Barbados, Kosovo, Kyrgzstan, and Jersey and Sint Maarten.


Question 2: 
Which countries/cities have the lowest average sentiment score?

SQL Queries:
>`` SQL
SELECT al.country AS country, AVG(p.sentiment_score) AS average_sentiment_score
FROM all_sessions al JOIN products p ON al.product_sku = p.product_sku 
GROUP BY country
ORDER BY average_sentiment_score 
LIMIT 5
>``

Answer:
Gibraltar, Maldives, Jamaica, Maurius, Brunei. 


Question 3: 
Which countries/cities have the highest average sentiment score?

SQL Queries:
>`` SQL
SELECT al.country AS country, al.city AS city, AVG(p.sentiment_score) AS average_sentiment_score
FROM all_sessions al JOIN products p ON al.product_sku = p.product_sku 
WHERE city != '(not set)' AND city != 'not available in demo dataset'
GROUP BY country, city
ORDER BY average_sentiment_score DESC
LIMIT 5
>``
Answer:
The cities with the highest average sentiment score are Stuttgart, Kharkiv, Westlake Village, Greer, Los Angeles.
The countries with the highest average sentiment score are Sint Maarten, Jordan, Luxembourg, Zimbabwe and Haiti.


Question 4: 
What products have the highest sentiment scores?

SQL Queries:
>`` SQL
SELECT al.v2_product_name AS product_name, AVG(p.sentiment_score) AS average_sentiment_score
FROM all_sessions al JOIN products p ON al.product_sku = p.product_sku 
GROUP BY product_name
ORDER BY average_sentiment_score DESC
LIMIT 5
>``
Answer:
Youtube Men's Vintage Tee, Google Hard Cover Journal, Google Men's Bayside Graphic Tee, Google Pocket Bluetooth Speaker,
Google Youth Short Sleeve Tee Red.

Question 5: 
Is there a correlation between product price and sentiment score?

SQL Queries:
>`` SQL
SELECT 	al.v2_product_name AS product_name, (a.unit_price/1000000) AS product_cost, 
		AVG(sr.sentiment_score) AS average_sentiment_score
FROM analytics a
JOIN all_sessions al ON a.full_visitor_id = al.full_visitor_id
JOIN sales_report sr ON al.product_sku = sr.product_sku
GROUP BY product_name, product_cost
ORDER BY product_cost DESC
>``
Answer:
No correlation 