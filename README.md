# DSA-kultra-mega-stores-inventory-analysis
This is a project on SQL-based business intelligence analysis of KMS inventory and sales data

## Project Overview
Business Intelligence analysis of Kultra Mega Stores (KMS) inventory and sales data from 2009-2012, focusing on sales performance, customer analysis, and operational efficiency.

## Company Background
**Kultra Mega Stores (KMS)** is headquartered in Lagos, Nigeria, specializing in office supplies and furniture. The company serves:
- Individual consumers
- Small businesses (retail)
- Large corporate clients (wholesale)

## Dataset Description
- **Analysis Period**: 2009-2012
- **Geographic Focus**: Lagos, Nigeria operations
- **Data Source**: KMS order management system
- **Record Types**: Customer orders, product sales, shipping data

## Analysis Scenarios

### Case Scenario I - Sales Performance
1. Product category performance analysis
2. Regional sales comparison (Top 3 vs Bottom 3)
3. Ontario appliance sales analysis
4. Bottom 10 customers revenue optimization
5. Shipping cost analysis by method

### Case Scenario II - Customer Intelligence
6. Most valuable customers identification
7. Top small business customer analysis
8. Corporate customer order frequency (2009-2012)
9. Most profitable consumer customer
10. Customer return analysis by segment
11. Shipping cost optimization analysis

## Key SQL Techniques Used
- Complex JOINs and subqueries
- Window functions for ranking
- Aggregate functions and GROUP BY

## Tools Used
- SQL Server

## Database Schema
```sql
-- Main tables structure
Orders (order_id, customer_id, product_id, order_date, quantity, sales)
Customers (customer_id, customer_name, segment, region)
Products (product_id, product_name, category, sub_category)
Shipping (order_id, shipping_mode, shipping_cost, order_priority)
```
## Query Examples
-- Example: 
```sql
Top 3 regions by sales
SELECT region, SUM(sales) as total_sales
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY region
ORDER BY total_sales DESC
LIMIT 3;
```
## Contact
[Gideon Taiwo Otolorin] - [otoloringideon@gmail.com]
Project Link: https://github.com/Gideon1436/kultra-mega-stores-inventory-analysis

