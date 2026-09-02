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

## Code:
```
-- Create employees table
CREATE TABLE employees (
    emp_id INTEGER PRIMARY KEY,
    emp_name TEXT,
    designation TEXT,
    salary REAL
);

-- Create employee_log table
CREATE TABLE employee_log (
    log_id INTEGER PRIMARY KEY AUTOINCREMENT,
    emp_id INTEGER,
    emp_name TEXT,
    designation TEXT,
    salary REAL
);

-- Create AFTER INSERT trigger
CREATE TRIGGER log_employee_insert
AFTER INSERT ON employees
BEGIN
    INSERT INTO employee_log
    (emp_id, emp_name, designation, salary)
    VALUES
    (NEW.emp_id, NEW.emp_name, NEW.designation, NEW.salary);
END;

-- Insert employee
INSERT INTO employees
(emp_id, emp_name, designation, salary)
VALUES
(1, 'Arun', 'Developer', 40000);

-- Display employee log
SELECT * FROM employee_log;
```

**Expected Output:**

<img width="403" height="271" alt="image" src="https://github.com/user-attachments/assets/12b77210-066b-4eb2-8700-09680def12c9" />

- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

## Code:
```
-- Create sensitive_data table
DROP TABLE IF EXISTS sensitive_data;

CREATE TABLE sensitive_data (
    id INTEGER PRIMARY KEY,
    data TEXT
);

-- Insert sample data
INSERT INTO sensitive_data (id, data)
VALUES (1, 'Confidential Information');

-- Create trigger to prevent deletion
CREATE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
BEGIN
    SELECT RAISE(ABORT, 'ERROR: Deletion not allowed on this table.');
END;

-- Attempt to delete a record
DELETE FROM sensitive_data
WHERE id = 1;

SELECT * FROM sensitive_data;
```

**Expected Output:**

<img width="332" height="286" alt="image" src="https://github.com/user-attachments/assets/ef3eb3e0-5963-4a95-bf5e-1395953d4f90" />

- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

## Code:
```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER(10,2)
);

ALTER TABLE products ADD last_modified TIMESTAMP;

CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := CURRENT_TIMESTAMP;
END;
/

INSERT INTO products VALUES (1, 'Laptop', 50000, NULL);

UPDATE products
SET price = 55000
WHERE product_id = 1;

SELECT * FROM products;
```

**Expected Output:**


<img width="1223" height="138" alt="image" src="https://github.com/user-attachments/assets/2305eb55-4225-49bf-9681-9eb43a07d3f1" />

- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

## Code:
```
CREATE OR REPLACE TRIGGER trg_after_update_customer_orders
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

UPDATE customer_orders
SET order_amount = 150
WHERE order_id = 1;

SELECT * FROM audit_log;
```

**Expected Output:**


<img width="1190" height="388" alt="image" src="https://github.com/user-attachments/assets/08bc02b9-93bd-428a-abbc-823c8c642d3e" />

- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

## Code:
```
CREATE OR REPLACE TRIGGER trg_check_salary_before_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20001, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/
INSERT INTO employees (emp_id, emp_name, salary) VALUES (101, 'John Doe', 2500);
INSERT INTO employees (emp_id, emp_name, salary) VALUES (102, 'Jane Smith', 3500);
```

**Expected Output:**


<img width="1187" height="311" alt="image" src="https://github.com/user-attachments/assets/c1af8724-b9aa-4ed8-9202-de1b2c38ddbd" />

- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
