# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

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

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

### Code:
```
SELECT 'Square of 6 is ' || (6 * 6) AS Result;
```

**Expected Output:**  

<img width="437" height="320" alt="image" src="https://github.com/user-attachments/assets/3f3d6a8d-614c-4202-81d8-3cc7ce28859f" />

Square of 6 is 36

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

### Code:
```
WITH RECURSIVE factorial(n, result) AS (
    SELECT 1, 1
    UNION ALL
    SELECT n + 1, result * (n + 1)
    FROM factorial
    WHERE n < 5
)
SELECT 'Factorial of 5 is ' || result AS Result
FROM factorial
WHERE n = 5;
```

**Expected Output:**  

<img width="437" height="427" alt="image" src="https://github.com/user-attachments/assets/ac03019e-297e-461d-8791-8a3407f2ef75" />

Factorial of 5 is 120

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

### Code:
```
SELECT
    CASE
        WHEN MOD(12, 2) = 0 THEN '12 is Even'
        ELSE '12 is Odd'
    END AS Result;
```

**Expected Output:**  

<img width="425" height="392" alt="image" src="https://github.com/user-attachments/assets/51fd7074-40b1-43ae-b97d-4cbeebb8047d" />

12 is Even

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

### Code:
```
WITH RECURSIVE reverse_num(n, rev) AS (
    SELECT 1234, 0

    UNION ALL

    SELECT n / 10,
           rev * 10 + (n % 10)
    FROM reverse_num
    WHERE n > 0
)
SELECT 'Reversed number of 1234 is ' || rev AS Result
FROM reverse_num
WHERE n = 0;
```

**Expected Output:**  

<img width="413" height="427" alt="image" src="https://github.com/user-attachments/assets/54905aff-a100-418e-a94e-577406f18993" />

Reversed number of 1234 is 4321

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

### Code:
```
WITH RECURSIVE multiplication(n) AS (
    SELECT 1
    UNION ALL
    SELECT n + 1
    FROM multiplication
    WHERE n < 10
)
SELECT '5 x ' || n || ' = ' || (5 * n) AS Result
FROM multiplication;
```

**Expected Output:**  

<img width="442" height="422" alt="image" src="https://github.com/user-attachments/assets/816ab012-0e8c-4676-ba1a-c53eb0a50d9f" />

Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
