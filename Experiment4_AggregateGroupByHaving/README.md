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
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table
<img width="1082" height="154" alt="image (8)" src="https://github.com/user-attachments/assets/732ed1ee-9c10-4ac1-9bba-4535b035cbee" />

```sql
SELECT PatientID, 
    COUNT(Medication) AS TotalMedications
FROM Prescriptions
GROUP BY PatientID;
```

**Output:**

<img width="651" height="802" alt="image" src="https://github.com/user-attachments/assets/ee2565cb-bbd1-4626-8a57-688c6cadfebd" />


**Question 2**
---
What is the count of male and female patients?

Sample table: Patients Table
<img width="1076" height="161" alt="image (3)" src="https://github.com/user-attachments/assets/daacba95-5d52-4dad-b655-137a44c504d2" />



```sql
SELECT 
    Gender, 
    COUNT(*) AS TotalPatients
FROM Patients
GROUP BY Gender;

```

**Output:**

<img width="611" height="428" alt="image" src="https://github.com/user-attachments/assets/b547d6fa-9752-483f-a55f-aba2a6f188a5" />


**Question 3**
---
How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table

<img width="1088" height="162" alt="image (7)" src="https://github.com/user-attachments/assets/1baeaf03-210b-4002-9a21-7fddce2d006f" />


```sql
SELECT 
    InsuranceCompany, 
    COUNT(*) AS TotalExpiredPatients
FROM Insurance
WHERE ValidityPeriod < CURRENT_DATE
GROUP BY InsuranceCompany;

```

**Output:**

<img width="884" height="803" alt="image" src="https://github.com/user-attachments/assets/3a9b2cc8-fb30-4ce2-9eb4-9c9251052264" />


**Question 4**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders


```sql
SELECT 
    AVG(purch_amt) AS AVERAGE
FROM orders;

```

**Output:**

<img width="360" height="366" alt="image" src="https://github.com/user-attachments/assets/b414b1e9-530c-440b-9fca-e7e4309c3058" />


**Question 5**
---
Write a SQL query to find the average length of names for people living in Chennai?



```sql
SELECT 
    AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city = 'Chennai';
```

**Output:**

<img width="451" height="374" alt="image" src="https://github.com/user-attachments/assets/4a1d7529-fb18-46d3-abe9-7a9a1ef4623f" />


**Question 6**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits


```sql
SELECT 
    SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';

```

**Output:**

<img width="372" height="365" alt="image" src="https://github.com/user-attachments/assets/ef0903a1-5ebd-4a87-87d7-ec5c57a675c6" />


**Question 7**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

```sql
SELECT 
    COUNT(DISTINCT age) AS COUNT
FROM employee;

```

**Output:**

<img width="329" height="377" alt="image" src="https://github.com/user-attachments/assets/2bca3efd-22a1-4c10-a449-12e7c37817ed" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

Sample table: employee
<img width="1011" height="215" alt="unnamed" src="https://github.com/user-attachments/assets/7d84cdd2-47b6-4451-8e51-ca90be24c828" />

```sql
SELECT 
    age, 
    MAX(income) AS "MAX(income)"
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;
```

**Output:**

<img width="569" height="426" alt="image" src="https://github.com/user-attachments/assets/1727fc56-c74a-4968-94de-ac2c7d623712" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee

<img width="1011" height="215" alt="unnamed" src="https://github.com/user-attachments/assets/74f9d704-c113-4e29-b89b-260da68c0265" />


```sql
SELECT 
    city, 
    SUM(income) AS Income
FROM employee
GROUP BY city
HAVING SUM(income) > 200000;
```

**Output:**

<img width="565" height="589" alt="image" src="https://github.com/user-attachments/assets/037655c9-f604-483f-830a-6fa2b96e2a3c" />


**Question 10**
---
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products
<img width="972" height="212" alt="unnamed" src="https://github.com/user-attachments/assets/6c4a39e9-c6e4-46e3-8250-e79b21618dc6" />



```sql
SELECT 
    category_id, 
    SUM(price) AS Total_Cost
FROM products
GROUP BY category_id
HAVING SUM(price) > 50;
```

**Output:**

<img width="587" height="404" alt="image" src="https://github.com/user-attachments/assets/ef7a4923-341b-423b-a899-d1897ee7537c" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
