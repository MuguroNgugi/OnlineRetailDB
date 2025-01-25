# OnlineRetailDB
A relational database schema for an online retail business, including tables for products, categories, customers, orders, payments, and deliveries.


# DataBase Design: Schemas and Tables;

** Features

1. Stores.Products
** Purpose = Stores Details of available products
** Columns = -ProductID (Primary Key), -Name, -Description, -CategoryID (Foreign Key), -Price, -StockQuantity
** Relatioship = Linked to Stores.Categories

2. Stores.Categories
** Purpose = Defines product Categories
** Columns = -CategoryID, -Name, -Description

3. Sales.Customers
** Purpose = Stores customer infomation
** Columns = -CustomerID (Primary Key), -FirstName, -LastName, -Email, -phone, -Address

4. Sales.Orders
** Purpose = Tracks customers orders
** Columns = -OrderID (Primary Key), CustomerID (Foreign Key), OrderDate, TotalAmount
** Relationship = Linked to Sales.Customers

5. Sales.OrderDetails
   ** Purpose = Stores details of individula items in each order
   ** Columns = OrderDetail (Primary Key), OrderID (Foreign Key), ProductID (Foreign Key), Quantity, Subtotal
   ** Relationship = Linked to Sales.Orders and Store.Products

7. Payments.PaymentsMethod
   ** Purpose = list avaiable paymnets methods
   ** Columns = PaymentMethodID (Primary Key), MethodName, Description

8.Payments.Payment
  ** Purpose = Trucks payment info fro orders
  ** Columns = PaymentID (Primary Key), OrderID (Foreign Key), PaymentMethodID (Foreign Key), Amount, PaymentDate
  ** Relationship = Linked to Sale.orders and Paymnent.PaymnetMethod

9. Delivery.DeliveryDetail
    ** Purpose = Stores delivery information for orders
    ** Columns = DeliveryID (Primary Key), OrderID (Foreign Key), DeliveryDate, Stuts (Pending, shipped, delivered), TrackingNumber
   ** Relationship = Linked to Sales.Orders.


CREATE DATABASE OnlineRetailDB;

USE OnlineRetailDB;

CREATE SCHEMA Stores;
CREATE SCHEMA Sales;
CREATE SCHEMA Payments;
CREATE SCHEMA Deliveries;

CREATE TABLE Stores.Categories
(
	CategoryID INT PRIMARY KEY IDENTITY (1,1), 
	Name NVARCHAR (100) NOT NULL,
	Description NVARCHAR (255)
); 

CREATE TABLE Stores.Products
(
	ProductID INT Primary key IDENTITY (1,1),
	Name NVARCHAR (100) NOT NULL,
	Description NVARCHAR (255),
	CategoryID INT NOT NULL,
	Price DECIMAL (10, 2) NOT NULL,
	StockQuantity INT NOT NULL,
	FOREIGN KEY (CategoryID) REFERENCES Stores.Categories(CategoryID)
);

CREATE TABLE Sales.Customers
(
	CustomerID INT PRIMARY KEY IDENTITY (1,1),
	FirstName NVARCHAR (100) NOT NULL,
	LastName NVARCHAR (100) NOT NULL,
	Email NVARCHAR (255) NOT NULL UNIQUE,
	Phone NVARCHAR (20),
	Address NVARCHAR (255)
);

CREATE TABLE Sales.Orders
(
	OrderID INT PRIMARY KEY IDENTITY (1,1),
	CustomerID INT NOT NULL,
	OrderDate DATE NOT NULL,
	TotalAmount DECIMAL (10, 2),
	FOREIGN KEY (CustomerID) REFERENCES Sales.Customers(CustomerID)
);

CREATE TABLE Sales.OderDeatils 
(
	OrderDetailID INT PRIMARY KEY IDENTITY (1,1),
	OrderID INT NOT NULL,
	ProductID INT NOT NULL,
	Quantity INT NOT NULL,
	Subtotal DECIMAL (10, 2),
	FOREIGN KEY (OrderID) REFERENCES Sales.Orders(OrderID),
	FOREIGN KEY (ProductID) REFERENCES Stores.Products(ProductID)
);

Create Payment Tables
CREATE TABLE Payments.PaymentMethods
(
	PaymentMethodID INT PRIMARY KEY IDENTITY (1,1),
	Method NVARCHAR (100) NOT NULL,
	Description NVARCHAR (255) 
);


CREATE TABLE Payments.Payments
(
	PaymentID INT PRIMARY KEY IDENTITY (1,1),
	OrderID INT NOT NULL,
	PaymentMethodID INT NOT NULL,
	Amount DECIMAL (10, 2) NOT NULL,
	PaymentDate DATE NOT NULL,
	FOREIGN KEY (OrderID) REFERENCES Sales.Orders(OrderID),
	FOREIGN KEY (PaymentMethodID) REFERENCES Payments.PaymentMethods(PaymentMethodID)
);

CREATE TABLE Deliveries.DeliveryDetails
(
	DeliveryID INT PRIMARY KEY IDENTITY (1,1),
	OrderID INT NOT NULL,
	DeliveryDate DATE,
	Status NVARCHAR (50),
	TrackingNumber NVARCHAR (50),
	FOREIGN KEY (OrderID) REFERENCES Sales.Orders(OrderID)
);

OnlineRetailDB/
├── README.md
├── create_tables.sql
├── sample_data.sql
├── er_diagram.png
├── LICENSE

