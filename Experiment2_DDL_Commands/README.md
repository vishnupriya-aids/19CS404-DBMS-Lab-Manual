# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
CREATE TABLE Invoices(
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate DATE,
    Amount REAL,
    CHECK (DueDate>InvoiceDate),
    CHECK (Amount>0)
);
```

**Output:**

<img width="1192" height="270" alt="image" src="https://github.com/user-attachments/assets/7636dce0-5f23-4bee-af1b-7875aa70ee80" />


**Question 2**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint faile

```sql
CREATE TABLE Shipments(
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1197" height="240" alt="image" src="https://github.com/user-attachments/assets/b0a5abd5-b41f-416e-9ad0-95b2dfb6a9bf" />


**Question 3**
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
   
```sql
CREATE TABLE Invoices(
     InvoiceID INTEGER PRIMARY KEY,
     InvoiceDate DATE,
     Amount REAL CHECK (Amount>0),
     DueDate DATE CHECK (DueDate > InvoiceDate),
     OrderID INTEGER,
     FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1182" height="257" alt="image" src="https://github.com/user-attachments/assets/304f1350-f0f5-4696-81c4-735bbe172a44" />


**Question 4**
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


```sql
INSERT INTO Customers
SELECT * FROM Old_customers;
```

**Output:**

<img width="1180" height="246" alt="image" src="https://github.com/user-attachments/assets/442dfe25-d104-4e72-8491-2cbfb36bb185" />


**Question 5**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10

```sql
CREATE TABLE Products(
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT UNIQUE NOT NULL,
    Price REAL CHECK (Price>0),
    StockQuantity INTEGER CHECK (StockQuantity>=0)
);
```

**Output:**

<img width="1195" height="277" alt="image" src="https://github.com/user-attachments/assets/e7bab10b-a792-4ccb-a4e8-39f64f7785ff" />


**Question 6**
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


```sql
CREATE TABLE Departments(
   DepartmentID INTEGER,
   DepartmentName TEXT
);
```

**Output:**

<img width="1193" height="337" alt="image" src="https://github.com/user-attachments/assets/f1643b6d-0dd9-41b4-bc78-342b912275ce" />


**Question 7**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
 
For example:

Test	Result
SELECT RollNo, Name, Gender 
FROM Student_details 
WHERE RollNo = 204;


RollNo      Name          Gender
----------  ------------  ----------
204         Samuel Black  M


```sql
INSERT INTO Student_details (RollNo, Name, Gender) VALUES (204,'Samuel Black','M');
```

**Output:**

<img width="1180" height="295" alt="image" src="https://github.com/user-attachments/assets/4980101f-c416-422e-b65e-b787c3144715" />


**Question 8**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science
For example:

Test	Result
select * from Student_details;
RollNo      Name          Gender      Subject     MARKS
----------  ------------  ----------  ----------  ----------
205         Olivia Green  F
207         Liam Smith    M           Mathematic  85
208         Sophia Johns  F           Science

```sql
INSERT INTO Student_details(RollNo, Name, Gender, Subject, MARKS)VALUES(205,'Olivia Green','F',NULL,NULL),
(207,'Liam Smith','M','Mathematic',85),(208,'Sophia Johnson','F','Science',NULL);
```

**Output:**

<img width="1195" height="270" alt="image" src="https://github.com/user-attachments/assets/29e88606-41e4-4df2-9a7a-c7db59152d33" />


**Question 9**
---
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           first_name  varchar(50  0                       0
3           last_name   varchar(50  0                       0


```sql
ALTER TABLE employee ADD COLUMN first_name varchar(50);
ALTER TABLE employee ADD COLUMN last_name varchar(50);
```

**Output:**

<img width="1196" height="308" alt="image" src="https://github.com/user-attachments/assets/5158966d-114b-4ba8-8c23-eb97764909f3" />


**Question 10**
---
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0
For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      Mobilenumber     number           0                  0

```sql
ALTER TABLE Student_details ADD Mobilenumber number;
```

**Output:**

<img width="1191" height="352" alt="image" src="https://github.com/user-attachments/assets/c48ff437-743f-45a1-8795-9a5d1e3d2e8f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
