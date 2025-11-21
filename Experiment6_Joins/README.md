# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
<img width="582" height="452" alt="image" src="https://github.com/user-attachments/assets/5261f91f-9f62-41e1-94dd-db772345917a" />


```sql
select c.cust_name,s.commission from customer c
LEFT JOIN salesman s
ON c.salesman_id=s.salesman_id;
```

**Output:**
--

<img width="568" height="748" alt="image" src="https://github.com/user-attachments/assets/e0f00f6a-06f5-47cb-b390-87e7833ff10c" />


**Question 2**
---
<img width="580" height="812" alt="image" src="https://github.com/user-attachments/assets/a562b2c1-7608-4af5-9bfb-5438d8d046d9" />


```sql
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name as "Customer Name",c.grade,s.name as "Salesman",s.commission from orders o
join customer c
on o.customer_id=c.customer_id
join salesman s
on o.salesman_id=s.salesman_id;
```

**Output:**
--
<img width="570" height="915" alt="image" src="https://github.com/user-attachments/assets/86b0d7bb-e429-4b38-b9e4-87ea1734d6cc" />


**Question 3**
---
<img width="565" height="770" alt="image" src="https://github.com/user-attachments/assets/0c77d587-a8b0-4daf-892e-3e70964a8876" />


```sql
select o.ord_no,o.purch_amt,o.ord_date,c.cust_name,c.city as "customer_city",c.grade,s.name as "salesman_name",s.city as "salesman_city",s.commission from orders o
inner join customer c
on o.customer_id=c.customer_id
inner join salesman s
on o.salesman_id=s.salesman_id;
```

**Output:**
--
<img width="572" height="912" alt="image" src="https://github.com/user-attachments/assets/2a644368-d92b-4627-adf0-7279a57c6238" />


**Question 4**
---
<img width="612" height="560" alt="image" src="https://github.com/user-attachments/assets/bcaa0e8b-7214-4e66-aef7-66197105369d" />


```sql
select n.nurse_id,department_name from nurses n
inner join departments d
on n.department_id=d.department_id
where n.first_name='David' and  last_name='Moore';
```

**Output:**
--
<img width="543" height="297" alt="image" src="https://github.com/user-attachments/assets/5e9e6257-b5a0-4d7b-b6f3-8787b02db2dd" />


**Question 5**
---
<img width="578" height="928" alt="image" src="https://github.com/user-attachments/assets/35be6a89-5b89-4fab-8aad-d6d478bf9e4c" />


```sql
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as "Order Amount" from customer c
left join orders o 
on c.customer_id=o.customer_id
order by o.ord_date ASC;
```

**Output:**
--
<img width="576" height="916" alt="image" src="https://github.com/user-attachments/assets/3fb3641d-d704-4cac-bfdb-ff315a739ca5" />


**Question 6**
---
<img width="607" height="977" alt="image" src="https://github.com/user-attachments/assets/42a0873a-4b83-4b28-9760-6d8e30655905" />


```sql
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount',s.name,s.commission
from customer c
left join orders o
on c.customer_id  =o.customer_id  
left join salesman s
on c.salesman_id=s.salesman_id;
```

**Output:**
--
<img width="573" height="915" alt="image" src="https://github.com/user-attachments/assets/df2e6697-e375-4ca6-a327-e80402ec7472" />


**Question 7**
---
<img width="565" height="746" alt="image" src="https://github.com/user-attachments/assets/c4870c2f-1f0f-4f94-8f8b-de4a1f907be6" />


```sql
select c.cust_name as 'Customer Name',c.city,s.name as 'Salesman',s.commission
from customer c
join salesman s
on c.salesman_id =s.salesman_id 
where s.commission>0.12;
```

**Output:**
--
<img width="572" height="561" alt="image" src="https://github.com/user-attachments/assets/34b70f30-e5a2-4c60-a9a9-7e976f48bc9c" />


**Question 8**
---

<img width="588" height="642" alt="image" src="https://github.com/user-attachments/assets/8da8bc08-db2c-4506-bbd8-7d66d133aa85" />

```sql
SELECT
    p.first_name AS patient_name,
    a.*
FROM
    patients AS p
INNER JOIN
    appointments AS a ON p.patient_id = a.patient_id;

```

**Output:**
--
<img width="595" height="422" alt="image" src="https://github.com/user-attachments/assets/bbf0ec14-4e7f-4c43-9169-71ff1d6cff9a" />


**Question 9**
---
<img width="582" height="620" alt="image" src="https://github.com/user-attachments/assets/28f366fc-89db-4c79-ae67-f058f78be062" />


```sql
SELECT
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM
    patients p
INNER JOIN
    doctors d ON p.doctor_id = d.doctor_id
WHERE
    p.discharge_date IS NOT NULL;

```

**Output:**
--
<img width="580" height="292" alt="image" src="https://github.com/user-attachments/assets/d53998f4-a02b-4edb-9350-c2fceccbac53" />


**Question 10**
---
<img width="590" height="277" alt="image" src="https://github.com/user-attachments/assets/a944171f-0e84-47ff-889e-6bb38f6d2c7e" />


```sql
select c.* from customer c
left join salesman s on c.salesman_id=s.salesman_id
where s.name="Mc Lyon";


```

**Output:**
--
<img width="573" height="312" alt="image" src="https://github.com/user-attachments/assets/1f368600-1024-479e-8131-8c44aa9a8608" />



## RESULT

<img width="732" height="75" alt="image" src="https://github.com/user-attachments/assets/7f1ea3fc-6adc-43b2-ab7d-08c8c743ab4d" />

Thus, the SQL queries to implement different types of joins have been executed successfully.

