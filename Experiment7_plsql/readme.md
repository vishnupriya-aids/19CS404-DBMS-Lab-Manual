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

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

### program
```sql
  SET SERVEROUTPUT ON;
  
  DECLARE
      a NUMBER := 50;
      b NUMBER := 80;
  BEGIN
      IF a > b THEN
          DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
      ELSE
          DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
      END IF;
  END;
  /
```
**Output:**  
<img width="242" height="124" alt="Screenshot 2025-11-14 113813" src="https://github.com/user-attachments/assets/af8864e9-9f5a-464c-bcf1-4c957932a1ec" />


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

### program
```sql
  SET SERVEROUTPUT ON;
  
  DECLARE
      n   NUMBER := 10;
      i   NUMBER := 1;
      sum NUMBER := 0;
  BEGIN
      WHILE i <= n LOOP
          sum := sum + i;
          i := i + 1;
      END LOOP;
  
      DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
  END;
  /
```
**Output:**  
<img width="659" height="198" alt="image" src="https://github.com/user-attachments/assets/a671e938-6f53-4876-82bd-5afe3914ff34" />


---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

### program
```sql
  SET SERVEROUTPUT ON;
  
  DECLARE
      n NUMBER := 7;
      a NUMBER := 0;
      b NUMBER := 1;
      c NUMBER;
      i NUMBER := 1;
  BEGIN
      DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
  
      WHILE i <= n LOOP
          DBMS_OUTPUT.PUT(a || ' ');
          c := a + b;
          a := b;
          b := c;
          i := i + 1;
      END LOOP;
  END;
  /
```
** Output:**  
 <img width="770" height="460" alt="image" src="https://github.com/user-attachments/assets/7289f70c-01d7-4b4e-ad0a-03968a041188" />


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

### program
```sql
  SET SERVEROUTPUT ON;
  
  DECLARE
      n NUMBER := 1535;
      rem NUMBER;
      rev NUMBER := 0;
      temp NUMBER;
  BEGIN
      temp := n;
  
      WHILE temp > 0 LOOP
          rem := MOD(temp, 10);
          rev := rev * 10 + rem;
          temp := FLOOR(temp / 10);
      END LOOP;
  
      DBMS_OUTPUT.PUT_LINE('Reversed number is: ' || rev);
  END;
  /
```
**Output:**  
<img width="372" height="189" alt="image" src="https://github.com/user-attachments/assets/0d350c09-8179-46d9-b885-3ea560fecba7" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.
### program
```sql
  SET SERVEROUTPUT ON;
  
  DECLARE
      a NUMBER := 10;
      b NUMBER := 9;
      c NUMBER := 15;
      largest NUMBER;
  BEGIN
      IF a > b AND a > c THEN
          largest := a;
      ELSIF b > c THEN
          largest := b;
      ELSE
          largest := c;
      END IF;
  
      DBMS_OUTPUT.PUT_LINE('Largest number is: ' || largest);
  END;
  /
```
**Output:**  
<img width="401" height="171" alt="image" src="https://github.com/user-attachments/assets/4fae40fa-9029-4853-a8b0-de9ca0e48ca6" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

