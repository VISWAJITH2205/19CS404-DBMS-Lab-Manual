# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
 Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30
 Sample table: CUSTOMERS
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 1          Ramesh     32              Ahmedabad     2000
 2          Khilan        25              Delhi                 1500
 3          Kaushik      23              Kota                  2000
 4          Chaitali       25             Mumbai            6500
 5          Hardik        27              Bhopal              8500
 6          Komal         22              Hyderabad       4500
 7           Muffy          24              Indore            10000
 
 
For example:
 Result
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 2           Khilan      25          Delhi       1500
 3           Kaushik     23          Kota        2000
 4           Chaitali    25          Mumbai      6500
 5           Hardik      27          Bhopal      8500
 6           Komal       22          Hyderabad   4500
 7           Muffy       24          Indore      10000

```
SELECT * FROM CUSTOMERS WHERE AGE < 30;
```

**Output:**

![Screenshot 2025-05-18 174604](https://github.com/user-attachments/assets/f8707850-92ca-48f6-8c53-045b70a3b705)


**Question 2**
---
 Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage
 Table Name: Medications (attributes: medication_id, medication_name, dosage)
 For example:
 Result
 medic  medication_name  dosage-----  ---------------  --------------
2      Ibuprofen        200mg

```
SELECT medication_id AS medic, medication_name, dosage FROM Medications
 WHERE dosage = (SELECT MIN(dosage) FROM Medications);
```

**Output:**

![Screenshot 2025-05-18 174725](https://github.com/user-attachments/assets/05aff4bb-03bc-4745-a37f-82cca81aae92)


**Question 3**
---
 Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.
 Sample table: CUSTOMERS
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 1          Ramesh     32              Ahmedabad     2000
 2          Khilan        25              Delhi                 1500
 3          Kaushik      23              Kota                  2000
 4          Chaitali       25             Mumbai            6500
 5          Hardik        27              Bhopal              8500
 6          Komal         22              Hyderabad       4500
 7           Muffy          24              Indore            10000
 
 
For example:
 Result
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 4           Chaitali    25          Mumbai      6500
 5           Hardik      27          Bhopal      8500
 7           Muffy       24          Indore      10000

```
SELECT * FROM CUSTOMERS WHERE SALARY > 4500;
```

**Output:**

![Screenshot 2025-05-18 175010](https://github.com/user-attachments/assets/2164c22c-6217-4a91-8dfc-89881ebb2cf5)


**Question 4**
---
 Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the
 maximum grade achieved in each subject.
 Sample table: GRADES (attributes: student_id, student_name, subject, grade)
 For example:
 Result
 student_name     grade---------------  --------------
Charlie          95
 Emma             92
 John             85

```
SELECT student_name, grade FROM GRADES g
 WHERE grade = (SELECT MAX(grade) FROM GRADES WHERE subject = g.subject);
```

**Output:**

![Screenshot 2025-05-18 175127](https://github.com/user-attachments/assets/8662dff4-5c9a-4904-aa98-5f7a0441c73c)


**Question 5**
---
 Write a SQL query to Find employees who have an age less than the average age of employees with incomes over
 2.5 Lakh
 Employee Table
 name             type------------   --------------
id                    INTEGER
 name              TEXT
 age                 INTEGER
 city                 TEXT
 income           INTEGER
 For example:
 Result
 id     name             age              city             income-----  ---------------  ---------------  ---------------  ----------
 101    Peter            32               NewYork          200000
 102    Mark             32               California       300000
 103    Donald           25               Arizona          1000000
 104    Obama            35               Florida          5000000
 105    Linklon          32               Georgia          250000
 107    Adam             35               California       5000000

```
SELECT id, name, age, city, income FROM Employee
 WHERE age < (SELECT AVG(age) FROM Employee WHERE income > 250000);
```

**Output:**

![Screenshot 2025-05-18 175318](https://github.com/user-attachments/assets/f8e109da-d179-4fec-91a6-6425b977f2ef)


**Question 6**
---
 Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum
 grade achieved in each subject.
 Sample table: GRADES (attributes: student_id, student_name, subject, grade)
 For example:
 Result
 student_id       student_name     subject          grade---------------  ---------------  ---------------  --------------
2                Bob              Math             85
 6                Frank            Science          85
 7                John             Social           85

```
SELECT student_id, student_name, subject, grade FROM GRADES g
 WHERE grade = (SELECT MIN(grade) FROM GRADES WHERE subject = g.subject);
```

**Output:**

![Screenshot 2025-05-18 175430](https://github.com/user-attachments/assets/c3fc26f8-1590-4267-9cfc-c40a4520a6e1)


**Question 7**
---
 Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi
 Sample table: CUSTOMERS
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 1          Ramesh     32              Ahmedabad     2000
 2          Khilan        25              Delhi                 1500
 3          Kaushik      23              Kota                  2000
 4          Chaitali       25             Mumbai            6500
 5          Hardik        27              Bhopal              8500
 6          Komal         22              Hyderabad       4500
 7           Muffy          24              Indore            10000
 
 
For example:
 Result
 ID          NAME        AGE         ADDRESS     SALARY----------  ----------  ----------  ----------  ----------
 2           Khilan      25          Delhi       1500

```
SELECT * FROM CUSTOMERS
 WHERE ADDRESS = 'Delhi';
```

**Output:**

![Screenshot 2025-05-18 175817](https://github.com/user-attachments/assets/9e260d88-af76-46c6-b0b5-683888065924)


**Question 8**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade
 achieved in each subject.
 Sample table: GRADES (attributes: student_id, student_name, subject, grade)
 For example:
 Result
 student_id       student_name     subject          grade---------------  ---------------  ---------------  --------------
3                Charlie          Math             95
 5                Emma             Science          92
 7                John             Social           85

```
SELECT student_id, student_name, subject, grade FROM GRADES g
 WHERE grade = (SELECT MAX(grade) FROM GRADES WHERE subject = g.subject);
```

**Output:**

![Screenshot 2025-05-18 175933](https://github.com/user-attachments/assets/64f5c875-4df7-4ea2-9f53-4db259d6fcfc)


**Question 9**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

```
SELECT id,name,age,city,income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);
```

**Output:**

![Screenshot 2025-05-18 180051](https://github.com/user-attachments/assets/d5dd9404-6231-48c5-9ac2-7cd494f11f32)


**Question 10**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.
salesman table
name type
salesman_id numeric(5) name varchar(30) city varchar(15) commission decimal(5,2)
customer table
name type
customer_id int cust_name text city text grade int salesman_id int

```
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;
```

**Output:**

![Screenshot 2025-05-18 180231](https://github.com/user-attachments/assets/9fbf323f-f0ce-48ca-9c7c-1b2658db282b)

---

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
