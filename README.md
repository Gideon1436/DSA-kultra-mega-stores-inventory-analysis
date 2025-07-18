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
Select top 1 [Product_Category],
	count ([Product_Category])as [Product Count] 
		from [KMS Sql Case Study]
			group by Product_Category  
				Order by [Product Count] desc
```

## Exploratory Data Analysis
### Answers to the scenarios are found below:
```Sql
Select * from [KMS Sql Case Study]

-----1. Which product category had the highest sales?--------

Select top 1 [Product_Category],
	count ([Product_Category])as [Product Count] 
		from [KMS Sql Case Study]
			group by Product_Category  
				Order by [Product Count] desc

-----2. What are the Top 3 and Bottom 3 regions in terms of Sales?------
----Top 3----
Select top 3 [Region], sum (Sales) as [Total Sales]
	from [KMS Sql Case Study]
		group by Region
			Order by [Total Sales] desc

----Bottom 3----
Select top 3 [Region], sum (Sales) as [Total Sales]
	from [KMS Sql Case Study]
		group by Region
			Order by [Total Sales] asc


-----3. What were the total sales of appliances in Ontario?-----
Select Region, sum (sales) as [Total Sales]
	from [KMS Sql Case Study]
		where Region = 'Ontario'
			Group by Region 


-----4. Advice the mangement of KMS on what to do to increase the revenue from the bottom 10 customers----

Select top  10 [Customer_Name], sum ([Sales]) as [Total Sales]
	from [KMS Sql Case Study]
		group by Customer_Name
			Order by [Total Sales] asc


----5. KMS incurred the most shipping cost using which shipping method?

Select top 1 [Ship_Mode], sum  ([Shipping_Cost]) as [Total Shipping Cost]
	from [KMS Sql Case Study]
		group by Ship_Mode
			Order by [Total Shipping Cost] desc


----6. Who are the most valuable customers, and what products or services do they typically purchase?

Select [Customer_Name], Product_Name, sum (sales) as [Total Sales]
	from [KMS Sql Case Study]
		group by Customer_Name, Product_Name
			Order by [Total Sales] desc


-----7. Which small business customer had the highest sales?----

Select top 1 Customer_Name, Customer_Segment,
	sum ([Sales]) as [Total Sales]
		from [KMS Sql Case Study]
			where Customer_Segment = 'Small Business'
				group by Customer_Name, Customer_Segment
					Order by [Total Sales] desc


----8. Which corporate customer placed the most number of orders in 2009-2012?----


Select top 1 Customer_Name, Customer_Segment,
	count ([Order_ID]) as [Total Order]
		from [KMS Sql Case Study]
			where Customer_Segment = 'Corporate' and 
				Order_Date between '2009' and '2012'
					group by Customer_Name, Customer_Segment
						Order by [Total Order] desc


----9. Which customer was the most profitable one?----


Select top 1 Customer_Name, Customer_Segment,
	sum ([Profit]) as [Total Profit]
		from [KMS Sql Case Study]
			where Customer_Segment = 'Consumer'
				group by Customer_Name, Customer_Segment
					Order by [Total Profit] desc
	

----10. Which customer returned items, and what segment do they belong to?-----

Select Customer_Name, Customer_Segment, [Status]
		from [KMS Sql Case Study]
			join [dbo].[Order_Status]
				on [KMS Sql Case Study].Order_ID = [dbo].[Order_Status].[Order_ID]


----If the delivery truck is the most economical but the slowest shipping method and 
	------Express Air is the fatest but the most expensive one, do you think the company 
	-------------appropriately spent shipping costs based on the Order Priority? Explain your answer------


Select Order_Priority, Ship_Mode,
	count ([Order_ID]) as [Order Count],
		sum (Sales-Profit) as [Estimated Shipping Cost],
			Avg (Datediff (Day, [Order_Date], [Ship_Date])) as [Avg Ship Date]
				from [KMS Sql Case Study]
					group by Order_Priority, Ship_Mode	
						Order by Order_Priority, Ship_Mode desc
```

## Explantions to Scenario 4 and 11
### Scenario 4
KMS Management should assign someone to personally call these lowest spending customers, ask them what they need, offer them discounts for buying more, and suggest other products they might want to buy to help grow their business with the company.

### Scenario 11
The shipping data reveals that the company did not appropriately spend shipping costs based on the Order Priority because they used Express Air which is the most expensive for low-priority orders while often assigning slower Delivery Truck to critical and high-priority shipments.

## Contact
[Gideon Taiwo Otolorin] - [otoloringideon@gmail.com]
Project Link: https://github.com/Gideon1436/kultra-mega-stores-inventory-analysis

