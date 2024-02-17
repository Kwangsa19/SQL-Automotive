# SQL-Automotive

## 



## Database and Tables
> Copy and paste all of this into your SQL editor

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
