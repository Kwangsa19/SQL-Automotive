# SQL-Automotive

## Scenario
An automotive dealership sells various car models to customers. Each sale can include multiple car models. The dealership wants to analyze its sales data to:

1. Identify the relationship between sales and customers.
2. Calculate total sales revenue since the beginning of 2021.
3. Determine the top 3 most popular car models based on sales frequency.
4. Calculate the average sale amount per customer.

## Database and Tables
> Copy and paste this code into your SQL editor.

> This is conducted on MySQL/MariaDB relational database management system. 

```
CREATE DATABASE sql_automotive;

-- Create Customers table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(255)
);

-- Insert data into Customers
INSERT INTO Customers (CustomerID, CustomerName) VALUES
(1, 'Alice Johnson'),
(2, 'Bob Smith'),
(3, 'Carol Williams'),
(4, 'Dave Jones'),
(5, 'Eve Davis'),
(6, 'Frank White'),
(7, 'Grace Lee'),
(8, 'Henry Ford'),
(9, 'Isabel Ruiz'),
(10, 'Jack Ma'),
(11, 'Karen Hill'),
(12, 'Leo Messi'),
(13, 'Mia Wong'),
(14, 'Nora Elbaz'),
(15, 'Oscar Wells');

-- Create Cars table
CREATE TABLE Cars (
    CarID INT PRIMARY KEY,
    CarModel VARCHAR(255),
    Price DECIMAL(10, 2)
);

-- Insert data into Cars
INSERT INTO Cars (CarID, CarModel, Price) VALUES
(1, 'Sedan', 20000),
(2, 'SUV', 25000),
(3, 'Convertible', 30000),
(4, 'Hatchback', 18000),
(5, 'Coupe', 27000),
(6, 'Pickup', 28000),
(7, 'Van', 22000),
(8, 'Sports Car', 55000),
(9, 'Electric', 35000),
(10, 'Hybrid', 30000),
(11, 'Station Wagon', 24000),
(12, 'Minivan', 26000),
(13, 'Luxury Sedan', 45000),
(14, 'Compact', 19000),
(15, 'Off-Road', 33000);

-- Create Sales table
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    CustomerID INT,
    SaleDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

-- Insert data into Sales
INSERT INTO Sales (SaleID, CustomerID, SaleDate) VALUES
(1, 1, '2021-05-15'),
(2, 2, '2021-06-20'),
(3, 3, '2021-07-25'),
(4, 4, '2021-08-30'),
(5, 5, '2021-09-05'),
(6, 6, '2021-10-15'),
(7, 7, '2021-11-20'),
(8, 8, '2021-12-25'),
(9, 9, '2022-01-30'),
(10, 10, '2022-02-05'),
(11, 11, '2022-03-15'),
(12, 12, '2022-04-20'),
(13, 13, '2022-05-25'),
(14, 14, '2022-06-30'),
(15, 15, '2022-07-05');

-- Create SaleDetails table
CREATE TABLE SaleDetails (
    SaleDetailID INT PRIMARY KEY,
    SaleID INT,
    CarID INT,
    Quantity INT,
    FOREIGN KEY (SaleID) REFERENCES Sales(SaleID),
    FOREIGN KEY (CarID) REFERENCES Cars(CarID)
);

-- Insert data into SaleDetails
INSERT INTO SaleDetails (SaleDetailID, SaleID, CarID, Quantity) VALUES
(1, 1, 1, 1),
(2, 1, 2, 1),
(3, 2, 2, 2),
(4, 3, 3, 1),
(5, 4, 4, 1),
(6, 5, 5, 1),
(7, 6, 7, 1),
(8, 7, 8, 1),
(9, 8, 9, 1),
(10, 9, 10, 1),
(11, 10, 6, 2),
(12, 11, 11, 1),
(13, 12, 12, 1),
(14, 13, 13, 1),
(15, 14, 14, 2),
(16, 15, 15, 1),
(17, 6, 5, 2),
(18, 7, 4, 3),
(19, 8, 3, 1),
(20, 9, 2, 2),
(21, 10, 1, 1);
```

## Solutions
1. Identify the relationship between sales and customers.
```
SELECT s.SaleID, c.CustomerName
FROM Sales s
INNER JOIN Customers c ON s.CustomerID = c.CustomerID;
```
This query will return which customers (by name) corresponds to each sale. 
* First, we selected `SaleID` from `Sales` table and `CustomerName` from `Customers`. These will show in the output. The initial for `sales` table is s.
* Second, we used INNER JOIN to combine rows from `Sales` and `Customers` where there is match in the `CustomerID` columns of both tables.
* Last but not least, the result will show which customer (by name) corresponds to each sale.
* Output: 

![heidisql_EvmOGFFfkS](https://github.com/Kwangsa19/SQL-Automotive/assets/135963482/24e8de51-f593-4f6c-87b1-3bd397cbad98)

2. Calculate total sales revenue since the beginning of 2021.
```
SELECT SUM(sd.Quantity * ca.Price) AS TotalRevenue
FROM SaleDetails sd
INNER JOIN Sales s ON sd.SaleID = s.SaleID
INNER JOIN Cars ca ON sd.CarID = ca.CarID
WHERE s.SaleDate >= '2021-01-01';
```
This SQL query calculates the total revenue generated from car sales since January 1, 2021.
* First, we defined `TotalRevenue` as the output of the total revenue since 2021.
* We used `sd` as `SaleDetails` (to avoid confusion) for easier reference. The `ca` means table `cars`. 
* Then, we joinned sales details and SaleID on one condition which is SaledID in `SaleDetails` matches `SaleID` in the table `Sales`. After that, we joined sales details with `cars` on one condition which is `sd.CarID` matches `ca.CarID`.  
* The result will show the total revenue generated from `sales` since January 1st, 2021.
* Output:

![heidisql_NU08h1JyaG](https://github.com/Kwangsa19/SQL-Automotive/assets/135963482/875e6ae5-efc8-4245-ad26-72af766e2fd2)

   
3. Determine the top 3 most popular car models based on sales frequency.

```
SELECT ca.CarModel, COUNT(sd.CarID) AS SalesFrequency
FROM SaleDetails sd
INNER JOIN Cars ca ON sd.CarID = ca.CarID
GROUP BY sd.CarID
ORDER BY SalesFrequency DESC
LIMIT 3;
```
This SQL query is designed to find the top 3 most popular car models based on the frequency of their sales. 
* First, we set up `SalesFrequency` column for the output.
* Second, `saleDetails` table is inner joined with `cars` on one condition which is `sd.CarID` matches `ca.CarID`.
* Third, once we found what car models and sales frequency are, we group them by their `sd.CardID` and reverse them alphabetically. It allows the best selling car to appear at the top.
* Finally, we set `LIMIT` to 3 to display three best selling cars.
* Output:

![heidisql_7wOMmRJ1ep](https://github.com/Kwangsa19/SQL-Automotive/assets/135963482/4d373d57-c56a-4464-8844-22ebeb4537d6)


4. Calculate the average sale amount per customer.
```
SELECT c.CustomerName, AVG(sd.Quantity * ca.Price) AS AvgSaleAmount
FROM Sales s
INNER JOIN Customers c ON s.CustomerID = c.CustomerID
INNER JOIN SaleDetails sd ON s.SaleID = sd.SaleID
INNER JOIN Cars ca ON sd.CarID = ca.CarID
GROUP BY s.CustomerID;
```
This SQL query calculates the average sale amount per customer for all sales recorded in the database.
* First, we selected `CustomerName` from `customer` table and return the average sale amount by writing `AVG(sd.Quantity * ca.Price)`. The initial `sd` stands for `SaleDetails` and `ca` refers to `car` table.
* Second, from `sales s` table, we inner join it with `Customers c` on one condition that `CustomerID` in `sales` table matches `CustomerID` in `Customer` table.
* Third, we inner join it with `SaleDetails sd` on one condition that `SaleID` in `Sales` table matches `SaleID` in `SaleDetails`.
* Fourth, we inner join it with `cars ca` on one condition that `CarID` in `SaleDetails` table matches `CarID` in `cars`.
* Last but not least, we group them by `CustomerID` in the `Sales` table.
* Output:
  
![heidisql_HraJyWZtAR](https://github.com/Kwangsa19/SQL-Automotive/assets/135963482/358aa3ab-a96c-4741-b7a0-6fe1e8430c8b)

