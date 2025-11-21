# Experiment 10: PL/SQL – Triggers
## NAME: MOHAMMAD SHAHIL
## REG.NO:212223240044

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

### Program:
```
 -- Clean up previous runs
DROP TABLE employee_log PURGE;
DROP TABLE employees PURGE;

-- Create main table
CREATE TABLE employees (
   emp_id NUMBER PRIMARY KEY,
   emp_name VARCHAR2(50),
   salary NUMBER
);

-- Create log table
CREATE TABLE employee_log (
   log_id NUMBER GENERATED ALWAYS AS IDENTITY,
   emp_id NUMBER,
   emp_name VARCHAR2(50),
   salary NUMBER,
   log_date DATE
);

-- Create trigger
CREATE OR REPLACE TRIGGER log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
   INSERT INTO employee_log(emp_id, emp_name, salary, log_date)
   VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/
INSERT INTO employees VALUES (101, 'John', 5000);
COMMIT;
SELECT * FROM employee_log;
SET SERVEROUTPUT ON;
INSERT INTO employees VALUES (102, 'Alice', 7000);
COMMIT;
SET SERVEROUTPUT ON;
INSERT INTO employees VALUES (105, 'bob', 8000);
COMMIT;
SELECT * FROM employee_log;

```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

 <img width="1008" height="389" alt="image" src="https://github.com/user-attachments/assets/f35c0c90-d89b-425a-a7bc-d00ca81ab65c" />


  

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.
### Program:
```
CREATE OR REPLACE TRIGGER prevent_delete_trigger
BEFORE DELETE ON sensitive_data
BEGIN
   RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/
DELETE FROM sensitive_data WHERE record_id = 1;

```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

<img width="940" height="189" alt="image" src="https://github.com/user-attachments/assets/5487443a-0c1d-49c0-baa8-4dc49c17bc44" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.
### Program:
```
DROP TABLE products PURGE;

CREATE TABLE products (
   product_id NUMBER PRIMARY KEY,
   product_name VARCHAR2(50),
   price NUMBER,
   last_modified DATE
);

CREATE OR REPLACE TRIGGER update_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
   :NEW.last_modified := SYSDATE;
END;
/
INSERT INTO products VALUES (1, 'Laptop', 700, NULL);
COMMIT;
SELECT * FROM products;

```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

<img width="1008" height="371" alt="image" src="https://github.com/user-attachments/assets/9421d130-5a23-47c3-940d-5542155233ae" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.
### Program:
```
-- Clean up if existing
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE audit_log PURGE';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/

BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE customer_orders PURGE';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/

-- Step 1: Create main table
CREATE TABLE customer_orders (
   order_id NUMBER PRIMARY KEY,
   customer_name VARCHAR2(50),
   order_value NUMBER
);

-- Step 2: Create audit log table with update counter
CREATE TABLE audit_log (
   update_count NUMBER
);

-- Initialize counter
INSERT INTO audit_log VALUES (0);
COMMIT;

-- Step 3: Create AFTER UPDATE trigger
CREATE OR REPLACE TRIGGER update_counter_trigger
AFTER UPDATE ON customer_orders
BEGIN
   UPDATE audit_log
   SET update_count = update_count + 1;
END;
/
INSERT INTO customer_orders VALUES (1, 'Alice', 500);
INSERT INTO customer_orders VALUES (2, 'Bob', 700);
COMMIT;
SELECT * FROM customer_orders;
UPDATE customer_orders SET order_value = 600 WHERE order_id = 1;
COMMIT;
UPDATE customer_orders SET order_value = 800 WHERE order_id = 2;
COMMIT;
SELECT * FROM audit_log;
```
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
<img width="740" height="292" alt="image" src="https://github.com/user-attachments/assets/8ca0a188-2aa3-4eac-a97a-7e846b8277d1" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### Program:
```
CREATE OR REPLACE TRIGGER check_salary_before_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
   IF :NEW.salary < 3000 THEN
      RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
   END IF;
END;
/
INSERT INTO employees VALUES (102, 'Ravi', 2500);
```
**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`


<img width="996" height="432" alt="image" src="https://github.com/user-attachments/assets/9a7f1f6b-04c3-4cf9-b62a-1c776f81d45c" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.


