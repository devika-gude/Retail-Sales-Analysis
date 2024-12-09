# Retail-Sales-Analysis

This project involves the design and execution of an advanced SQL-based system for querying and data manipulation, followed by Tableau for impactful data visualization. The goal is to gain valuable insights into sales performance, customer behavior, product trends, and operational efficiency, which can help drive strategic business decisions.


#### OBJECTIVES 

- **Sales Trend Analysis:** Analyze the total sales over time (daily, monthly, yearly) to identify patterns, seasonal trends, and any fluctuations in sales volume.
- **Customer Segmentation:** Use SQL to segment customers based on their purchasing behavior, such as total spending, frequency of purchases, and preferred product categories.
- **Category and Product Performance Evaluation:** Evaluate the sales performance of different product categories and identify top-performing products based on total revenue and number of transaction.
- **High-Value Transaction Identification:** Identify transactions where the total sale exceeds a certain threshold and analyze these high-value transactions to understand their contribution to overall sales.
- **Time-Based Sales Analysis:** Classify sales transactions into different shifts (morning, afternoon, evening) and analyze how sales vary across different times of the day.
- **Business Analysis:** Use SQL queries to answer specific business questions, such as identifying top customers, most popular categories, and factors influencing sales performance.

##

#### Key Features

- **SQL:**
    Advanced querying techniques, including aggregate functions, joins, subqueries, and conditional filtering.
    Data transformation to prepare an analysis-ready dataset.

- **Tableau:**
    Interactive dashboards with slicers and filters for dynamic insights.
    Visual storytelling using charts like bar graphs, line charts, heat maps, and pie charts.
    Highlighted KPIs such as total sales, top-performing products, and highest revenue-generating regions.


#### Tools and Technologies
- *SQL:*  MySQL/PostgreSQL/Other SQL-based Database
- *Tableau:* Tableau Desktop/Online for visualizations
  
##

#### Project Workflow

#### Dataset Import and Preprocessing in SQL:
- Imported the retail sales dataset into a SQL database.
- Used structured queries to filter, clean, and manipulate the data as per analytical requirements.
- Prepared a refined dataset based on specific queries for export to Tableau.


#### SQL QUERIES

##### 1.  DATABASE SETUP

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
##

##### 2.  DATA RETRIEVAL QUERIES 

- **Counting the total number of transactions in retail_sales:**
```Sql
SELECT COUNT(*) FROM retail_sales;
```

- **Counting the number of distinct customers in retail_sales:**
```Sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
```
##

##### 3.  FILTERED DATA QUERIES 

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
##

##### 4.  AGGREGATED DATA QUERIES 

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
##

##### 5.  TIME-BASED DATA QUERIES 

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
##

##### 6.  DATA SEGREGATION 
	
- **Retrieving all data again to segregate it for documentation:**

```Sql
SELECT *  FROM retail_sales;
```

*** 

### Visualization in Tableau:
- Exported the processed SQL data to Tableau:
- Connected the Tableau workbook to the filtered database.
- Designed dashboards and visualizations to uncover insights, such as: Sales trends over time, Customer segmentation analysis, Product performance metrics.
##

#### Steps to Create Tableau Visualizations  

##### 1. **Install Tableau**  
   - Download and install Tableau Desktop from the official [Tableau website](https://www.tableau.com/).  
   - Ensure you have a valid license or use the free trial version.  

##### 2. **Connect to Data**  
   - Open Tableau Desktop and click on **"Connect"** from the left-hand panel.  
   - Select your data source type:  
     - For SQL Database: Choose the appropriate SQL connector (e.g., MySQL, PostgreSQL).  
     - For Excel/CSV: Click on "Microsoft Excel" or "Text File."  

   - Enter the database credentials or select the file path to connect.  

##### 3. **Import the Filtered SQL Data**  
   - Use the SQL query results (filtered dataset) exported to a file or directly query the database.  
   - Drag and drop the necessary tables or views into the Tableau workspace.  

##### 4. **Data Preparation**  
   - Perform **Joins** if you have multiple tables.  
   - Use the **Data Interpreter** if Tableau suggests cleaning the data.  
   - Rename fields for better readability, if needed.  

##### 5. **Create Visualizations**  
   - Navigate to the **"Sheet"** tab in Tableau.  
   - Drag and drop dimensions (e.g., `Region`, `Customer`) and measures (e.g., `Sales`, `Profit`) into the rows and columns.  
   - Use the **"Show Me"** panel to select chart types like bar charts, line charts, pie charts, or heatmaps.  
   - Apply filters to focus on specific data points, such as sales for a particular region or time frame.  

##### 6. **Build Dashboards**  
   - Go to the **"Dashboard"** tab.  
   - Drag and drop multiple sheets (visualizations) onto the dashboard layout.  
   - Customize the layout and use interactive features such as filters, slicers, and legends for better user engagement.  

##### 7. **Add Interactivity**  
   - Add filters to allow users to dynamically adjust the data they see (e.g., date range filters, product categories).  
   - Use **Actions** to create links between different sheets or dashboards.  

##### 8. **Customize and Style Visuals**  
   - Adjust colors, fonts, and sizes to match your presentation style.  
   - Use labels and annotations to highlight important trends or KPIs.  
   - Add titles and captions to make visualizations self-explanatory.  

##### 9. **Export and Share**  
   - Save the workbook as a `.twbx` file to include data and visualizations.  
   - Export the dashboards as images or PDFs for presentations.  
   - Publish the workbook to Tableau Online, Tableau Public, or Tableau Server for broader access.  

##

#### Findings
- **Customer Demographics:** The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions:** Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends:** Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights:** The analysis identifies the top-spending customers and the most popular product categories.

---

#### Conclusion
The integration of SQL and Tableau in the Retail Sales Analysis Project demonstrates the power of combining robust data processing with advanced visualization tools. SQL enables precise data manipulation and querying, ensuring that the dataset is optimized for analysis. Tableau then brings this data to life through interactive and intuitive visualizations, making it easier to uncover trends, understand customer behavior, and evaluate product performance.






