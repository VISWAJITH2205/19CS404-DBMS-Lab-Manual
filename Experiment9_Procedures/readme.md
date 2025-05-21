# Experiment 9: PL/SQL – Procedures and Functions
---
## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

---
### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

---

## 1. Write a PL/SQL Procedure to Find the Square of a Number

**Program:**
```
CREATE OR REPLACE PROCEDURE find_square (num IN NUMBER)
IS
   result NUMBER;
BEGIN
   result := num * num;
   DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || result);
END;
```
```
EXEC find_square(6);
```
OUTPUT :


![Screenshot 2025-05-21 192228](https://github.com/user-attachments/assets/b7c4a569-d4eb-43e1-9983-17c51c14336e)


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

**Program:**
```
CREATE OR REPLACE FUNCTION get_factorial (n IN NUMBER)
RETURN NUMBER
IS
   fact NUMBER := 1;
BEGIN
   FOR i IN 1..n LOOP
      fact := fact * i;
   END LOOP;
   RETURN fact;
END;
```

```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
```
OUTPUT :


![Screenshot 2025-05-21 192243](https://github.com/user-attachments/assets/64fca316-d316-4925-b5d4-2c74a40b702b)


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

**Program:**
```
CREATE OR REPLACE PROCEDURE check_even_odd (n IN NUMBER)
IS
BEGIN
   IF MOD(n, 2) = 0 THEN
      DBMS_OUTPUT.PUT_LINE(n || ' is Even');
   ELSE
      DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
   END IF;
END;
```

```
EXEC check_even_odd(12);
```
OUTPUT :


![Screenshot 2025-05-21 192303](https://github.com/user-attachments/assets/98be3fe4-f60a-4fa9-b458-f32a90f0bda8)


---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

**Program:**
```
CREATE OR REPLACE FUNCTION reverse_number (n IN NUMBER)
RETURN NUMBER
IS
   rev NUMBER := 0;
   temp NUMBER := n;
BEGIN
   WHILE temp > 0 LOOP
      rev := rev * 10 + MOD(temp, 10);
      temp := TRUNC(temp / 10);
   END LOOP;
   RETURN rev;
END;
```
```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || reverse_number(1234));
END;
```
OUTPUT :


![Screenshot 2025-05-21 192322](https://github.com/user-attachments/assets/002ce86a-bae2-4cf9-af19-02674fc07dc8)


---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

**Program:**
```
CREATE OR REPLACE PROCEDURE print_table (n IN NUMBER)
IS
BEGIN
   DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || n || ':');
   FOR i IN 1..10 LOOP
      DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
   END LOOP;
END;
```
```
EXEC print_table(5);
```
OUTPUT :


![Screenshot 2025-05-21 192623](https://github.com/user-attachments/assets/dcd78ec8-44c3-428b-b6f8-0eacdede00f3)


---

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
