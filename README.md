# LITA_Capstone_Project_SalesData
---
This where i want to analysis one of the projects for the completion of my Data analysis training with Incubator Hub

 ## Project Title: Performance Analysis for a Company
 ---
 
 [Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Findings](#finding)

[Conclusion](#conclusion)



 
 
## Project Overview
---
This project is geared towards analyzing  the sales performance of a company by exploring sales data to uncover insights such as top-selling products, regional performance, and monthly sales trends. The primary objective is to create an interactive Power BI dashboard that highlights key findings, enabling data-driven decision-making to improve sales strategies. The project involves data exploration, preparation, and analysis using Excel and SQL, with final visualizations in Power BI


## Data Sources:
---

The primary source of this data is HR DATA.excel provided by LITA and this is an open sources data that can freely downloaded without any restriction, online such as kaggle or fred, data.gov as well as any other sources like industry report.



## Tools Used:
 - Excel Microsoft Excel[Download Here](https://www.microsoft.com
     - For initial data exploration, 
     - creating pivot tables, 
       and calculating summary statistics using Average and 
 - SQL -Structured query language [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
     - For data extraction and analysis through structured queries.
 - Power BI - power business intellegence:[download Here](https://power-bi-desktop.en.microsoft.com)
     - For building an interactive dashboard to visualize key insights, trends, and segments.
 - Gitup- Github account[Download Here](https://www.github.com)
     - for portfolio building
  


 - 
  
 ## Data Cleaning and Preparation:
---
- Duplicates remover:
   - Check for duplicate rows in the dataset, especially in CustomerID or subscription records, and remove any redundancies.
   - Standardize Data:
   - Ensure consistency in data formats, such as dates (SubscriptionStart, SubscriptionEnd),
   - I checked for uniformity in categorical fields like SubscriptionType and Region.
   - Data Transformation: Calculate new fields, such as subscription duration   .
   - Active Status: Create an indicator for active subscriptions based on SubscriptionEnd and Canceled columns.
 
  ## Exploratory Data Analysis:

  - Retrieve the total sales for each product category. 
  - Find the number of sales transactions in each region. 
  - Find the highest-selling product by total sales value. 
  - Calculate total revenue per product. 
  - calculate monthly sales totals for the current year. 
  - find the top 5 customers by total purchase amount. 
  - calculate the percentage of total sales contributed by each region. 
  - identify products with no sales in the last quarter.
  ---
  

## Data Analysis:
---

```SQL
Create database Capstone_project

Select * from [dbo].[SalesData_PS]

---1.Total Sales for product Category---

Select Product, Sum(quantity*unitPrice) as TotalSales
from[dbo].[SalesData_PS]
group by product
order by TotalSales desc

Product	TotalSales
Shoes	613380
Shirt	485600
Hat	316195
Gloves	296900
Jacket	208230
Socks	180785
Above is summary of total Sales per Product



---2. Number of Sales transactions in each Region---

Select Region, count(OrderID) as Number_of_Sales
from[dbo].[SalesData_PS]
group by Region
order by Number_of_Sales desc

Region	Number_of_Sales
East	2483
North	2481
South	2480
West	2477

---3. The highest selling product by total sales value---

select Top 1 product,sum(quantity*unitPrice) as Total_sales_Value
from[dbo].[SalesData_PS]
group by Product

Product	Total_sales_Value
Shoes	613380



--4. Total Revenue by Product
Select Product, Sum(quantity*unitPrice) as TotalRevenue
from[dbo].[SalesData_PS]
group by product
order by TotalRevenue desc

Product	TotalRevenue
Shoes	613,380
Shirt	485,600
Hat	316,195
Gloves	296,900
Jacket	208,230
Socks	180,785
The Product with the highest sales is Shoes at the worth of 613,380



--5.Total Monthly Sales for 2024 (current year)

Select 
Case Month(orderdate)
when 1 then 'January'
when 2 then 'Febuary'
when 3 then 'March'
when 4 then 'April'
when 5 then 'May'
when 6 then 'June'
when 7 then 'July'
when 8 then 'August'
when 9 then 'September'
when 10 then 'October'
when 11 then 'November'
when 12 then 'December'
end as Month,
Sum(quantity*unitprice) as monthlysales
from [dbo].[SalesData_PS]
where Year(orderdate)= Year(getdate())
group by Month(orderdate)
order by Month(orderdate)

Month	monthlysales
January	198,400
Febuary	298,800
March   54,780
April	 9,440
May	 44,640
June	 148,200
July	 37,200
August	174,300

Monthly sales is as stated above, February has the highest performance with month sales of 298800


---6.TOP 5 CUSTOMERS BY TOTAL PURCHASE AMOUNT

Select top 5 Customer_Id, Sum(Quantity*UnitPrice) as Total_Purchase_Amount
from [dbo].[SalesData_PS]
group by Customer_Id
order by Total_Purchase_Amount desc

Customer_Id Total_Purchase_Amount

Cus1431    4235               
Cus1495    4235               
Cus1005    4235               
Cus1115    4235               
Cus1302    4235               

---7. % (PERCENTAGE) OF TOTAL SALES CONTRIBUTED BY EACH REGION---

Select Region,
Sum(quantity*unitprice) as Total_Sales,
Sum(quantity*unitprice)*100.0/(Select Sum(quantity*unitprice)
From [dbo].[SalesData_PS])
as Percentage_of_Totalsales
From [dbo].[SalesData_PS]
Group by Region
Order by percentage_of_totalsales desc
```

|Total_Sales|Region|Percentage_of_Totalsales|
|-----------|------|------------------------|
|#927,820   |South	|44%                     |
|#485925    |East |23%                     |
|#387,000	  |North |18%                     |
|#300,345	  |West  |14%                     |



```
---8 PRODUCT WITH NO SALES IN LAST QUARTER---
Select distinct product
From [dbo].[SalesData_PS]
Where product Not In(
Select product
From [dbo].[SalesData_PS]
Where OrderDate >= DateAdd(quarter, -1, GetDate()) and OrderDate < GetDate());

Product
Gloves
Jacket
Shirt
Shoes
Socks
```




![SALESDATA PIVOT TABLE COMBINE](https://github.com/user-attachments/assets/eec58b56-334a-4bdc-a9e2-85acdfb75758)






![CALCULATION ON EXCEL CONT](https://github.com/user-attachments/assets/7f8219c0-4b8b-4838-ad99-31138ceaff77)





![CALCULATION ON EXCEL WITH FORMULA](https://github.com/user-attachments/assets/4c937735-520e-48d3-8b05-a58b16de1680)











## Data Visualization


![Power bi dashboard sales data](https://github.com/user-attachments/assets/eaa18494-624c-4320-9855-6f3a7f211c77)

## Findings
---


Below is the detail findings based on the salesdata provided:

- Total Sales: $2,101,290

- Total Sales Amount: $2,101,290

- Total Quantity Sold: 68,469 units

- Total Number of Customers: 500

- Total Number of Orders (Order IDs): 20

Regional Sales Breakdown:

- South: $927,820 (highest-selling region, contributing 44% of total sales)
- East: $485,925
- North: $387,000
- West: $300,345 (lowest-selling region, contributing 14% of total sales)
- Total Number of Regions: 4 (North, South, East, and West)
Product Sales Performance:

- Total Number of Products: 6 (Shirt, Shoes, Hat, Socks, Jacket, and Gloves)
- Top-Selling Product: Shoes, with $613,380 in sales
- Lowest-Selling Product: Socks, with $180,785 in sales
Note: All products did not sell  in the last quarter, except for Hat.
Monthly Sales:

Highest Sales Month (2023): February, with $546,300
Highest Sales Month (2024): February, with $298,800
Both years experienced a noticeable drop in sales in March.
This summary captures key data points across regions, products, customers, and monthly trends, providing a comprehensive view of sales performance and customer engagement.








## Conclusions
---
Strong Regional Dependence:

- The South region is the dominant contributor, accounting for 44% of total sales, whereas West contributes the least (14%). This suggests a reliance on sales from the South and indicates growth potential in other regions.
Product Performance Variability:

- Shoes significantly outperform other products, while Socks have the lowest sales. This indicates high demand for Shoes, but also potential underperformance or low demand for Socks.
Seasonal Sales Patterns:

- February stands out as the highest sales month in both 2023 and 2024, showing a seasonal peak. However, sales sharply drop in March in both years, indicating potential challenges in maintaining sales momentum after February.
Customer and Order Volume:

- With 500 customers and only 20 orders, there is a possibility that orders are either bulk orders or there’s a high concentration of purchases among a few customers.

## Recommendations
---
Expand in Underperforming Regions:

- Increase marketing and promotional efforts in the West and North regions to drive sales, using region-specific campaigns that highlight popular or discounted items. Expanding the presence of these regions could balance sales reliance and enhance overall performance.
Boost Sales for Low-Performing Products:

- For Socks and other lower-selling items, consider bundling them with high-selling products (like Shoes) to drive incremental sales.
Offering targeted promotions, discounts, or limited-time offers for low-selling products could increase their attractiveness.
Maintain and Extend February Sales Peaks:

- Given the high February sales in both years, consider launching early-year campaigns and sales events that start in January, aiming to capture momentum and prevent the drop-off in March.
Introducing loyalty programs or incentives during February could encourage customers to return in March, reducing seasonal dips.
Enhance Customer Engagement:

- With only 20 orders from 500 customers, there's room to increase purchase frequency. Implement customer retention programs, such as:
Loyalty rewards for repeat purchases
Email marketing to engage customers with product updates, special offers, or reminders about products they’ve previously purchased.
Product-Specific Campaigns and Trend Analysis:

- Given the popularity of Shoes, conduct a deeper analysis into what drives demand for them and apply insights to other product lines. Running product-specific marketing campaigns that align with current trends may attract more customers to a wider range of products.
These strategies aim to maximize regional potential, balance product demand, and build customer loyalty, ultimately supporting sales growth and revenue stability throughout the year.













Conclusion:
---
