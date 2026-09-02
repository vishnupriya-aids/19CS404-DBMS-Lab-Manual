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
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2


```sql
SELECT
     SUBSTR(ValidityPeriod,1,4)AS ValidityYear,
     COUNT(DISTINCT PatientID) AS TotalPatients
FROM
     Insurance
GROUP BY
     ValidityPeriod
ORDER BY
     ValidityYear;
```

**Output:**

<img width="647" height="371" alt="image" src="https://github.com/user-attachments/assets/6b726ad9-e367-4f47-8377-5e0952702451" />


**Question 2**
---
How many medical records does each doctor have?

Sample table:MedicalRecords Table



For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3


```sql
SELECT
      DoctorID,
      COUNT(RecordID) AS TotalRecords
FROM
      MedicalRecords
GROUP BY 
      DoctorID
ORDER BY
      DoctorID;
```

**Output:**

<img width="590" height="615" alt="image" src="https://github.com/user-attachments/assets/a5e11dbb-d4d5-4cc0-ab00-b57537a0d40b" />


**Question 3**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table



For example:

Result
Diagnosis              DiagnosisCount
---------------------  --------------
Childhood vaccination  3


```sql
SELECT
      Diagnosis,
      COUNT(*) AS DiagnosisCount
FROM
     MedicalRecords
GROUP BY
     Diagnosis
ORDER BY
     DiagnosisCount DESC
LIMIT 1;
```

**Output:**

<img width="825" height="300" alt="image" src="https://github.com/user-attachments/assets/d07cacba-6c18-43be-8ff3-a2286ddde1ac" />


**Question 4**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26


```sql
SELECT
     MIN(purch_amt) AS MINIMUM
FROM
     orders;
```

**Output:**

<img width="338" height="298" alt="image" src="https://github.com/user-attachments/assets/40f4c089-8ea3-4d73-ab0d-64ccbf8a7aba" />


**Question 5**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
5


```sql
SELECT
     COUNT(*) AS COUNT
FROM
     employee
WHERE
     age > 32;
```

**Output:**

<img width="347" height="295" alt="image" src="https://github.com/user-attachments/assets/f296f3ad-db2e-4f71-897f-849b8ae345e8" />


**Question 6**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4


```sql
SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="332" height="297" alt="image" src="https://github.com/user-attachments/assets/0d9b2d98-9b65-4ba7-b805-066b60aaa1d1" />


**Question 7**
---
Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name          length
------------  ----------
Preeti Patel  12


```sql
SELECT name, LENGTH(name) AS length
FROM customer
ORDER BY LENGTH(name) DESC
LIMIT 1;

```

**Output:**

<img width="660" height="285" alt="image" src="https://github.com/user-attachments/assets/75cb8f22-9ba1-4207-913e-e18a54d87af4" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
SELECT address, SUM(salary)
FROM customer1
GROUP BY address
HAVING SUM(salary) > 2000;
```

**Output:**


<img width="582" height="472" alt="image" src="https://github.com/user-attachments/assets/822c51e8-0817-4839-a725-e4d00f6a088a" />


**Question 9**
---
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT
For example:

Result
PatientID   TotalRecords
----------  ------------
1           4


```sql
SELECT PatientID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*) > 3;
```

**Output:**


<img width="567" height="312" alt="image" src="https://github.com/user-attachments/assets/015a5df2-5c70-4901-8c66-d6c08c89cac3" />


**Question 10**
---
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products



For example:

Result
category_id  Total_Cost
-----------  ----------
2            63


```sql
SELECT category_id, SUM(price) AS Total_Cost
FROM products
GROUP BY category_id
HAVING SUM(price) > 50;
```

**Output:**

<img width="587" height="315" alt="image" src="https://github.com/user-attachments/assets/5e49f084-01e5-4c05-bdee-46851364c627" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
