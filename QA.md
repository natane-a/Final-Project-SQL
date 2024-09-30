What are your risk areas? Identify and describe them.
## Risk Areas

There were multiple risk areas presented within this dataset, especially the all_sessions table.
The time column is presented as an integer, some going into the millions, which led me to assume 
the values are stored in miliseconds, which would require conversion to answer any time related questions.
The country and city tables also have missing values, which would require 'WHERE' statements to exclude those
rows where country/city are significant.
The columns labelled total_transaction_revenue, transactions, product_quantity, product_revenue, item_quantity,
item_revnue, and transaction_revenue are also all predominately empty, meaning to find answers to questions 
pertaining to price would require joing all_sessions to another table, as the product_price column is not 
significant without product_quantity.

The analytics table can be joined to the all_sessions table using the full_visitor_id column, which is notable,
and also contains a unit_price column along with unit_quantity, which can be used together to calculate transaction
revenue. There are a lot of duplicate records in this table as well, so when using this table, I need to be sure
to use the DISTINCT clause.

The products table is the other table I used, and the only issue with that table is a single product having
a null value in the columns labelled sentiment_score and sentiment_magnitude.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

>`` SQL
SELECT DISTINCT(full_visitor_id), unit_price FROM analytics WHERE units_sold IS NOT NULL
>``
This query is to see how many unique transactions there are within the analytics dataset.
>`` SQL
SELECT SUM(units_sold) FROM analytics
>``
This query is to the see the total amount of units sold and compare it to sales report.
>`` SQL
SELECT SUM(total_ordered) FROM sales_report
>``
This query is to used to compare total_ordered in sales report, compared to units_sold.
>`` SQL
SELECT DISTINCT(full_visitor_id) FROM analytics
>``
This query is to see the amount of UNIQUE visitor ids in the analytic table
>`` SQL
SELECT DISTINCT(full_visitor_id) FROM analytics WHERE units_sold IS NOT NULL
>``
This query is to see unique ids that had orders placed.
>`` SQL
SELECT * FROM products WHERE sentiment_score IS NULL
>``
This query is to show all products that have no sentiment recorded.
>`` SQL
SELECT DISTINCT(product_sku) FROM products
>``
This query is to see all unique products.
