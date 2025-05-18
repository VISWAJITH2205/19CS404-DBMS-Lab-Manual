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
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.
 Sample table: orders
 ord_no      purch_amt   ord_date    customer_id  salesman_id----------  ----------  ----------  -----------  ----------
70001       150.5       2012-10-05  3005         5002
 70009       270.65      2012-09-10  3001         5005
 70002       65.26       2012-10-05  3002         5001
 
For example:
 Result
 COUNT----------
 6

```
SELECT COUNT(DISTINCT salesman_id)
 AS COUNT FROM orders;
```

**Output:**

![Screenshot 2025-05-18 170901](https://github.com/user-attachments/assets/42a9020f-6f7d-4ca1-ac80-e4343238ea95)


**Question 2**
---
 Write a SQL query to find the average length of email addresses (in characters):
 Table: customer
 name        type----------  ----------
 id          INTEGER
 name        TEXT
 city        TEXT
 email       TEXT
 phone       INTEGER
 For example:
 Result
 avg_email_length----------------
 15.0

```
SELECT AVG(LENGTH(email)) AS 
avg_email_length
 FROM customer;
```

**Output:**

![Screenshot 2025-05-18 171255](https://github.com/user-attachments/assets/96aaba11-f43b-4e02-bf9f-e2ee856aab25)


**Question 3**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?
 Table: fruits
 name        type----------  ----------
 id          INTEGER
 name        TEXT
 unit        TEXT
 inventory   INTEGER
 price       REAL
 
For example:
 Result
 price_diff----------
 4.65


```
SELECT MAX(price) - MIN(price) AS price_diff FROM fruits;
```

**Output:**

![Screenshot 2025-05-18 171509](https://github.com/user-attachments/assets/70d434de-1719-4329-9d63-f0689655f06b)


**Question 4**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price
 and category ID as Revenue for each category from the "products" table, and includes only those products
 where the total revenue is greater than 25.
 Sample table: products
 For example:
 Result
 category_id  Revenue-----------  ----------
 1            49.5
 2            126
 3            79.44

```
SELECT category_id, SUM(price * category_id) AS Revenue FROM products
 GROUP BY category_id
 HAVING SUM(price * category_id) > 25;
```

**Output:**

![Screenshot 2025-05-18 172115](https://github.com/user-attachments/assets/adf74419-0e66-4b86-b86f-266377e9f062)


**Question 5**
---
 How many medical records were created in each month?
 Sample table:MedicalRecords Table
 For example:
 Result
 Month       TotalRecords----------  ------------
 2023-12     2
 2024-01     6
 2024-02     2

```
SELECT strftime('%Y-%m', Date) AS Month, 
COUNT(*) AS TotalRecords FROM MedicalRecords
 GROUP BY MONTH
 ORDER BY MONTH;
```

**Output:**

![Screenshot 2025-05-18 172240](https://github.com/user-attachments/assets/ac214b38-11f3-4271-9907-fa1aff463e82)


**Question 6**
---
 What is the average dosage prescribed for each medication?
 Sample tablePrescriptions Table
 For example:
 Result
 Medication     AvgDosage-------------  ----------
 Ciprofloxacin  500.0
 Doxorubicin    60.0
 Ibuprofen      400.0
 Levothyroxine  50.0
 Lisinopril     10.0
 MMR            0.5
 Pending        0.0
 Prenatal vita  1.0
 Sertraline     50.0
 Topiramate     25.0

```
SELECT Medication, AVG(CAST(SUBSTR(Dosage, 1, LENGTH(Dosage) - 2) AS REAL)) AS AvgDosage FROM Prescriptions
GROUP BY Medication
 ORDER BY Medication;
```

**Output:**

![Screenshot 2025-05-18 172459](https://github.com/user-attachments/assets/f8175262-2ae7-4100-b7e1-43db2286aad1)


**Question 7**
---
 How many doctors specialize in each medical specialty?
 Sample table:Doctors Table
 For example:
 Result
 Specialty          TotalDocto-----------------  ----------
 Gastroenterology   1
 Neurology          1
 Obstetrics         3
 Ophthalmology      1
 Orthopedics        1
 Pediatrics         2
 Urology            1
 

```
SELECT Specialty, COUNT(*) AS TotalDoctors FROM Doctors 
GROUP BY Specialty
 ORDER BY Specialty;
```

**Output:**

![Screenshot 2025-05-18 172625](https://github.com/user-attachments/assets/d41ca5a0-539d-4dd6-83b3-67b20183f053)


**Question 8**
---
What is the most common diagnosis among patients?
 Sample table:MedicalRecords Table
 For example:
 Result
 Diagnosis              DiagnosisCount---------------------  --------------
 Childhood vaccination  3
 

```
SELECT Diagnosis, COUNT(*) AS DiagnosisCount FROM MedicalRecords
 GROUP BY Diagnosis ORDER BY DiagnosisCount DESC LIMIT 1;
```

**Output:**

![Screenshot 2025-05-18 173039](https://github.com/user-attachments/assets/d1d3a977-2615-46b5-911a-86016c8bc06e)


**Question 9**
---
 How many appointments are scheduled in each hour of the day?
 Sample table:Appointments Table
 name                              type--------------------          ----------
 AppointmentID               INTEGER
 PatientID                         INTEGER
 DoctorID                         INTEGER
 AppointmentDateTime   DATETIME
 Purpose                           TEXT
 Status                              TEXT     
For example:
 Result
 HourOfDay   TotalAppointments----------  ----------------
09          2
 10          5
 11          1
 14          1
 16          1

```
SELECT STRFTIME('%H', AppointmentDateTime) AS HourOfDay, COUNT(*) AS TotalAppointments
 FROM Appointments
 GROUP BY HourOfDay;
```

**Output:**

![Screenshot 2025-05-18 173216](https://github.com/user-attachments/assets/21eb183a-73aa-4830-b40f-e3a7e255a954)


**Question 10**
---
 Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city
 Table: customer
 name        type----------  ----------
 id          INTEGER
 name        TEXT   
city        TEXT
 email       TEXT
 phone       INTEGER
 For example:
 Result
 avg_email_length_below_30------------------------
14.0

```
SELECT AVG(LENGTH(email)) AS avg_email_length_below_30 
FROM customer WHERE city = 'Mumbai';
```

**Output:**

![Screenshot 2025-05-18 173347](https://github.com/user-attachments/assets/67325c9b-8cc6-49e9-b996-5f01441c20cf)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
