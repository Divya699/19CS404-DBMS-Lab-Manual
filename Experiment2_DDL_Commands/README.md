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
```
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
```

```
CREATE TABLE Invoices (


InvoiceID  INTEGER primary key,
InvoiceDate  DATE,
Amount  REAL CHECK(Amount>0),
DueDate  DATE CHECK(DueDate>InvoiceDate),
OrderID  INTEGER ,
foreign key(OrderID) REFERENCES  Orders(OrderID)
); 

```

**Output:**

<img width="1209" height="421" alt="AdobeExpressPhotos_11d046b42b634fed905ebf0344953a5b_CopyEdited" src="https://github.com/user-attachments/assets/bf883c93-35a7-49cd-8fea-157dfe151e61" />


**Question 2**
```

Write an SQL command can to add a column named email of type TEXT to the customers table

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0

 
```
```sql
ALTER TABLE customers
ADD COLUMN email TEXT;
```

**Output:**

<img width="1231" height="433" alt="AdobeExpressPhotos_8491848dd2584675add82e616418da75_CopyEdited" src="https://github.com/user-attachments/assets/97e83568-0ee5-4dda-95d5-6a447c3fdfab" />


**Question 3**
```
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
```sql
CREATE TABLE Products(
ProductID integer primary key,
ProductName text NOT NULL,
Price real CHECK(Price>0),
Stock integer CHECK(stock>=0)
);
```

**Output:**

<img width="1236" height="451" alt="AdobeExpressPhotos_c563e6790e7842e0a1767ccd02d6dc2a_CopyEdited" src="https://github.com/user-attachments/assets/592d7ffc-7e59-41cc-9263-b1c42aecdc2a" />

**Question 4**
```
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 
```
```sql
ALTER TABLE  customer
ADD COLUMN birth_date timestamp;
```

**Output:**

<img width="1209" height="496" alt="AdobeExpressPhotos_b1b6f3fa0edd40fcbc1ca07cb55103d7_CopyEdited" src="https://github.com/user-attachments/assets/cd0c268f-044d-439f-9d75-3badad212b33" />

**Question 5**
```
In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 
```
```sql
INSERT INTO Employee(EmployeeID,Name ,Position, Department,Salary )
VALUES(5,'George Clark','Consultant', NULL,NULL),
(7,'Noah Davis','Manager','HR',60000),
(8,'Ava Miller','Consultant','IT',NULL);

```

**Output:**
<img width="1221" height="418" alt="AdobeExpressPhotos_12c03c4497ea42a6916fbff524e88e0e_CopyEdited" src="https://github.com/user-attachments/assets/653e27d3-8f1f-42f0-a5a7-7eb2a62a3a6d" />


**Question 6**
```
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
For example:

Test	Result
pragma table_info('Events');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EventID     INTEGER     0                       0
1           EventName   TEXT        0                       0
2           EventDate   DATE        0                       0

```
```sql
create table Events(
EventID INTEGER,
EventName  TEXT,
EventDate  DATE 
);
```

**Output:**

<img width="1234" height="552" alt="AdobeExpressPhotos_b21e3dbbc72f452daaa1632e16d9b7c0_CopyEdited" src="https://github.com/user-attachments/assets/d10b5efe-029e-463b-accf-7b8127bb0e5b" />


**Question 7**
```
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616
```
```sql
INSERT INTO Customers(CustomerID,Name,Address,City,ZipCode)
values(301,'Michael Jordan','123 Maple St','Chicago',60616);

```

**Output:**
<img width="1212" height="365" alt="AdobeExpressPhotos_b6d4758a0c974ce398888b6667c1289d_CopyEdited" src="https://github.com/user-attachments/assets/a484bf68-0209-4391-819a-463b0762ddf8" />


**Question 8**
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700
```
```sql
Create table item(

item_id TEXT primary key,
item_desc TEXT NOT NULL,
rate  INTEGER NOT NULL,
icom_id  TEXT (4),

FOREIGN KEY (icom_id) REFERENCES company(com_id) ON UPDATE SET NULL ON DELETE SET NULL
);


```

**Output:**
<img width="1266" height="464" alt="AdobeExpressPhotos_f3337a82274f4cf9a51fa097fa71b025_CopyEdited" src="https://github.com/user-attachments/assets/dd2e889a-f271-4077-8633-2be0dcfcc294" />



**Question 9**
```
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5

```
```sql
INSERT INTO Products(ProductID, ProductName, Price, Stock )
SELECT ProductID, ProductName, Price, Stock 
FROM Discontinued_products;
```

**Output:**

<img width="864" height="374" alt="AdobeExpressPhotos_44aa717c69b841ddae0d7f6f9a4fc53a_CopyEdited" src="https://github.com/user-attachments/assets/907d505c-e95e-4583-a3b1-31903e601fb4" />


**Question 10**
```
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;
```
```sql
CREATE TABLE Attendance(
AttendanceID  INTEGER  PRIMARY KEY,
EmployeeID  INTEGER, 
AttendanceDate  DATE, 

Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),

FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)

);
```

**Output:**

<img width="919" height="455" alt="AdobeExpressPhotos_d052812fbb17431cae17090b2d67c44c_CopyEdited" src="https://github.com/user-attachments/assets/3236c0a1-cfa7-4ce7-ae29-9db65df5bea6" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
