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

**DATABASE SETUP**

•	Database Creation: The project begins by setting up a database named `retail_db` to store all sales-related data.
•	Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

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

