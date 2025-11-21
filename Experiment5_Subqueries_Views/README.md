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
-- <img width="933" height="384" alt="image" src="https://github.com/user-attachments/assets/811a1377-023e-4ba8-963e-fce85d3cff52" />


```sql
SELECT 
    department_id AS depar,
    department_name
FROM 
    Departments
WHERE 
    LENGTH(department_name) > (
        SELECT AVG(LENGTH(department_name))
        FROM Departments
    );

```

**Output:**

<img width="462" height="313" alt="image" src="https://github.com/user-attachments/assets/d36524d9-03e2-4455-88a5-4b3963d70f6a" />


**Question 2**
<img width="970" height="599" alt="image" src="https://github.com/user-attachments/assets/d96df600-88d1-458a-a8ce-613c3ddd212b" />


```sql
SELECT 
    s.salesman_id,
    s.name
FROM 
    salesman s
JOIN 
    customer c 
ON 
    s.salesman_id = c.salesman_id
GROUP BY 
    s.salesman_id, s.name
HAVING 
    COUNT(c.customer_id) > 1;
```

**Output:**

<img width="496" height="369" alt="image" src="https://github.com/user-attachments/assets/fbd74a0f-f6ed-483a-8154-c4f8084cdddf" />


**Question 3**
<img width="1148" height="586" alt="image" src="https://github.com/user-attachments/assets/124e352e-8b19-435c-a399-a6daabfceb4d" />


```sql
SELECT
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    o.customer_id,
    o.salesman_id
FROM
    orders AS o
JOIN
    salesman AS s ON o.salesman_id = s.salesman_id
WHERE
    s.name = 'Paul Adam';
```

**Output:**

<img width="996" height="298" alt="image" src="https://github.com/user-attachments/assets/74c7af5b-b54b-4304-b6c0-ab0237500ca7" />


**Question 4**
<img width="818" height="550" alt="image" src="https://github.com/user-attachments/assets/d8ce078d-5753-40f1-b094-14a3aae751d8" />


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY < 2500;
```

**Output:**

<img width="961" height="356" alt="image" src="https://github.com/user-attachments/assets/12129727-46d5-448d-bcb6-3c6806d8a566" />


**Question 5**
<img width="826" height="546" alt="image" src="https://github.com/user-attachments/assets/c84ac9db-1386-4e44-ac30-958a2c0881bb" />


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="977" height="336" alt="image" src="https://github.com/user-attachments/assets/b97d25ab-03de-462e-ac8c-7d61c32e6fc2" />


**Question 6**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.
SALESMAN TABLE

| name        | type         |
| ----------- | ------------ |
| salesman_id | numeric(5)   |
| name        | varchar(30)  |
| city        | varchar(15)  |
| commission  | decimal(5,2) |

ORDERS TABLE

| name        | type |
| ----------- | ---- |
| ord_no      | int  |
| purch_amt   | real |
| ord_date    | text |
| customer_id | int  |
| salesman_id | int  |


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM ORDERS o
JOIN SALESMAN s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**

<img width="1235" height="548" alt="image" src="https://github.com/user-attachments/assets/1c2de7da-1bd6-4b68-ae4f-a82f30f4ed96" />


**Question 7**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

| name   | type    |
| ------ | ------- |
| id     | INTEGER |
| name   | TEXT    |
| age    | INTEGER |
| city   | TEXT    |
| income | INTEGER |


```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**

<img width="1245" height="503" alt="image" src="https://github.com/user-attachments/assets/054814a6-ee14-4fb3-a640-2a9326852728" />


**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

| ID | NAME     | AGE | ADDRESS   | SALARY |
| -- | -------- | --- | --------- | ------ |
| 1  | Ramesh   | 32  | Ahmedabad | 2000   |
| 2  | Khilan   | 25  | Delhi     | 1500   |
| 3  | Kaushik  | 23  | Kota      | 2000   |
| 4  | Chaitali | 25  | Mumbai    | 6500   |
| 5  | Hardik   | 27  | Bhopal    | 8500   |
| 6  | Komal    | 22  | Hyderabad | 4500   |
| 7  | Muffy    | 24  | Indore    | 10000  |


```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="1205" height="669" alt="image" src="https://github.com/user-attachments/assets/48ca9725-8dd6-453e-8181-54a052fa5c80" />


**Question 9**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

| name        | type         |
| ----------- | ------------ |
| salesman_id | numeric(5)   |
| name        | varchar(30)  |
| city        | varchar(15)  |
| commission  | decimal(5,2) |


orders table

| name        | type |
| ----------- | ---- |
| order_no    | int  |
| purch_amt   | real |
| order_date  | text |
| customer_id | int  |
| salesman_id | int  |

```sql
SELECT o.ord_no AS ord_no,o.purch_amt,o.ord_date AS ord_date,o.customer_id,o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.name = 'Paul Adam';

```

**Output:**

<img width="1246" height="439" alt="image" src="https://github.com/user-attachments/assets/1f2056e2-f20d-4524-bc60-58dfca3b24a2" />


**Question 10**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

| name  | type    |
| ----- | ------- |
| id    | INTEGER |
| name  | TEXT    |
| city  | TEXT    |
| email | TEXT    |
| phone | INTEGER |


```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);
```

**Output:**

<img width="482" height="524" alt="image" src="https://github.com/user-attachments/assets/7812d08a-b194-4849-bc2a-c1e2bfa57680" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
