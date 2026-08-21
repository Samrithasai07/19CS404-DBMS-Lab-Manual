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
--
Write a SQL query to calculate the original price using the discount percentage and the given discounted price. Return product_id, discounted_price, discount_percentage, and original_price.

Sample table: Products

product_id | discounted_price | discount_percentage

 ------------+------------------+---------------------

 101 | 45.00 | 0.10 

102 | 63.75 | 0.15 

103 | 80.00 | 0.20

```sql
SELECT 
    product_id,
    discounted_price,
    discount_percentage,
    discounted_price / (1 - discount_percentage) AS original_price
FROM Products;
```

**Output:**

<img width="1242" height="388" alt="image" src="https://github.com/user-attachments/assets/348ec114-f759-4a49-93c7-5b97f18594ee" />


**Question 2**
---
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

```sql
update products
set quantity=quantity*1.1;
```

**Output:**

<img width="1224" height="695" alt="image" src="https://github.com/user-attachments/assets/525fcd67-6683-4c68-9f15-18c0efd7cceb" />

**Question 3**
---
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer
```sql
delete from customer
where CUST_COUNTRY='UK' and WORKING_AREA='London' and GRADE <3;
```

**Output:**

<img width="1266" height="579" alt="image" src="https://github.com/user-attachments/assets/0ed13bbd-0dce-4f5a-9dd6-ae1961f67038" />


**Question 4**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.

 
Sample table: Customer
```sql
delete from customer
where grade <>3;
```

**Output:**

<img width="1085" height="642" alt="image" src="https://github.com/user-attachments/assets/e5d47106-6273-4d9d-af04-ef60cdc4366c" />


**Question 5**
---
Write a SQL query to assign a priority of 'Low', 'Medium', or 'High' to value2 based on whether it is less than 20, between 20 and 50, or greater than 50, respectively in the Calculations table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0

```sql
select id, value2,
case 
  when value2 < 20 then 'Low'
  when value2 between 20 and 50 then 'Medium'
  when value2 > 50  then 'High'
end as priority
from Calculations;
```

**Output:**

<img width="933" height="576" alt="image" src="https://github.com/user-attachments/assets/05da50e5-f7ff-4ccf-a929-a0d94c262fc0" />


**Question 6**
---
Write a SQL query to find all employees along with the day of the week on which they were hired from the emp table

emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT  

```sql
SELECT 
    ename, 
    hiredate, 
    CASE STRFTIME('%w', hiredate)
        WHEN '0' THEN 'Sunday'
        WHEN '1' THEN 'Monday'
        WHEN '2' THEN 'Tuesday'
        WHEN '3' THEN 'Wednesday'
        WHEN '4' THEN 'Thursday'
        WHEN '5' THEN 'Friday'
        WHEN '6' THEN 'Saturday'
    END AS day_of_week
FROM emp;
```

**Output:**

<img width="871" height="459" alt="image" src="https://github.com/user-attachments/assets/5749efd8-d3b8-4425-9552-502057a8dd66" />


**Question 7**
---
Write a SQL query to find customers who are either from the city 'New York' or who have a grade greater than 200. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:
```sql
SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE city = 'New York'
   OR grade > 200;
```

**Output:**
<img width="1237" height="522" alt="image" src="https://github.com/user-attachments/assets/7903b5ba-738c-4424-99a6-69136ac11d34" />


**Question 8**
---
Write a query to fetch the EmpFname from the EmployeeInfo table in upper case and use the ALIAS name as EmpName.

EmployeeInfo Table

```sql
SELECT UPPER(EmpFname) AS EmpName
FROM EmployeeInfo;
```

**Output:**
<img width="705" height="392" alt="image" src="https://github.com/user-attachments/assets/96130043-a70b-406f-89eb-d4967fc4a828" />


**Question 9**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from doctors
where doctor_id between 2 and 4;
```

**Output:**

<img width="1224" height="936" alt="image" src="https://github.com/user-attachments/assets/c1020105-3137-4321-b8ca-c620f3769784" />


**Question 10**
---
Write a query to fetch 3 top salaried records from EmployeePosition table.

EmpID       EmpPosition  DateOfJoining  Salary
----------  -----------  -------------  ----------
1           Manager      2024-05-01     500000
1           Executive    2024-05-01     300000
3           Manager      2024-05-01     90000

```sql
SELECT EmpID, EmpPosition, DateOfJoining, Salary
FROM EmployeePosition
WHERE DateOfJoining = '2024-05-01'
  AND Salary > 5000
ORDER BY EmpID ASC, Salary DESC
LIMIT 3;
```

**Output:**

<img width="1140" height="354" alt="image" src="https://github.com/user-attachments/assets/0f01005b-9705-492b-9f88-8cc815a3856d" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
