# Retail-Sales-Analysis

This project involves the design and execution of an advanced SQL-based system to analyze retail sales data. The goal is to gain valuable insights into sales performance, customer behavior, product trends, and operational efficiency, which can help drive strategic business decisions.


#### OBJECTIVES 

- **Sales Trend Analysis:** Analyze the total sales over time (daily, monthly, yearly) to identify patterns, seasonal trends, and any fluctuations in sales volume.
- **Customer Segmentation:** Use SQL to segment customers based on their purchasing behavior, such as total spending, frequency of purchases, and preferred product categories.
- **Category and Product Performance Evaluation:** Evaluate the sales performance of different product categories and identify top-performing products based on total revenue and number of transaction.
- **High-Value Transaction Identification:** Identify transactions where the total sale exceeds a certain threshold and analyze these high-value transactions to understand their contribution to overall sales.
- **Time-Based Sales Analysis:** Classify sales transactions into different shifts (morning, afternoon, evening) and analyze how sales vary across different times of the day.
- **Business Analysis:** Use SQL queries to answer specific business questions, such as identifying top customers, most popular categories, and factors influencing sales performance.

##
#### PROJECT STRUCTURE:

##### 1.DATABASE SETUP

- **Database Creation:** The project begins by setting up a database named `retail_db` to store all sales-related data.
- **Table Creation:** A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE  DATABASE  retail_db;
CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

##### 2.DATA RETRIEVAL QUERIES 

- **Counting the total number of transactions in retail_sales:**
```Sql
SELECT COUNT(*) FROM retail_sales;
```

- **Counting the number of distinct customers in retail_sales:**
```Sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
```

##### 3.FILTERED DATA QUERIES 

- **Total Sales Trend Over Time for a Specific Date Range**
  
Query : Retrieve the total sales trend for a specific date range (the year 2022), broken down by month.

```Sql
SELECT DATE_FORMAT(sale_date, '%Y-%m') AS month,  
       SUM(total_sale) AS total_sales  
FROM retail_sales  
WHERE sale_date BETWEEN '2022-01-01' AND '2022-12-31'  -- filter for the year 2022
GROUP BY month  
ORDER BY month;
```

- **Calculate total sales and orders by category:**
  
Query: Retrieves the sum of sales and the total number of orders for each category

```Sql
SELECT category,  
       SUM(total_sale) as net_sale,  
       COUNT(*) as total_orders  
FROM retail_sales  
GROUP BY category;
```

- **Find the average age of customers who purchased items from the 'Beauty' category:**
  
Query: Retrieves the sum of sales and the total number of orders for the 'Beauty' category

```Sql
SELECT ROUND(AVG(age), 2) as avg_age  
FROM retail_sales  
WHERE category = 'Beauty';
```

- **Find all transactions where the total sale is greater than 1000:**
  
Query: Retrieves all the transactions where the total sale amount exceeds 1000.

```Sql
SELECT *  
FROM retail_sales  
WHERE total_sale > 1000;
```

##### 4.AGGREGATED DATA QUERIES 

- **Count transactions by gender and category:**
  
Query: Retrieves a count of the total transactions for each gender within each product category.

```Sql
SELECT category,  
       gender,  
       COUNT(*) as total_trans  
FROM retail_sales  
GROUP BY category, gender  
ORDER BY category;
```

- **Top 5 customers based on highest total sales:**
  
Query: Retrieve the five customers who have made the highest total purchases.

```Sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```

- **Determine the number of unique customers who made purchases in each category:**
  
Query: Retrieves the number of unique customers who have made purchases in each product category.

```Sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) AS cnt_unique_cs
FROM retail_sales
GROUP BY category;
```

##### 5.TIME-BASED DATA QUERIES 

- **Classifying sales transactions into shifts and calculating total orders for each shift:**
  
Query: Classify each transaction into a specific shift based on the sale time and return the total number of orders for each shift.

```Sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift;
```

 
- **Identify the category with the highest number of total purchases:**
  
Query: Retrieves the category with the highest number of total purchases.

```Sql
SELECT 
    category, 
    COUNT(*) AS total_purchases
FROM retail_sales
GROUP BY category
ORDER BY total_purchases DESC
LIMIT 1;
```

- **Calculate the total revenue generated by each category:**
  
Query: Retrieves the total revenue generated by each product category.

```Sql
SELECT 
    category, 
    SUM(total_sale) AS total_revenue
FROM retail_sales
GROUP BY category;
```


6.	DATA SEGREGATION 



