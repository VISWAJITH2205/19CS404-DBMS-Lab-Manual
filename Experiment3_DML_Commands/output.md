**Question 1**
--
Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.
 Products table--------------
product_id
 product_name
 category
 cost_price
 sell_price
 reorder_lvl
 quantity
 supplier_id

```
UPDATE Products 
SET product_name = 'Premium Bread'
 WHERE product_id = 5;
```

**Output:**

![Screenshot 2025-05-18 082434](https://github.com/user-attachments/assets/bb45f7c9-b0e0-4166-b810-96a6a05d085d)


**Question 2**
---
 Write a SQL query to remove rows from the table 'customer' with the following condition 
1. 'cust_country' must be 'India',
 2. 'cus_city' must not be 'Chennai',
 Sample table: Customer
 +-----------+-------------+-------------+--------------+--------------+-------+-------------+------------
+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT 
| PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     
| AGENT_CODE |
 +-----------+-------------+-------------+--------------+--------------+-------+-------------+------------
+-------------+---------------+--------------+------------+
 | C00013    
| Holmes      
|     
7000.00 |       
| C00001    
|     
| Micheal     
2000.00 |       
| C00020    
|     
| London      
4000.00 | BBBBBBB      
| London       
| New York    
6000.00 | CCCCCCC      
| Albert      
6000.00 |       
For example:
 | New York    
6000.00 | BBBBSBB      
| UK           
| A003       
| New York     
| A008       
| New York     
| A008       
|
 | USA          
|
 | USA          
|
 |     
|     
|     
2 |     
2 |     
3 |     
6000.00 |     
3000.00 |     
5000.00 |     
5000.00 
5000.00 
7000.00 


```
DELETE FROM customer 
WHERE cust_country = 'India' AND cust_city <> 'Chennai';
```

**Output:**

![Screenshot 2025-05-18 083129](https://github.com/user-attachments/assets/2fae494a-23dc-4290-bca6-bdb7cefc2fb7)
![Screenshot 2025-05-18 083152](https://github.com/user-attachments/assets/5e29e8d0-dba7-4964-83e4-d0b9b659b7f7)
![Screenshot 2025-05-18 083216](https://github.com/user-attachments/assets/cb1b1713-3a5e-472d-bc8f-e14432bb30da)


**Question 3**
---
 Write a query to get information of Employees from EmployeeInfo1 table where the Employee is not assigned to
 any department.
 EmpID EmpFname EmpLname Department Project Address DOB Gender
 1 Sanjay Mehra HR P1 Hyderabad(HYD) 01/12/1976M
 2 Ananya Mishra Admin P2 Delhi(DEL) 02/05/1968 F
 
For example:
 Result
 EmpID       EmpFname    EmpLname    Department  Project     Address         DOB         Gender----------  ----------  ----------  ----------  ----------  --------------  ----------  ----------
 6           Vijay       Mehra                   P1          Hyderabad(HYD)  1976-12-01  M

```
SELECT * FROM EmployeeInfo1
 WHERE Department IS NULL;
```

**Output:**

![Screenshot 2025-05-18 083624](https://github.com/user-attachments/assets/698b906a-6520-473f-9a86-50a2a1c3bd7a)


**Question 4**
---
 Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.
 Employees table--------------
employee_id
 first_name
 last_name
 email
 phone_number
 hire_date
 job_id
 salary
 commission_pct
 manager_id
 department_id
 For example:
 Test Result
 SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE FROM EMPLOYEES 
WHERE DEPARTMENT_ID=50 LIMIT 3;
 EMPLOYEE_ID  FIRST_NAME  HIRE_DATE-----------  ----------  ----------
 120          Matthew     2024-01-24
 121          Adam        2024-01-24
 122          Payam       2024-01-24

```
 UPDATE Employees SET hire_date = '2024-01-24'
 WHERE department_id = 50;
```

**Output:**

![Screenshot 2025-05-18 084209](https://github.com/user-attachments/assets/8289b231-123e-4b0a-82e3-98353b969403)


**Question 5**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'
 Sample table: Doctors
 attributes : doctor_id, first_name, last_name, specialization

```
DELETE FROM Doctors
 WHERE specialization = 'Cardiology';
```

**Output:**

![Screenshot 2025-05-18 084540](https://github.com/user-attachments/assets/f993528c-5205-48b3-b2c7-f846049a95e7)


**Question 6**
---
 Write a SQL query to Select all patients who were admitted during the year 2023.
 Table: Patients
 name                  type--------------------  ----------
 patient_id            INT
 first_name            VARCHAR(50)
 last_name             VARCHAR(50)
 date_of_birth         DATE
 admission_date        DATE
 discharge_date        DATE
 doctor_id             INT
 For example:
 Result
 patient_id  first_name  admission_date----------  ----------  --------------
 4           Abhishek    2023-02-10
 5           Alice       2023-08-02

```
SELECT patient_id, first_name, admission_date FROM Patients 
WHERE strftime('%Y', admission_date) = '2023';
```

**Output:**

![Screenshot 2025-05-18 084852](https://github.com/user-attachments/assets/6c233882-f038-4535-9518-18820be70ad7)


**Question 7**
---
Write a SQL query to find all employees who were hired in the year 2022 from emp table.
 cid         name        type        ----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
 2           job         VARCHAR(50)
 3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         
For example:
 Result
 empno       ename       job         mgr         hiredate    sal         comm        deptno  ----------  ----------   -------    ------     -----------   -----      -----      -------    
 7369        SMITH       CLERK       7902        2022-08-22  800                     20
 7499        ALLEN       SALESMAN    7698        2022-08-22  1600        300         30
 7521        WARD        SALESMAN    7698        2022-08-22  1250        500         30
 7900        JAMES       CLERK       7698        2022-08-22  950                     30
 7902        FORD        ANALYST     7566        2022-08-22  3000                    20
 7934        MILLER      CLERK       7782        2022-08-22  1300                    10

```
SELECT * FROM emp 
WHERE strftime('%Y', hiredate) = '2022';
```

**Output:**

![Screenshot 2025-05-18 085219](https://github.com/user-attachments/assets/5abb15d2-fb8c-4975-b939-e9ecfecc2598)


**Question 8**
---
 Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the
 products table.
 Products Table 
name          ----------    
product_id     
product_name   
category       
cost_price     
sell_price     
reorder_lvl    
quantity       
supplier_id    
type       ---------- 
INT PRIMARY KEY        
VARCHAR(10) 
VARCHAR(50) 
DECIMAL(10) 
DECIMAL(10) 
INT        
INT        
INT               
For example:
 Test--pragma table_info('products');
 select changes();
 Result
 changes()----------
 2

```
UPDATE Products
 SET reorder_lvl = reorder_lvl * 0.7
 WHERE cost_price > 50 AND quantity < 100;
```

**Output:**

![Screenshot 2025-05-18 090001](https://github.com/user-attachments/assets/95c6bbfc-6f41-4f4f-a5ce-6ad15e1a96d2)
![Screenshot 2025-05-18 090011](https://github.com/user-attachments/assets/ecfd3ddb-0bc3-4257-b4da-2a8fdb900b0c)


**Question 9**
---
 Write a SQL statement to double the availability of the product with product_id 1.
 products table--------------
product_id
 product_name
 category_id
 availability

```
UPDATE products
 SET availability = availability * 2
 WHERE product_id = 1;
```

**Output:**

![Screenshot 2025-05-18 090614](https://github.com/user-attachments/assets/456c596e-a56c-41c1-92dd-8c50bb76e16e)


**Question 10**
---
 Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.
 Sample table: Surgeries
 attributes: surgery_id, patient_id, surgeon_id, surgery_date

```
DELETE FROM surgeries
 WHERE surgery_date = '2024-02-28';
```

**Output:**

![Screenshot 2025-05-18 091005](https://github.com/user-attachments/assets/3b1ae9f7-1ff1-4196-94ed-2de01513cd26)

