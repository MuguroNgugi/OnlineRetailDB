# OnlineRetailDB
A relational database schema for an online retail business, including tables for products, categories, customers, orders, payments, and deliveries.


# DataBase Design: Schemas and Tables;

** Features

1. Stores.Products
** Purpose = Stores Details of available products
** Columns = -ProductID (Primary Key), -Name, -Description, -CategoryID (Foreign Key), -Price, -StocckQuantity
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

5. 
