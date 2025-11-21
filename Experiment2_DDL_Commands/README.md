# Experiment 2: DDL Commands
### Name : MOHAMMAD SHAHIL
### Register Number : 212223240044

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
CREATE TABLE contacts(
contact_id INT PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK(LENGTH(phone)>=10)
);

```

**Output:**
![image](https://github.com/user-attachments/assets/cb6e0a5d-32d2-4819-8e66-ceca9c27428a)


**Question 2**
---
Insert the following products into the Products table:
Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

```sql
INSERT INTO Products(Name,Category,Price,Stock) 
VALUES ('Smartphone','Electronics','800','150');
INSERT INTO Products(Name,Category,Price,Stock)
VALUES ('Headphones','Accessories','200','300');
```

**Output:**

![Screenshot 2025-05-03 104726](https://github.com/user-attachments/assets/5f06893a-977d-44cd-bab7-64aef6ef977b)



**Question 3**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

```sql
ALTER TABLE employee ADD designation varchar(50);
```

**Output:**
![image](https://github.com/user-attachments/assets/dacc0bde-962e-4878-93eb-2d1ebb7361f7)


**Question 4**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES ('104','Tablet','Electronics','100','50');
```

**Output:**
![image](https://github.com/user-attachments/assets/af64f42c-56c7-4bef-a145-3515d22253b1)


**Question 5**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders(
OrderID INT PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INT,
FOREIGN KEY(CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**
![image](https://github.com/user-attachments/assets/4c9398ca-de58-47fa-96a6-8dbc202ece98)


**Question 6**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
CREATE TABLE Invoices(
InvoiceID INT PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE CHECK(DueDate>InvoiceDate),
Amount REAL CHECK(Amount>0)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/18cce143-dceb-42c8-adf8-77f1b1d13b99)


**Question 7**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices(
InvoiceID INT PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE CHECK(DueDate>InvoiceDate),
OrderID INT,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/4b57f161-7e2d-4e37-9d7c-0da475ff8bd6)


**Question 8**
---
Create a table named Tasks with the following columns:
TaskID as INTEGER
TaskName as TEXT
DueDate as DATE

```sql
CREATE TABLE Tasks(
TaskID INTEGER,
TaskName TEXT,
DueDate DATE
);
```

**Output:**

![image](https://github.com/user-attachments/assets/9f9a0a4e-5d8a-4663-98ae-536cf84a0baf)


**Question 9**
---
Insert all products from Discontinued_products into Products.
Table attributes are ProductID, ProductName, Price, Stock

```sql
INSERT INTO Products(ProductID,ProductName,Price,Stock)
SELECT ProductID,ProductName,Price,Stock FROM Discontinued_Products;
```

**Output:**

![image](https://github.com/user-attachments/assets/53800105-544f-4392-8f0f-344bcb0a500a)


**Question 10**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE

```sql
ALTER TABLE Companies 
ADD COLUMN designation varchar(50);
ALTER TABLE Companies 
ADD COLUMN net_salary number;
ALTER TABLE Companies 
ADD COLUMN dob date;
```

**Output:**

![image](https://github.com/user-attachments/assets/0c063267-1d3c-486d-9b6a-4770063e4b2c)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
