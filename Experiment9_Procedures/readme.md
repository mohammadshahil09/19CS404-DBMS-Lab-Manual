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

#### Program:
```
CREATE OR REPLACE PROCEDURE find_square (num IN NUMBER)
IS
   result NUMBER;
BEGIN
   result := num * num;
   DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || result);
END;
```

```
EXEC find_square(6);
```

**Expected Output:**  
Square of 6 is 36
![op1](https://github.com/user-attachments/assets/533227d9-6718-4bb9-88e6-8222e3d797b8)



---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

#### Program:
```
CREATE OR REPLACE FUNCTION get_factorial (n IN NUMBER)
RETURN NUMBER
IS
   fact NUMBER := 1;
BEGIN
   FOR i IN 1..n LOOP
      fact := fact * i;
   END LOOP;
   RETURN fact;
END;
```
```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
```

**Expected Output:**  
Factorial of 5 is 120

![op2](https://github.com/user-attachments/assets/0eefbe95-da02-4001-8b92-e1e374f517ac)


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

#### Program:
```
CREATE OR REPLACE PROCEDURE check_even_odd (n IN NUMBER)
IS
BEGIN
   IF MOD(n, 2) = 0 THEN
      DBMS_OUTPUT.PUT_LINE(n || ' is Even');
   ELSE
      DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
   END IF;
END;
```
```
EXEC check_even_odd(12);
```

**Expected Output:**  
12 is Even

![op3](https://github.com/user-attachments/assets/5fe13720-02e9-45ad-aa6a-43a10a94b5d7)


---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

#### Program:
```
CREATE OR REPLACE FUNCTION reverse_number (n IN NUMBER)
RETURN NUMBER
IS
   rev NUMBER := 0;
   temp NUMBER := n;
BEGIN
   WHILE temp > 0 LOOP
      rev := rev * 10 + MOD(temp, 10);
      temp := TRUNC(temp / 10);
   END LOOP;
   RETURN rev;
END;
```
```
BEGIN
   DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || reverse_number(1234));
END;
```

**Expected Output:**  
Reversed number of 1234 is 4321

![op4](https://github.com/user-attachments/assets/759cedd2-6cd8-4a1b-9a56-26f88bd86797)


---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

#### Program:
```
CREATE OR REPLACE PROCEDURE print_table (n IN NUMBER)
IS
BEGIN
   DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || n || ':');
   FOR i IN 1..10 LOOP
      DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
   END LOOP;
END;
```
```
EXEC print_table(5);
```

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

![op5](https://github.com/user-attachments/assets/6eb9acff-de64-4eee-9607-3d3f9ae6fb28)


---

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
