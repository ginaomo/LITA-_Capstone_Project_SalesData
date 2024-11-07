# LITA_Capstone_Project_SalesData
---
This where i want to analysis one of the projects for the completion of my Data analysis training with Incubator Hub

 ## Project Title: Performance Analysis for a Company
 ---
 
## Project Overview
---
This project is geared towards analyzing  the sales performance of a company by exploring sales data to uncover insights such as top-selling products, regional performance, and monthly sales trends. The primary objective is to create an interactive Power BI dashboard that highlights key findings, enabling data-driven decision-making to improve sales strategies. The project involves data exploration, preparation, and analysis using Excel and SQL, with final visualizations in Power BI- Excel Microsoft Excel[Download Here](https://www.microsoft.com)



## Tools used:
      - For initial data exploration, 
      - creating pivot tables, 
        and calculating summary statistics using Average and 
- SQL -Structured query language [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
     - For data extraction and analysis through structured queries.
- Power BI - power business intellegence:[download Here](https://power-bi-desktop.en.microsoft.com)
     - For building an interactive dashboard to visualize key insights, trends, and segments.
 - Gitup- Github account[Download Here](https://www.github.com)
     - for portfolio building





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

---2. Number of Sales transactions in each Region---

Select Region, count(OrderID) as Number_of_Sales
from[dbo].[SalesData_PS]
group by Region
order by Number_of_Sales desc

---3. The highest selling product by total sales value---

select Top 1 product,sum(quantity*unitPrice) as Total_sales_Value
from[dbo].[SalesData_PS]
group by Product

--4. Total Revenue by Product
Select Product, Sum(quantity*unitPrice) as TotalRevenue
from[dbo].[SalesData_PS]
group by product
order by TotalRevenue desc


--5.Total Monthly Sales for 2024(current year)

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

--6.TOP 5 CUSTOMERS BY TOTAL PURCHASE AMOUNT

Select top 5 Customer_Id, Sum(Quantity*UnitPrice) as Total_Purchase_Amount
from [dbo].[SalesData_PS]
group by Customer_Id
order by Total_Purchase_Amount desc

---7. % (PERCENTAGE) OF TOTAL SALES CONTRIBUTED BY EACH REGION---

Select Region,
Sum(quantity*unitprice) as Total_Sales,
Sum(quantity*unitprice)*100.0/(Select Sum(quantity*unitprice)
From [dbo].[SalesData_PS])
as Percentage_of_Totalsales
From [dbo].[SalesData_PS]
Group by Region
Order by percentage_of_totalsales desc


--8 PRODUCT WITH NO SALES IN LAST QUARTER--
Select distinct product
From [dbo].[SalesData_PS]
Where product Not In(
Select product
From [dbo].[SalesData_PS]
Where OrderDate >= DateAdd(quarter, -1, GetDate()) and OrderDate < GetDate());


```






## VISUALIZATION

![Power bi dashboard sales data](https://github.com/user-attachments/assets/eaa18494-624c-4320-9855-6f3a7f211c77)
