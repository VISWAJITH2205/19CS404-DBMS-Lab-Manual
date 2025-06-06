# Experiment 10: PL/SQL – Triggers
---
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

---
## 1. Write a trigger to log every insertion into a table.

PROGRAM :

```
CREATE TABLE employees (
    emp_id     NUMBER PRIMARY KEY,
    emp_name   VARCHAR2(100),
    emp_dept   VARCHAR2(50),
    emp_salary NUMBER
);
CREATE TABLE employee_log (
    log_id       NUMBER GENERATED BY DEFAULT ON NULL AS IDENTITY PRIMARY KEY,
    emp_id       NUMBER,
    emp_name     VARCHAR2(100),
    emp_dept     VARCHAR2(50),
    emp_salary   NUMBER,
    inserted_at  DATE DEFAULT SYSDATE
);
CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, emp_name, emp_dept, emp_salary)
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.emp_dept, :NEW.emp_salary);
END;
/
INSERT INTO employees (emp_id, emp_name, emp_dept, emp_salary)
VALUES (101, 'Alice', 'HR', 50000);

SELECT * FROM employee_log;

```
OUTPUT :


![Screenshot 2025-05-21 194805](https://github.com/user-attachments/assets/896e7cf9-1f20-41ac-98c5-e766026f79f4)


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.

PROGRAM :

```
CREATE TABLE sensitive_data (
    data_id    NUMBER PRIMARY KEY,
    data_value VARCHAR2(100)
);

CREATE OR REPLACE TRIGGER trg_prevent_delete_sensitive
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/

INSERT INTO sensitive_data (data_id, data_value) VALUES (1, 'Confidential Info');


DELETE FROM sensitive_data WHERE data_id = 1;
```
OUTPUT:


![Screenshot 2025-05-21 194820](https://github.com/user-attachments/assets/a3d199a7-617e-41ac-94b3-b8bb2bbe4ef8)


---
## 3. Write a trigger to automatically update a last_modified timestamp.

PROGRAM :

```
CREATE TABLE products (
    product_id     NUMBER PRIMARY KEY,
    product_name   VARCHAR2(100),
    price          NUMBER(10, 2),
    quantity       NUMBER
);

INSERT INTO products (product_id, product_name, price, quantity)
VALUES (101, 'Laptop', 850.00, 10);

INSERT INTO products (product_id, product_name, price, quantity)
VALUES (102, 'Mouse', 25.50, 100);


CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSDATE;
END;
/
-- Update a product
UPDATE products
SET product_name = 'New Name'
WHERE product_id = 101;

-- Check the last_modified column
SELECT product_id, product_name, last_modified
FROM products
WHERE product_id = 101;
```
OUTPUT :


![Screenshot 2025-05-21 194831](https://github.com/user-attachments/assets/424e6737-4825-4706-aca5-ec5fc358ab67)


---

## 4. Write a trigger to keep track of the number of updates made to a table.

PROGRAM :

```
CREATE TABLE customer_orders (
    order_id     NUMBER PRIMARY KEY,
    customer_id  NUMBER,
    order_date   DATE,
    total_amount NUMBER
);
CREATE TABLE audit_log (
    table_name     VARCHAR2(50) PRIMARY KEY,
    update_count   NUMBER DEFAULT 0
);
INSERT INTO audit_log (table_name, update_count)
VALUES ('CUSTOMER_ORDERS', 0);
CREATE OR REPLACE TRIGGER trg_count_updates_customer_orders
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'CUSTOMER_ORDERS';
END;
/
-- Update a row in customer_orders
UPDATE customer_orders
SET total_amount = total_amount + 10
WHERE order_id = 1;

-- Check the update count
SELECT * FROM audit_log;
```

OUTPUT :



![Screenshot 2025-05-21 194843](https://github.com/user-attachments/assets/4e9dfd23-ffec-496a-95b3-991470c3a33c)



---

## 5. Write a trigger that checks a condition before allowing insertion into a table.

PROGRAM :

```
CREATE TABLE employee (
    emp_id     NUMBER PRIMARY KEY,
    emp_name   VARCHAR2(100),
    salary     NUMBER
);
CREATE OR REPLACE TRIGGER trg_check_min_salary
BEFORE INSERT ON employee
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/
INSERT INTO employee (emp_id, emp_name, salary)
VALUES (1, 'John Doe', 2500);

INSERT INTO employee (emp_id, emp_name, salary)
VALUES (2, 'Jane Smith', 4000);
```

OUTPUT :

![Screenshot 2025-05-21 194857](https://github.com/user-attachments/assets/1e90c93c-702d-40cc-a72d-e8ce022ad6ca)

---
## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
