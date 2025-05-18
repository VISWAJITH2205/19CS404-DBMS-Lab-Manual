
**Question 1**
--
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	
SELECT * FROM Customers WHERE CustomerID = 301;

Result
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616


```
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode) VALUES
('301','Michael Jordan', '123 Maple St', 'Chicago', '60616');
```

**Output:**

![Screenshot 2025-05-17 081621](https://github.com/user-attachments/assets/7b23f678-5b9a-4a44-a63f-25bd47fc9590)


**Question 2**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1

```
CREATE TABLE Invoices (
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK (Amount > 0),
DueDate DATE,
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
CHECK (DueDate > InvoiceDate)
);
```

**Output:**

![Screenshot 2025-05-17 082038](https://github.com/user-attachments/assets/e3c4b9d2-c757-4adc-9c86-1304573de34c)
![Screenshot 2025-05-17 082054](https://github.com/user-attachments/assets/4c7c5a09-b537-43dd-a3c8-614dafd61a33)

**Question 3**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           designatio  varchar(50  0                       0

```
ALTER TABLE employee
ADD designation varchar(50);
```

**Output:**

![Screenshot 2025-05-17 082354](https://github.com/user-attachments/assets/1103e446-e573-4ee4-8050-bc132dae2024)

**Question 4**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York

```
CREATE TABLE Department (
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
);
```

**Output:**

![Screenshot 2025-05-17 082533](https://github.com/user-attachments/assets/5e0d882f-be93-4b5b-b40f-bf98174cbcc6)
![Screenshot 2025-05-17 082545](https://github.com/user-attachments/assets/e8e0c0c0-af0f-4af8-a709-04a8114b0bc0)

**Question 5**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0


```
ALTER TABLE customer
ADD discount DECIMAL(5,2);
```

**Output:**

![Screenshot 2025-05-17 083036](https://github.com/user-attachments/assets/27e8ebf9-581e-4db3-b386-3331cf313943)

**Question 6**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851


```
INSERT INTO Books (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished FROM Out_of_print_books;
```

**Output:**

![Screenshot 2025-05-17 083246](https://github.com/user-attachments/assets/62014c17-517f-43ae-8ab3-705ebbbf2256)

**Question 7**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0


```
CREATE TABLE Reviews (
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

![Screenshot 2025-05-17 083428](https://github.com/user-attachments/assets/4ca99a70-3a2c-4ff6-9d0a-d63726f45560)

**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName

```
CREATE TABLE Products (
ProductID INTEGER PRIMARY KEY,
ProductName TEXT NOT NULL,
Price REAL CHECK (Price > 0),
Stock INTEGER CHECK (Stock >= 0)
);
```

**Output:**

![Screenshot 2025-05-17 083547](https://github.com/user-attachments/assets/c696c368-e04a-4b34-81f2-ac475e2864f8)


**Question 9**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT
For example:

Test	Result
pragma table_info('Departments');
cid    name             type        notnull     dflt_value  pk
-----  ---------------  ----------  ----------  ----------  ----------
0      DepartmentID     INTEGER     0                       0
1      DepartmentName   TEXT        0                       0


```
CREATE TABLE Departments (
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

![Screenshot 2025-05-17 083700](https://github.com/user-attachments/assets/930453fa-bb39-4c0e-8ec5-75db57c884a4)

**Question 10**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com


```
INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email FROM old_customers;
```

**Output:**

![Screenshot 2025-05-17 084330](https://github.com/user-attachments/assets/ec7320f1-beaf-4f72-9830-e5a28f7a5425)

