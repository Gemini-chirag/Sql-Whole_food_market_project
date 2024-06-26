## Whole Foods Market Retail Strategy Analysis
## Overview
This project aims to provide analytical support to Whole Foods Market in revamping their retail strategy in India. 
The analysis focuses on understanding order patterns, customer behavior, and return trends to help the company make data-driven business decisions. 
The data has been loaded into MySQL, and various SQL queries have been crafted to extract meaningful insights.

## Dataset Details
The dataset consists of three main tables: orders, customers, and returns. Below are the details of each table:

1.## Table: orders
Column Name	Type	Description
Order_ID	VARCHAR	Primary Key for each order placed
Order_Date	VARCHAR	Date when the order was placed
Ship_Date	VARCHAR	Date when the order was shipped
Customer_ID	VARCHAR	ID of the customer who placed the order
Segment	VARCHAR	Segment to which the product sold belongs
State	VARCHAR	State where the order was placed
City	VARCHAR	City where the order was placed
Product_ID	VARCHAR	ID of the product sold
Category	VARCHAR	Category of the product sold
SubCategory	VARCHAR	Subcategory of the product sold
Product_Name	VARCHAR	Name of the product sold
Sales	DOUBLE	Sale price of the order
Quantity	DOUBLE	Quantity of the product for which the order was placed
Discount	DOUBLE	Percentage discount offered on the MRP
Profit	DOUBLE	Total profit made on the order

2. Table: customers
Column Name	Type	Description
Customer_ID	VARCHAR	ID of the customer, primary key of the table
Customer_Name	VARCHAR	Name of the customer

4. Table: returns
Column Name	Type	Description
Order_ID	VARCHAR	Primary key of the order returned
Returned	VARCHAR	If the order was returned or not


## Key Queries and Insights
1. Total Sales by State and City
Query to calculate the total sales for each state and city:

sql

SELECT State, City, SUM(Sales) AS Total_Sales
FROM orders
GROUP BY State, City
ORDER BY Total_Sales DESC; 

2. Top 10 Most Profitable Products
Query to find the top 10 products based on profit:

sql

SELECT Product_Name, SUM(Profit) AS Total_Profit
FROM orders
GROUP BY Product_Name
ORDER BY Total_Profit DESC
LIMIT 10;

3. Customer Purchase Frequency
Query to calculate the number of orders placed by each customer:

sql

SELECT c.Customer_Name, COUNT(o.Order_ID) AS Order_Count
FROM customers c
JOIN orders o ON c.Customer_ID = o.Customer_ID
GROUP BY c.Customer_Name
ORDER BY Order_Count DESC;

4. Return Rate by Product Category
Query to calculate the return rate for each product category:

sql

SELECT o.Category, COUNT(r.Order_ID) * 100.0 / COUNT(o.Order_ID) AS Return_Rate
FROM orders o
LEFT JOIN returns r ON o.Order_ID = r.Order_ID AND r.Returned = 'Yes'
GROUP BY o.Category
ORDER BY Return_Rate DESC;

5. Discount Impact on Profit
Query to analyze the impact of discounts on profit:

sql

SELECT Discount, AVG(Profit) AS Avg_Profit
FROM orders
GROUP BY Discount
ORDER BY Discount;
