# Shopify-Fall-2021-Data-Science-Internship

1a) There are outliers in the dataset. There are a couple of orders for shopid=42 with 2000 total items. There also expensive orders with sh0pid=78 where a single pair of shoes are worth $25725. The value $3145.35 is the mean of all the orders.
1b) Using the median, we can mitigate the affect of outliers on the AOV.
1c) The median order value is $284.

2a) 
SELECT COUNT(o.ShipperID) 
FROM Orders as o JOIN Shippers as s 
WHERE o.ShipperID = s.ShipperID AND s.ShipperName = "Speedy Express"

VALUE = 54

I saw that 'Speedy Express' was in the 'Shippers' table. 'Orders' was the table that had all the orders. So, I joined the two tables and got a count of the orders.

2b) 
SELECT LastName 
FROM (SELECT MAX(Max), LastName 
FROM (SELECT COUNT(o.EmployeeID) AS Max, LastName 
FROM Employees as e JOIN Orders AS o 
WHERE e.EmployeeID = o.EmployeeID
GROUP BY o.EmployeeID))

VALUE = Peacock

I had to join the 'Employees' and 'Orders' table. I needed to group by the 'EmployeeID', count the 'EmployeeID', find the max of the count and select the 'LastName' associated with that 'EmployeeID'.

2c) 
SELECT ProductName
FROM (SELECT MAX(Quantity), ProductName
FROM (SELECT SUM(od.Quantity) as Quantity, ProductName 
FROM OrderDetails AS od 
JOIN Orders AS o ON od.OrderID = o.OrderID
JOIN Products as p ON od.ProductID = p.ProductID
JOIN Customers as c ON c.CustomerID = o.CustomerID
WHERE c.Country = "Germany"
GROUP BY p.ProductName))

VALUE = Boston Crab Meat

I had to join the 'Orders', 'OrderDetails', 'Products' and 'Customers' tables together. I needed to get the associate Germany in 'Customers', associate the 'CustomerID' with 'OrderID' in 'Orders', associate the 'OrderID' with the 'ProductID' in 'OrderDetails' and find the 'ProductName' in 'Products'.
