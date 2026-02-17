# SQL Practice – Database Operations

This document contains examples of SQL queries written during training.
It demonstrates basic knowledge of:

- CREATE TABLE
- SELECT
- INSERT
- UPDATE
- DELETE
- GROUP BY
- JOIN

---

# CREATE TABLE

```sql
CREATE TABLE Liliia_Dymytriieva (
  ID int PRIMARY KEY AUTO_INCREMENT,
  Name varchar(50) NOT NULL,
  Phone varchar(15) NOT NULL,
  BirthdayDate date NOT NULL
);
```

---

# SELECT Queries

```sql
-- 1. Select all clients from New York
SELECT * FROM Customers WHERE City = 'New York';

-- 2. Get clients older than 30
SELECT * FROM Customers WHERE Age > 30;

-- 3. Select orders with status "Completed"
SELECT * FROM Orders WHERE Status = 'Completed';

-- 4. Find clients whose phone starts with "123"
SELECT * FROM Customers WHERE PhoneNumber LIKE '123%';

-- 5. Orders after February 5, 2024
SELECT * FROM Orders WHERE OrderDate > '2024-02-05';

-- 6. Orders with amount greater than 300
SELECT * FROM Orders WHERE Sum > 300;

-- 7. Unique cities
SELECT DISTINCT City FROM Customers;

-- 8. Total number of orders
SELECT COUNT(*) FROM Orders;

-- 9. Clients without orders
SELECT * FROM Clients WHERE OrderID IS NULL;

-- 10. Orders from February 2024
SELECT * FROM Orders
WHERE OrderDate >= '2024-02-01'
AND OrderDate < '2024-03-01';

-- 11. Last 3 orders
SELECT * FROM Orders
ORDER BY OrderDate DESC
LIMIT 3;
```

---

# INSERT Queries

```sql
-- 1. Insert new client
INSERT INTO Customers (FirstName, LastName, Age, PhoneNum, City)
VALUES ('Tom', 'Hanks', 50, '111-222-3333', 'Los Angeles');

-- 2. Insert client without age
INSERT INTO Customers (FirstName, LastName, Age, PhoneNum, City)
VALUES ('Tom', 'Hanks', NULL, '111-222-3333', 'Los Angeles');

-- 3. Insert new order
INSERT INTO Orders (CustomerID, OrderDate, TotalAmount, Status)
VALUES (3, '2024-03-01', 400.50, 'Pending');

-- 4. Insert order for non-existing customer
-- If there is no foreign key constraint,
-- the order will be added successfully.

-- 5. Insert multiple clients
INSERT INTO Customers (FirstName, LastName, City)
VALUES 
('Tom', 'Hanks', 'Los Angeles'),
('Katy', 'Mayer', 'New York'),
('Max', 'Joy', 'Chicago');
```

---

# UPDATE Queries

```sql
-- 1. Update phone number
UPDATE Customers
SET PhoneNum = '999-888-7777'
WHERE CustomerID = 5;

-- 2. Update order status
UPDATE Orders
SET Status = 'Shipped'
WHERE Status = 'Pending';

-- 3. Update city
UPDATE Customers
SET City = 'San Francisco'
WHERE City = 'Los Angeles';
```

---

# DELETE Query

```sql
-- Delete orders with amount less than 100
DELETE FROM Orders WHERE Sum < 100;
```

---

# GROUP BY Queries

```sql
-- Total order amount per customer
SELECT CustomerID, SUM(Sum)
FROM Orders
GROUP BY CustomerID;

-- Number of clients in each city
SELECT City, COUNT(*)
FROM Customers
GROUP BY City;
```

---

# JOIN Query

```sql
-- Orders with customer names
SELECT Customers.FirstName,
       Customers.LastName,
       Orders.ID AS OrderID
FROM Customers
JOIN Orders
ON Customers.ID = Orders.CustomerID;
