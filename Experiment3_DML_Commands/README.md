# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
UPDATE products
SET sell_price = sell_price * 1.10
WHERE category = 'Bakery';
```

**Output:**

<img width="1200" height="527" alt="image" src="https://github.com/user-attachments/assets/5cadd397-c1f1-49d7-b12e-7b94bdfa8da7" />


**Question 2**
---
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
 

For example:

Test	Result
select changes();
changes()
----------
3


```sql
UPDATE products
SET reorder_lvl = reorder_lvl * 0.70
WHERE product_name LIKE '%cream%'
  AND quantity > reorder_lvl;
```

**Output:**

<img width="1182" height="477" alt="image" src="https://github.com/user-attachments/assets/d49a5ed1-e7ad-481a-9d6c-f0eccb53a754" />


**Question 3**
---
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
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

Test	Result
SELECT * FROM EMPLOYEES WHERE DEPARTMENT_ID=80 AND COMMISSION_PCT=.25;
EMPLOYEE_ID  FIRST_NAME  LAST_NAME   EMAIL       PHONE_NUMBER        HIRE_DATE   JOB_ID      SALARY      COMMISSION_PCT  MANAGER_ID  DEPARTMENT_ID
-----------  ----------  ----------  ----------  ------------------  ----------  ----------  ----------  --------------  ----------  -------------
151          John        Bernstein   DBERNSTE    011.44.1344.345268  8/7/87      SA_REP      9500        0.25            145         80
152          John        Hall        PHALL       011.44.1344.478968  8/8/87      SA_REP      9000        0.25            145         80
161          John        Sewall      SSEWALL     011.44.1345.529268  8/17/87     SA_REP      7000        0.25            146         80
162          John        Vishney     CVISHNEY    011.44.1346.129268  8/18/87     SA_REP      10500       0.25            147         80
168          John        Ozer        LOZER       011.44.1343.929268  8/24/87     SA_REP      11500       0.25            148         80
175          John        Hutton      AHUTTON     011.44.1644.429266  8/3

```sql
UPDATE employees
SET first_name = 'John'
WHERE department_id = 80
  AND commission_pct < 0.35;
```

**Output:**

<img width="1178" height="545" alt="image" src="https://github.com/user-attachments/assets/da6fd14b-d452-492c-a2c4-0198d90981c0" />


**Question 4**
---
Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
3


```sql
UPDATE sales
SET total_sell_price = quantity * sell_price
WHERE product_id = 10;
```

**Output:**

<img width="1197" height="480" alt="image" src="https://github.com/user-attachments/assets/09023997-fc3c-4603-8d06-1cb46516ba64" />


**Question 5**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
For example:

Test	Result
select changes();
changes()
-----------------
4


```sql
UPDATE products
SET reorder_lvl = 40
WHERE category = 'Grocery';
```

**Output:**

<img width="1193" height="390" alt="image" src="https://github.com/user-attachments/assets/0a9a60fd-3298-481b-bc30-d24961c75c04" />


**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
3


```sql
DELETE FROM customer
WHERE grade <> 3;
```

**Output:**

<img width="670" height="526" alt="image" src="https://github.com/user-attachments/assets/0c3e89b7-52ec-48c4-a54e-baa3518b2ed7" />


**Question 7**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28


```sql
DELETE FROM surgeries
WHERE surgery_id = 3;
```

**Output:**
<img width="1192" height="375" alt="image" src="https://github.com/user-attachments/assets/339c0718-f3b2-4991-a0ba-2750835f70d2" />


**Question 8**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM doctors
WHERE specialization IS NULL;
```

**Output:**

<img width="1183" height="612" alt="image" src="https://github.com/user-attachments/assets/aee4f021-a2e3-4fb8-bad0-f594faacea62" />


**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00001      Micheal     New York    New York      USA           2           3000         5000         2000         6000             CCCCCCC     A008
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00002      Bolt        New York    New York      USA           3           5000         7000         9000         3000             DDNRDRH     A008
changes()
----------
3


```sql
DELETE FROM customer
WHERE WORKING_AREA = 'New York';
```

**Output:**

<img width="1182" height="821" alt="image" src="https://github.com/user-attachments/assets/e6835c67-85ad-4ffb-a93a-46c39e5ed710" />


**Question 10**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_COUNTRY' is neither 'India' nor 'USA'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
11


```sql
DELETE FROM customer
WHERE CUST_COUNTRY NOT IN ('India','USA');
```

**Output:**

<img width="1186" height="548" alt="image" src="https://github.com/user-attachments/assets/fc4586fc-e916-4875-8a60-4465a1cf3c58" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
