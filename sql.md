
### How many orders were shipped by Speedy Express in total?
```sql
SELECT COUNT(OrderID) AS "Total order by Speedy Express"
FROM Orders
where ShipperID = (select ShipperID
       from Shippers
       where ShipperName = 'Speedy Express')

```
### What is the last name of the employee with the most orders?
```sql
select LastName as " Last name of the employee with the most orders"
from Employees 
where EmployeeID = (select top 1 EmployeeID
                  from Orders
                  group by EmployeeID
                  order by count(EmployeeID) desc)

```
### What product was ordered the most by customers in Germany?
```sql
SELECT ProductName
FROM Products
Where ProductID  in (select TOP 1 ProductID
             from OrderDetails
                   where OrderID in (select OrderID 
             from Orders
             where CustomerID in (select CustomerID
                              from Customers
                                            where Country = 'Germany'))
                    group by ProductID
                    order by count(Quantity) desc)
```