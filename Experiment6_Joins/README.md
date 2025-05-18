# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:

ATTRIBUTES - nurse_id, first_name, last_name, department_id



DEPARTMENTS TABLE:

ATTRIBUTES - department_id, department_name



For example:

Result
nurse_id         first_name       last_name        department_id    department_name
---------------  ---------------  ---------------  ---------------  ---------------
1                Emma             Taylor           1                Cardiology
2                David            Moore            2                Orthopedics
3                Sophia           Clark            3                Pediatrics

```
SELECT n.*, d.department_name FROM nurses n
INNER JOIN departments d ON n.department_id = d.department_id;
```

**Output:**

![Screenshot 2025-05-18 181342](https://github.com/user-attachments/assets/538e4991-fc11-4a58-87d6-3d2394cde2f3)


**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

For example:

Result
first_name       surgery_id       patient_id       surgeon_id       surgery_date
---------------  ---------------  ---------------  ---------------  ------------
Bob              2                2                2                2024-02-28

```
SELECT p.first_name, s.* FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id WHERE p.date_of_birth > '1990-01-01';

```

**Output:**

![Screenshot 2025-05-18 181513](https://github.com/user-attachments/assets/c440fc5b-4227-4bba-89bf-a4e678a26ac9)


**Question 3**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

CUSTOMER TABLE:



ORDERS TABLE:



For example:

Result
cust_name
---------------
Nick Rimando
Jozy Altidore

```
SELECT DISTINCT c.cust_name
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.purch_amt < 100;
```

**Output:**

![Screenshot 2025-05-18 181724](https://github.com/user-attachments/assets/5e43b786-1f25-4a6a-8912-d85ab520b139)


**Question 4**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
For example:

Result
ord_no           purch_amt        cust_name        city
---------------  ---------------  ---------------  ---------------
70007            948.5            Graham Zusi      California
70010            1983.43          Fabian Johns     Paris

```
SELECT o.ord_no, o.purch_amt, c.cust_name, c.city
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

![Screenshot 2025-05-18 181843](https://github.com/user-attachments/assets/539261b3-68e8-41cd-aaf5-2ea727c602fa)


**Question 5**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Brad Guzan       London           Pit Alex         0.11
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Geoff Cameron    Berlin           Lauson Hen       0.12
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13

```
SELECT c.cust_name AS "Customer Name", c.city AS "city", s.name AS "Salesman", s.commission FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

![Screenshot 2025-05-18 181954](https://github.com/user-attachments/assets/fd886163-9290-40f0-962c-336d3ba9309c)


**Question 6**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

For example:

Result
cust_name        city             ord_no           ord_date         Order Amount  name        commission
---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------
Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13
        

```
SELECT c.cust_name, c.city, o.ord_no, o.ord_date, o.purch_amt AS "Order Amount", s.name, s.commission 
FROM customer c LEFT JOIN orders o ON c.customer_id = o.customer_id
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

![Screenshot 2025-05-18 182159](https://github.com/user-attachments/assets/9a53232a-d444-4ec4-8c06-8770d0d73574)


**Question 7**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table : salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
ord_no           purch_amt        ord_date         cust_name        customer_city  grade       salesman_name  salesman_city  commission
---------------  ---------------  ---------------  ---------------  -------------  ----------  -------------  -------------  ----------
70001            150.5            2012-10-05       Graham Zusi      California     200         Nail Knite     Paris          0.13
70009            270.65           2012-09-10       Brad Guzan       London         100         Pit Alex       London         0.11
70002            65.26            2012-10-05       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
70004            110.5            2012-08-17       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
70007            948.5            2012-09-10       Graham Zusi      California     200         Nail Knite     Paris          0.13
70005            2400.6           2012-07-27       Brad Davis       New York       200         Bob Emily      New York       0.15
70008            5760.0           2012-09-10       Nick Rimando     Chennai        100         Bob Emily      New York       0.15
70010            1983.43          2012-10-10       Fabian Johns     Paris          300         Mc Lyon        Paris          0.14
70003            2480.4           2012-10-10       Geoff Cameron    Berlin         100         Lauson Hen     San Jose       0.12
70012            250.45           2012-06-27       Julian Green     London         300         Nail Knite     Paris          0.13
70011            75.29            2012-08-17       Jozy Altidore    Moscow         200         Paul Adam      Rome           0.13
70013            3045.6           2012-04-25       Nick Rimando     Chennai        100         Bob Emily      New York       0.15

```
SELECT o.ord_no, o.purch_amt, o.ord_date, c.cust_name, c.city AS customer_city, c.grade, s.name AS salesman_name, s.city AS salesman_city, s.commission
FROM orders o JOIN customer c ON o.customer_id = c.customer_id
JOIN salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

![Screenshot 2025-05-18 182420](https://github.com/user-attachments/assets/a0e03158-7fc8-46fd-921d-3e15b632bc2d)


**Question 8**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column.

Customer Table:



Salesmen Table:

 

For example:

Result
name             cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
Bob Emily        Brad Davis       New York         200              5001
Bob Emily        Nick Rimando     Chennai          100              5001
Nail Knite       Graham Zusi      California       200              5002
Nail Knite       Julian Green     London           300              5002
Pit Alex         Brad Guzan       London           100              5005
Mc Lyon          Fabian Johns     Paris            300              5006
Paul Adam        Jozy Altidore    Moscow           200              5007
Lauson Hen       Geoff Cameron    Berlin           100              5003

```
SELECT s.name, c.cust_name, c.city, c.grade, c.salesman_id FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id;
```

**Output:**

![Screenshot 2025-05-18 182559](https://github.com/user-attachments/assets/58e735dd-edfd-47c0-ae04-1db06cfeb2c8)


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date



For example:

Result
patient_name     test_name
---------------  ---------------
Alice            Blood Pressure
Bob              X-Ray
Charlie          Blood Test

```
SELECT p.first_name AS patient_name, t.test_name FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id;
```

**Output:**

![Screenshot 2025-05-18 182707](https://github.com/user-attachments/assets/1f64e504-52c7-4ef7-934b-0aaf442c1d11)


**Question 10**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13

```
SELECT c.cust_name AS "Customer Name", c.city AS "city", s.name AS "Salesman", s.commission FROM customer c JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

![Screenshot 2025-05-18 182815](https://github.com/user-attachments/assets/e90f1422-dca6-4d81-a990-31602eb7291b)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
