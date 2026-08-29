# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
```
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1

```
```
select 
DoctorID,
COUNT(DoctorID)  as TotalAppointments
FROM 
  Appointments 
GROUP BY DoctorID;
```

**Output:**

<img width="865" height="749" alt="AdobeExpressPhotos_e44d73db344f476da9f8d1b88b9144e9_CopyEdited" src="https://github.com/user-attachments/assets/6fa15f42-7768-4cdf-9db3-e776678ac187" />


**Question 2**
```
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table



For example:

Result
PatientID   TotalMedications
----------  ----------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1


```
```
select PatientID,
COUNT(PatientID) as TotalMedications
from Prescriptions 
GROUP BY PatientID;

```

**Output:**

![Output2](output.png)

**Question 3**
```
How many appointments are scheduled for each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
3           3
4           2
6           1
7           3
10          1


```
```
select DoctorID,
count(DoctorID) as TotalAppointments
from Appointments
group by doctorID;
```

**Output:**

![Output3](output.png)

**Question 4**
```
Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MAXIMUM
----------
5760.0


```
```
select MAX(purch_amt) as MAXIMUM
from orders;

```

**Output:**

![Output4](output.png)

**Question 5**
```
Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
employees_in_california
-----------------------
2
```

```
SELECT count (name) as employees_in_california 
from employee
where city ='California';

```

**Output:**

![Output5](output.png)

**Question 6**
```
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer


For example:

Result
COUNT
----------
9

```
```
select COUNT(*) as COUNT
from customer
where city!='Noida';
```

**Output:**

![Output6](output.png)

**Question 7**
```
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15
```

```
select name as fruit_name,inventory as lowest_quantity
from fruits
order by inventory ASC
LIMIT 1;
```

**Output:**

![Output7](output.png)

**Question 8**
```
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products

For example:

Result
category_id  Total_Cost
-----------  ----------
2            63

```
```
select category_id,SUM (price) AS Total_Cost
from products
group by category_id
HAVING sum(price)>50;

**Output:**

![Output8](output.png)

**Question 9**

```

fruit_name  lowest_quantity
----------  ---------------
Watermelon  15
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15
fruit_name  lowest_quantity
----------  ---------------
Apple       5
fruit_name  lowest_quantity
----------  ---------------
Apple       5
Passed all tests!  

Correct
Marks for this submission: 1.00/1.00.
Question 8
Correct
Mark 1.00 out of 1.00
Flag question
Question text
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products



For example:

Result
category_id  Total_Cost
-----------  ----------
2            63
Answer:(penalty regime: 0 %)
group by category_id
HAVING sum(price)>50;


Feedback
Expected	Got	
category_id  Total_Cost
-----------  ----------
2            63
category_id  Total_Cost
-----------  ----------
2            63
category_id  Total_Cost
-----------  ----------
2            63
4            70
category_id  Total_Cost
-----------  ----------
2            63
4            70
Passed all tests!  

Correct
Marks for this submission: 1.00/1.00.
Question 9
Correct
Mark 1.00 out of 1.00
Flag question
Question text
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.

Sample table: products



For example:

Result
category_id  product_name  Price
-----------  ------------  ----------
1            Orange        15.5
2            Monitor       25

```
```
select category_id,product_name,max(price) as Price
from products
group by category_id
HAVING max(price)>15;
```

**Output:**

![Output9](output.png)

**Question 10**
```
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products



For example:

Result
category_id  Revenue
-----------  ----------
1            49.5
2            126
3            79.44
```

```
select category_id ,sum(price * category_id) as Revenue
from products
group by category_id
HAVING sum(price*category_id)> 25;

```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
