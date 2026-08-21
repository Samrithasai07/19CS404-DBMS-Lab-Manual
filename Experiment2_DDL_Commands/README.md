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
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
CREATE TABLE Attendance(
  AttendanceID INTEGER PRIMARY KEY,
  EmployeeID INTEGER,
  AttendanceDate DATE,
  Status TEXT CHECK(Status IN ('Present','Absent','Leave')),
  FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)

);
```

**Output:**

<img width="1286" height="428" alt="image" src="https://github.com/user-attachments/assets/aa32a9e2-06d0-4158-9a12-fdc9a0082b2f" />


**Question 2**
---
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

```sql
ALTER TABLE Employee
ADD COLUMN first_name varchar(50);

ALTER TABLE Employee
ADD COLUMN last_name varchar(50);
```

**Output:**

<img width="1279" height="444" alt="image" src="https://github.com/user-attachments/assets/3b9157af-8d0a-4ba5-b59d-04a2d39acb2e" />


**Question 3**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1277" height="363" alt="image" src="https://github.com/user-attachments/assets/2853e145-2ad3-4959-a809-5380f4cb0e01" />


**Question 4**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4),
    FOREIGN KEY (icom_id)
    REFERENCES company (com_id)
    ON UPDATE SET NULL
    ON DELETE SET NULL
);

```

**Output:**

<img width="1282" height="474" alt="image" src="https://github.com/user-attachments/assets/2afd0a88-8764-4a61-aafb-9b3e5fddee32" />


**Question 5**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```sql
INSERT INTO Books (ISBN, Title, Author)
VALUES ('978-6655443321', 'Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="1257" height="428" alt="image" src="https://github.com/user-attachments/assets/044abf61-fc89-412a-ac19-da74e7a4440c" />


**Question 6**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

```sql
ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);
```

**Output:**

<img width="1259" height="465" alt="image" src="https://github.com/user-attachments/assets/af977a06-268f-4eb1-b0d8-e9b7ee1045c8" />

**Question 7**
---
Insert the following students into the Student_details table: RollNo Name Gender Subject MARKS


```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (202, 'Ella King', 'F', 'Chemistry', 87);
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (203, 'James Bond', 'M', 'Literature', 78);
```

**Output:**

<img width="1221" height="348" alt="image" src="https://github.com/user-attachments/assets/47efb505-e565-41d8-88eb-642cb3288dc0" />

**Question 8**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.


```sql
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (301, 'Michael Jordan', '123 Maple St', 'Chicago', '60616');
```

**Output:**

<img width="1252" height="349" alt="image" src="https://github.com/user-attachments/assets/16ac5c71-b954-4f34-8013-1e1c29f7036b" />


**Question 9**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL NOT NULL,
    DueDate DATE,
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    CHECK (Amount > 0),
    CHECK (DueDate > InvoiceDate)
);
```

**Output:**

<img width="1254" height="397" alt="image" src="https://github.com/user-attachments/assets/e6443140-aba5-4c05-ab53-930d3182ce75" />


**Question 10**
---
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375

```sql
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (306, 'Diana Prince', 'Themyscira', NULL, NULL);

INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (307, 'Bruce Wayne', 'Wayne Manor', 'Gotham', 10007);

INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (308, 'Peter Parker', 'Queens', NULL, 11375);
```

**Output:**

<img width="1256" height="412" alt="image" src="https://github.com/user-attachments/assets/22247929-3bdf-4666-82b3-3745a7eaab2d" />

## SEB GRADE
<img width="1103" height="97" alt="image" src="https://github.com/user-attachments/assets/903fb8fa-63ff-4722-89a3-661db944531a" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
