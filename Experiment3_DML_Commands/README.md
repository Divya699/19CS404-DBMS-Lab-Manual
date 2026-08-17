# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
```
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2
```
```sql
UPDATE products
SET reorder_lvl = reorder_lvl*0.7
WHERE cost_price>50 AND quantity<100;

```

**Output:**


<img width="1198" height="601" alt="AdobeExpressPhotos_824f1be5ea0c4b209406faf0858a2cad_CopyEdited" src="https://github.com/user-attachments/assets/f9b61215-8960-4f93-aa30-43c679a0cb49" />

**Question 2**
```

Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test	Result
select changes();
changes()
----------
1
```

```sql
UPDATE suppliers
SET address = '58 Lakeview, Magnolia'
WHERE supplier_id=5;
```

**Output:**

<img width="1196" height="524" alt="AdobeExpressPhotos_b01f941a804947ec85f3363b2c01582b_CopyEdited" src="https://github.com/user-attachments/assets/9a9c39a0-a73a-4784-85a5-d64251240589" />


**Question 3**
```
For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
1
```

```sql
UPDATE sales
SET sell_price = sell_price + 3
WHERE product_id IN(
SELECT product_id
FROM products
WHERE supplier_id=4
);
```

**Output:**

<img width="1196" height="524" alt="Screenshot 2026-08-17 112323" src="https://github.com/user-attachments/assets/0f2bf656-844f-4c0d-87a6-0fe66dc48e39" />


**Question 4**
```
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```

```sql
UPDATE products
SET quantity = quantity*1.1;
```

**Output:**


<img width="1187" height="683" alt="AdobeExpressPhotos_cfd6d01797ab4fc3a31359c19cdebce8_CopyEdited" src="https://github.com/user-attachments/assets/7dc5d897-16c1-4776-8061-4de5cc9e09ce" />


**Question 5**
```
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE job_id = 'SA_REP' AND EMAIL='updated' LIMIT 5;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
150          Peter       updated     10500       SA_REP
151          David       updated     10000       SA_REP
152          Peter       updated     9500        SA_REP
153          Christophe  updated     8500        SA_REP
154          Nanette 
```

```sql
update employees
set salary = salary + 500,
email = 'updated'
where job_id = 'SA_REP' and commission_pct>0.15;
```

**Output:**

<img width="1202" height="663" alt="AdobeExpressPhotos_8afe6f5df6d842d2b9bdf41d7504f8eb_CopyEdited" src="https://github.com/user-attachments/assets/a2a3f2df-5a46-472d-b87a-dc9515262efd" />


**Question 6**
```
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
3           3           3           2024-03-25
```
```sql
delete from surgeries
where surgery_date = '2024-02-28'
```
**Output:**

<img width="1199" height="570" alt="AdobeExpressPhotos_74fff16a958d43f28503a2f7734524d7_CopyEdited" src="https://github.com/user-attachments/assets/bcaf7d2b-d524-4503-8c19-e152a43811fd" />


**Question 7**
```
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
0
```
```sql
DELETE FROM Customer
WHERE GRADE=3
AND CUST_NAME LIKE'%BBB%'
AND PAYMENT_AMT > 2000;
```

**Output:**


<img width="1199" height="570" alt="Screenshot 2026-08-17 111728" src="https://github.com/user-attachments/assets/05d82a81-3e28-4697-9585-b47cdaa6ee66" />

**Question 8**
```
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
2
```
```sql
delete from Customer
where CUST_COUNTRY NOT IN ('UK','USA','canada')
and grade>=3;

```

**Output:**


<img width="1219" height="588" alt="AdobeExpressPhotos_160c3013f6764cf8893a47477c786414_CopyEdited" src="https://github.com/user-attachments/assets/f12b4575-8a68-43db-97dd-cead87cb2cec" />


**Question 9**
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
4
```


```sql
delete from customer
where CUST_COUNTRY = 'UK'
and WORKING_AREA = 'London'
and GRADE < 3;
```

**Output:**

<img width="1223" height="590" alt="AdobeExpressPhotos_a659e48ec3eb4c2d8acb71c4cc34b5d0_CopyEdited" src="https://github.com/user-attachments/assets/7bf12ec8-41e9-4a40-b23a-1cdbcb9109f1" />


**Question 10**
```
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00012      Steven      San Jose    San Jose      USA           1           5000         7000         9000         3000             KRFYGJK     A012
C00003      Martin      Torento     Torento       Canada        2           8000         7000         7000         8000             MJYURFD     A004
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
changes()
----------
6
```

```sql
delete from Customer
where LENGTH (CUST_NAME)=6;

```

**Output:**


<img width="1228" height="686" alt="Screenshot 2026-08-17 111400" src="https://github.com/user-attachments/assets/57bab82d-5610-44e1-ae29-3073894b766c" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
