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
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
2                Bob              Math             85
6                Frank            Science          85
7                John             Social           85

```sql
SELECT *
FROM Grades g
WHERE g.grade = (
    SELECT MIN(g2.grade)
    FROM Grades g2
    WHERE g2.subject = g.subject
);
```

**Output:**

<img width="1241" height="472" alt="image" src="https://github.com/user-attachments/assets/c29ba13f-ebd3-42c4-b3ab-20eeb0c188d7" />


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
3           Kaushik     23          Kota        2000
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
6           Komal       22          Hyderabad   4500
7           Muffy       24          Indore      10000


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="1198" height="628" alt="image" src="https://github.com/user-attachments/assets/dba89b54-185a-4d90-bd27-b27a2794f08b" />


**Question 3**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85

```sql
SELECT *
FROM Grades g
WHERE g.grade = (
    SELECT MAX(g2.grade)
    FROM Grades g2
    WHERE g2.subject = g.subject
);
```

**Output:**

<img width="1273" height="490" alt="image" src="https://github.com/user-attachments/assets/578f401f-c2c9-410a-920d-498b6dab734f" />


**Question 4**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301


```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1236" height="467" alt="image" src="https://github.com/user-attachments/assets/02aae27a-9841-45e3-8a29-e0f2ab5c5160" />


**Question 5**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85


```sql
SELECT student_name, grade
FROM Grades g
WHERE g.grade = (
    SELECT MIN(g2.grade)
    FROM Grades g2
    WHERE g2.subject = g.subject
);
```

**Output:**

<img width="747" height="458" alt="image" src="https://github.com/user-attachments/assets/7a85717d-a066-4033-925f-66f755449111" />


**Question 6**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    salesman_id
----------  ----------  ----------  -----------
70002       65.26       2012-10-05  5001
70005       2400.6      2012-07-27  5001
70008       5760.0      2012-09-10  5001
70013       3045.6      2012-04-25  5001


```sql
SELECT o.ord_no,
       o.purch_amt,
       o.ord_date,
       o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.commission = (
    SELECT MAX(commission)
    FROM salesman
);
```

**Output:**

<img width="1017" height="507" alt="image" src="https://github.com/user-attachments/assets/5ef6a1c7-bb65-41fa-aa9b-438c42227be2" />


**Question 7**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name   city
-----  ---------------
Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh


```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="562" height="482" alt="image" src="https://github.com/user-attachments/assets/fa26c83f-4b7f-43c2-991e-9dcf0cbef484" />


**Question 8**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
105    Linklon          32               Georgia          250000


```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**

<img width="1243" height="460" alt="image" src="https://github.com/user-attachments/assets/f902b95b-b886-420d-bb1a-896424eba51e" />


**Question 9**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
 

For example:

Result
customer_id  cust_name    city        grade       salesman_id
-----------  -----------  ----------  ----------  -----------
3005         Graham Zusi  California  200         5002


```sql
SELECT *
FROM customer
WHERE customer_id = (
    SELECT salesman_id
    FROM salesman
    WHERE name = 'Mc Lyon'
) - 2001;
```

**Output:**

<img width="1242" height="347" alt="image" src="https://github.com/user-attachments/assets/1b9a9a7d-5f73-41bf-9d74-0d08ae421d35" />


**Question 10**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70002       65.26       2012-10-05  3002         5001
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70013       3045.6      2012-04-25  3002         5001


```sql
SELECT o.ord_no,
       o.purch_amt,
       o.ord_date,
       o.customer_id,
       o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**

<img width="1247" height="517" alt="image" src="https://github.com/user-attachments/assets/218b7608-ec67-4356-be9c-596369463c69" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
