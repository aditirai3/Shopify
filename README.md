# Shopify Fall 2021 Data Science Intern Challenge 

**Question 1:** Given some sample data, write a program to answer the following:
On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
Answer: The calculated AOV of $3145.13 corresponds to the mean of the dataset.
However, this is not the correct metric since the dataset contains several outliers.
The min value is 90 and max value is 704000, which has resulted in a skewed AOV
(mean value).
What metric would you report for this dataset?
Answer: A metric such as Median would be better suited for this analysis as it is less affected by outliers and skewed data

What is its value?
Answer: $284

Link to analysis: 

**Question 2:** SQL. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

How many orders were shipped by Speedy Express in total?

Answer: 54 orders.
Query:
SELECT COUNT(*) AS OrderNum
FROM [Orders]
JOIN [Shippers]
    ON [Shippers].ShipperID = [Orders].ShipperID
WHERE [Shippers].ShipperName = “Speedy Express”;

What is the last name of the employee with the most orders?
Answer: Peacock
Query:
SELECT [Employees].LastName, COUNT([Orders].EmployeeID) AS NumOrders
FROM [Orders]
JOIN [Employees] ON  [Employees].EmployeeID = [Orders].EmployeeID
GROUP BY [Employees].EmployeeID
ORDER BY NumOrders DESC LIMIT 1;


What product was ordered the most by customers in Germany?
Answer: Boston Crab Meat with total quantity ordered of 160
Query:
SELECT [Products].ProductName, SUM([OrderDetails].Quantity) AS TotalQuantity
FROM [Orders]
JOIN [OrderDetails] ON [OrderDetails].OrderID = [Orders].OrderID
JOIN [Products] ON [OrderDetails].ProductID = [Products].ProductID
JOIN [Customers] ON [Customers].CustomerID = [Orders].CustomerID
WHERE [Customers].Country = "Germany"
GROUP BY [Products].ProductID
ORDER BY TotalQuantity DESC
LIMIT 1;
