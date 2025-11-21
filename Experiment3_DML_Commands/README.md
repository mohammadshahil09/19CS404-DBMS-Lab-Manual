# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```
sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```
sql
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
```
sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```
sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```
sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```
sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
![image](https://github.com/user-attachments/assets/4edfbe94-d2a2-4790-aaac-56760b245cb8)

```
sql
UPDATE Products SET quantity=(quantity*1.10);
```

**Output:**

![image](https://github.com/user-attachments/assets/85a4836f-123c-4637-bcc7-d23e9f2fe1c4)

**Question 2**
---
![image](https://github.com/user-attachments/assets/01f97ed1-fc38-4cde-bdb4-a737c5af82b1)


```sql
UPDATE Employees SET first_name='John' WHERE department_id=80 AND commission_pct<0.35;
```

**Output:**

![image](https://github.com/user-attachments/assets/9a1bed06-0e20-4777-8487-3ce48aecdd10)


**Question 3**
---
![image](https://github.com/user-attachments/assets/dd2d8229-5c68-45ab-8a30-d721e365512d)


```sql
UPDATE Employees SET email='not available',commission_pct=0.55 WHERE department_id=110;
```

**Output:**

![image](https://github.com/user-attachments/assets/edcd4d72-71c4-4777-abf5-3e8ec9e27c6c)


**Question 4**
---
![image](https://github.com/user-attachments/assets/5477916f-1378-46b1-821b-541c1053cabd)


```sql
UPDATE Employees SET salary=8000 WHERE employee_id=105 AND salary<5000;
```

**Output:**

![image](https://github.com/user-attachments/assets/e0fca6fc-a4f8-468a-a13c-c5faf9dde25a)


**Question 5**
---
![image](https://github.com/user-attachments/assets/1eca85d1-b3d9-4af5-8431-756c45189f44)


```sql
UPDATE Employees SET salary=salary*2 WHERE department_id=20 AND job_id like '%MAN';
```

**Output:**

![image](https://github.com/user-attachments/assets/8c8f2253-a802-4e5e-8a03-3cdfa6f11021)


**Question 6**
---
![image](https://github.com/user-attachments/assets/baa40d29-342f-4df1-9c43-d0ea4f364941)


```sql
DELETE FROM Doctors WHERE doctor_id=1;
```

**Output:**

![image](https://github.com/user-attachments/assets/e2ba0952-f9e3-4c6b-9694-8ab026b0a9a4)


**Question 7**
---
![image](https://github.com/user-attachments/assets/861f2edc-7e6c-4257-b7e8-bf14fdc659a6)


```sql
DELETE FROM Customer WHERE GRADE=2;
```

**Output:**

![image](https://github.com/user-attachments/assets/0610af38-38ed-458b-a24a-7938456be64e)


**Question 8**
---
![image](https://github.com/user-attachments/assets/bbcfde15-fdc4-4bf9-af97-9c76afa51fb3)


```sql
DELETE FROM Surgeries WHERE surgery_id=3 OR surgeon_id=4;
```

**Output:**

![image](https://github.com/user-attachments/assets/2c63a4f7-ecef-4a17-af11-8d568054ab04)


**Question 9**
---
![image](https://github.com/user-attachments/assets/a9eb0580-b7a2-42cf-a238-d7f8724f3462)

```sql
DELETE FROM Doctors WHERE last_name is NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/cee58d80-36cc-43b7-a9a1-034776d6bda4)


**Question 10**
---
![image](https://github.com/user-attachments/assets/9ee2dc3e-402d-4093-9609-81b72e094074)


```sql
DELETE FROM Customer WHERE WORKING_AREA='New York';
```

**Output:**

![image](https://github.com/user-attachments/assets/bee90e63-4c2f-4767-bbfa-fb79325fae3b)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
