What issues will you address by cleaning the data?

I will address issues such as:
Null values 
Duplicate Records
Reducing values

Queries:
Below, provide the SQL queries you used to clean your data.

Example:
>```sql
SELECT al.country AS country, 
		SUM((a.unit_price / 1000000)* a.units_sold) AS transaction_revenue
FROM all_sessions al
JOIN analytics a ON al.full_visitor_id = a.full_visitor_id
WHERE ((a.unit_price / 1000000)* a.units_sold) IS NOT NULL 
GROUP BY al.country
ORDER BY transaction_revenue DESC
>```

>`` SQL
WITH distinct_visitor_id AS (
	SELECT DISTINCT(al.full_visitor_id) AS full_visitor_id, al.city, a.units_sold AS units_sold
	FROM all_sessions al
	JOIN analytics a ON al.full_visitor_id = a.full_visitor_id
	WHERE a.units_sold IS NOT NULL AND city != 'not available in demo dataset'
)
SELECT city, AVG(units_sold) AS average_units_sold
FROM distinct_visitor_id
GROUP BY city
ORDER BY average_units_sold DESC;
>``

>`` SQL
WITH top_categories AS(
	SELECT 	country,
			city,
			v2_product_category AS product_category,
			COUNT(*) AS category_count,
			RANK() OVER (PARTITION BY city, country
			ORDER BY COUNT(*) DESC) AS rank
	FROM all_sessions
	WHERE v2_product_category != '(not set)' AND city != 'not available in demo dataset' 
	GROUP BY city, country, product_category
)
SELECT city, country, product_category, category_count
FROM top_categories
WHERE rank <=5 
ORDER BY category_count DESC, rank
>``

