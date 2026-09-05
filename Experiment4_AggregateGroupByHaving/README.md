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
--
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
SELECT 
    MIN(purch_amt) AS MINIMUM
FROM 
    orders;
```

**Output:**

<img width="865" height="425" alt="image" src="https://github.com/user-attachments/assets/e151e97d-6af0-418b-9d00-150729711c0e" />


**Question 2**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select sum(purch_amt) as TOTAL
from orders;
```

**Output:**

<img width="861" height="408" alt="image" src="https://github.com/user-attachments/assets/dc301625-ba2f-4eb2-9a95-49e6e03cb80c" />


**Question 3**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT 
    AVG(income) AS Average_Salary
FROM 
    employee;
```

**Output:**

<img width="857" height="402" alt="image" src="https://github.com/user-attachments/assets/af9e3f2a-7bda-4d00-a58e-2d289aed8714" />


**Question 4**
---
How many prescriptions were written for each medication?

Sample tablePrescriptions Table
```sql
select medication,count(*) as  TotalPrescriptions
from prescriptions
group by medication;
```

**Output:**

<img width="856" height="836" alt="image" src="https://github.com/user-attachments/assets/e1066ad7-5a5b-4fd9-b3bc-2723279514ba" />


**Question 5**
---
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?

Sample table: Patients Table
```sql
SELECT
    CASE
        WHEN (2025 - CAST(strftime('%Y', DateOfBirth) AS INTEGER)) <= 30
            THEN '20-30'
        WHEN (2025 - CAST(strftime('%Y', DateOfBirth) AS INTEGER)) <= 40
            THEN '31-40'
        WHEN (2025 - CAST(strftime('%Y', DateOfBirth) AS INTEGER)) <= 50
            THEN '41-50'
        ELSE 'Above 50'
    END AS AgeGroup,
    COUNT(*) AS TotalPatients
FROM Patients
GROUP BY AgeGroup
ORDER BY
    CASE AgeGroup
        WHEN '20-30' THEN 1
        WHEN '31-40' THEN 2
        WHEN '41-50' THEN 3
        WHEN 'Above 50' THEN 4
    END;
```

**Output:**

<img width="852" height="552" alt="image" src="https://github.com/user-attachments/assets/f50a0e51-efe8-4cb8-9c41-23796708797a" />

**Question 6**
---
What is the count of male and female patients?

Sample table: Patients Table
```sql
select gender,count(*) as TotalPatients
from patients
group by gender;
```

**Output:**

<img width="863" height="460" alt="image" src="https://github.com/user-attachments/assets/572683e5-cb5a-4f5f-bf53-90ef7c3b4cb3" />

**Question 7**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.

Sample table: customer1
```sql
SELECT 
  CAST(age / 5 AS INTEGER) * 5 AS age_group,
  SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY CAST(age / 5 AS INTEGER) * 5
HAVING SUM(salary) > 5000;
```

**Output:**

<img width="872" height="462" alt="image" src="https://github.com/user-attachments/assets/1eacd36d-9c33-4656-bd27-1e861775d837" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.
```sql
select occupation,avg(workhour) as 'AVG(workhour)'
from employee1
group by occupation
having AVG(workhour) between 10 and 12;
```

**Output:**

<img width="860" height="470" alt="image" src="https://github.com/user-attachments/assets/02c32465-bbd5-4032-a353-970af58528b4" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.
```sql
SELECT 
    jdate,
    MIN(workhour) AS "MIN(workhour)"
FROM 
    employee1
GROUP BY 
    jdate
HAVING 
    MIN(workhour) < 10;
```

**Output:**

<img width="852" height="532" alt="image" src="https://github.com/user-attachments/assets/aeb3e483-e448-44b0-9fc2-614f382896dd" />


**Question 10**
---
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products
```sql
select category_id,min(price) as Price
from products
group by category_id
having min(price) < 10;
```

**Output:**

<img width="876" height="463" alt="image" src="https://github.com/user-attachments/assets/a6517b1c-ae83-404e-aa6b-104e8140f62e" />

## FINAL GRADE
<img width="1132" height="117" alt="image" src="https://github.com/user-attachments/assets/ca02f92c-c4d6-45f3-b187-fa1e68225173" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
