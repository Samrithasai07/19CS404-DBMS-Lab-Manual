# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

**Program:**
```
CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, emp_name)
    VALUES (:NEW.emp_id, :NEW.emp_name);
END;
/
```

**Result:**

<img width="617" height="264" alt="image" src="https://github.com/user-attachments/assets/525b4d47-74c0-4af6-951b-82b892229d59" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

**Program:**
```
CREATE OR REPLACE TRIGGER trg_prevent_sensitive_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'Deletion not allowed on this table.');
END;
/
```

**Result:**

<img width="636" height="259" alt="image" src="https://github.com/user-attachments/assets/21a3192d-60bd-4e55-bc09-9df2a9420ad8" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

**Program:**
```
CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
```

**Result:**

<img width="570" height="256" alt="image" src="https://github.com/user-attachments/assets/8888d613-7322-4821-b885-84ea1fac6116" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

**Program:**
```
CREATE OR REPLACE TRIGGER trg_track_order_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/
```

**Result:**

<img width="580" height="271" alt="image" src="https://github.com/user-attachments/assets/2ddbe7b1-66f8-4909-b4da-84d0fffc797a" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

**Program:**
```
CREATE OR REPLACE TRIGGER trg_check_min_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'Salary below minimum threshold.');
    END IF;
END;
/
```

**Result:**

<img width="643" height="264" alt="image" src="https://github.com/user-attachments/assets/930bed7d-9562-43ff-a547-1ce9fc640d1b" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
