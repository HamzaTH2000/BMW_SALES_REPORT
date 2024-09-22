## 1. Revenue, Revenue PY, and % Change
### a. By Year

```sql
SELECT 
    Year, 
    SUM(`Quantity Sold` * `Unit Price`) AS Revenue,
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY Year) AS Revenue_Previous_Year,
    (SUM(`Quantity Sold` * `Unit Price`) - LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY Year)) / 
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY Year) * 100 AS Percent_Change
FROM sales_data
GROUP BY Year
ORDER BY Year; 




SELECT 
    MONTHNAME(Date) AS MonthName, 
    MONTH(Date) AS MonthNumber,
    SUM(`Quantity Sold` * `Unit Price`) AS Revenue,
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY MONTH(Date)) AS Revenue_Previous_Month,
    (SUM(`Quantity Sold` * `Unit Price`) - LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY MONTH(Date))) / 
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY MONTH(Date)) * 100 AS Percent_Change
FROM sales_data
GROUP BY MonthName, MonthNumber
ORDER BY MonthNumber;



### c. By Weekdays
SELECT 
    DAYNAME(Date) AS Weekday, 
    DAYOFWEEK(Date) AS WeekdayNumber,
    SUM(`Quantity Sold` * `Unit Price`) AS Revenue,
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY DAYOFWEEK(Date)) AS Revenue_Previous_Weekday,
    (SUM(`Quantity Sold` * `Unit Price`) - LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY DAYOFWEEK(Date))) / 
    LAG(SUM(`Quantity Sold` * `Unit Price`), 1) OVER (ORDER BY DAYOFWEEK(Date)) * 100 AS Percent_Change
FROM sales_data
GROUP BY WeekdayNumber, Weekday
ORDER BY WeekdayNumber;


SELECT 
    Model, 
    SUM(`Quantity Sold`) AS Total_Quantity_Sold
FROM sales_data
GROUP BY Model
ORDER BY Total_Quantity_Sold DESC
LIMIT 10;



SELECT 
    Model, 
    MAX(`Unit Price`) AS Highest_Unit_Price
FROM sales_data
GROUP BY Model
ORDER BY Highest_Unit_Price DESC
LIMIT 5; 



SELECT 
    Model, 
    AVG(`Unit Price`) AS Average_Unit_Price
FROM sales_data
GROUP BY Model
ORDER BY Average_Unit_Price DESC
LIMIT 5;  



SELECT 
    Channel, 
    SUM(`Quantity Sold`) AS Total_Quantity_Sold
FROM sales_data
GROUP BY Channel
ORDER BY Total_Quantity_Sold DESC;



SELECT 
    Year,
    SUM(`Quantity Sold`) AS Quantity_Sold,
    LAG(SUM(`Quantity Sold`), 1) OVER (ORDER BY Year) AS Quantity_Sold_Previous_Year
FROM sales_data
GROUP BY Year
ORDER BY Year;


SELECT 
    Country, 
    SUM(`Quantity Sold` * `Unit Price`) AS Total_Revenue,
    SUM(`Quantity Sold`) AS Total_Quantity_Sold
FROM sales_data
GROUP BY Country
ORDER BY Total_Revenue DESC;


SELECT 
    Region,
    SUM(`Quantity Sold` * `Unit Price`) AS Revenue,
    SUM(`Quantity Sold`) AS Quantity_Sold
FROM sales_data
GROUP BY Region
ORDER BY Revenue DESC, Quantity_Sold DESC;






