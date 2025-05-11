# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### PROGRAM :
```
DECLARE
   num1 NUMBER := 25;  
   num2 NUMBER := 40;
   greatest NUMBER;
BEGIN
   IF num1 > num2 THEN
      greatest := num1;
   ELSE
      greatest := num2;
   END IF;

   DBMS_OUTPUT.PUT_LINE('The greatest number is: ' || greatest);
END;
/
```

### OUTPUT :

![Screenshot 2025-05-11 223223](https://github.com/user-attachments/assets/9abd2b59-9be7-4711-b4c3-df058f24a7d2)


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### PROGRAM :
```
DECLARE
   N         NUMBER := 10; 
   counter   NUMBER := 1;
   sum       NUMBER := 0;
BEGIN
   WHILE counter <= N LOOP
      sum := sum + counter;
      counter := counter + 1;
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Sum of first ' || N || ' natural numbers is: ' || sum);
END;
/
```

### OUTPUT :

![Screenshot 2025-05-11 223753](https://github.com/user-attachments/assets/ba565639-b1ce-473f-8fed-7dfb5a4ab412)


---

## 3. Write a PL/SQL program to generate Fibonacci series

### PROGRAM :
```
DECLARE
   n        NUMBER := 10;  
   a        NUMBER := 0;
   b        NUMBER := 1;
   c        NUMBER;
   counter  NUMBER := 1;
BEGIN
   DBMS_OUTPUT.PUT_LINE('Fibonacci Series:');
   WHILE counter <= n LOOP
      DBMS_OUTPUT.PUT_LINE(a);
      c := a + b;
      a := b;
      b := c;
      counter := counter + 1;
   END LOOP;
END;
/

```

### OUTPUT :

![Screenshot 2025-05-11 224002](https://github.com/user-attachments/assets/002fb3d9-f110-4f66-ab5c-a955a261728e)


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### PROGRAM :
```
DECLARE
    original_number NUMBER := 12345; 
    reversed_number NUMBER := 0;
    remainder NUMBER;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Original Number: ' || original_number);
    
    WHILE original_number > 0 LOOP
        remainder := MOD(original_number, 10);
        reversed_number := (reversed_number * 10) + remainder;
        original_number := TRUNC(original_number / 10);
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Reversed Number: ' || reversed_number);
END;
/
```

### OUTPUT :

![Screenshot 2025-05-11 224203](https://github.com/user-attachments/assets/5a5cf377-0c9c-4921-9531-6efe55c20f41)


---

## 5. Write a PL/SQL program to find the largest of three numbers

### PROGRAM :
```
DECLARE
   num1 NUMBER := 25;  
   num2 NUMBER := 42;
   num3 NUMBER := 17;
   largest NUMBER;
BEGIN
   IF num1 >= num2 AND num1 >= num3 THEN
      largest := num1;
   ELSIF num2 >= num1 AND num2 >= num3 THEN
      largest := num2;
   ELSE
      largest := num3;
   END IF;

   DBMS_OUTPUT.PUT_LINE('The largest number is: ' || largest);
END;
/
```

### OUTPUT :

![Screenshot 2025-05-11 224504](https://github.com/user-attachments/assets/0642279c-cc51-4ce7-8af6-46193a9ff207)


---

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
