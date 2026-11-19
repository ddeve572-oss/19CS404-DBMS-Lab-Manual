# Experiment 2: DDL Commands

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
-- Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

For example:

Test	Result
SELECT * FROM Student_details WHERE RollNo = 201;
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
201         David Lee   M           Physics     92


```sql
-- insert into student_details('RollNo','Name','Gender','Subject','MARKS')values('201','David Lee','M','Physics',92);
```

**Output:**

<img width="1195" height="332" alt="image" src="https://github.com/user-attachments/assets/32f8ab11-08ae-4957-9b62-caa47ff38a05" />


**Question 2**
---
-- Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
-- create table item(
item_id text primary key,
item_desc text not null,
rate integer,
icom_id text varchar(4),
foreign key(icom_id) references
company(com_id)
on update set null
on delete set null);
```

**Output:**

<img width="1235" height="440" alt="image" src="https://github.com/user-attachments/assets/67262d5a-26c4-4d43-a0b9-13dbf43978c8" />


**Question 3**
---
-- In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375

```sql
-- insert into Customers(
CustomerID, Name,Address,City,ZipCode)values(306,'Diana Prince','Themyscira',null,null),
(307,'Bruce Wayne','Wayne Mano','Gotham',10007),
(308,'Peter Parker','Queens',null,11375);
```

**Output:**

<img width="1278" height="330" alt="image" src="https://github.com/user-attachments/assets/ca2afcb3-24c0-41df-a5cc-acaec80843ff" />


**Question 4**
---
-- Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0


```sql
--alter table Student_details
add column MobileNumber NUMBER;
alter table Student_details 
add column Address VARCHAR(100);
```

**Output:**

<img width="1226" height="412" alt="image" src="https://github.com/user-attachments/assets/34bd7cca-b167-412a-89c2-255d0bf21105" />


**Question 5**
---
-- Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
-- create table Orders(
OrderID integer primary key,
OrderDate date not null,
CustomerID integer,
foreign key(CustomerID)references Customers(CustomerID));
```

**Output:**

<img width="1225" height="342" alt="image" src="https://github.com/user-attachments/assets/6f144b8b-a7db-4f6b-896a-39413baec2d3" />


**Question 6**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
-- create table Products(
ProductID primary key,
ProductName not null,
Price real check (Price>0),
Stock integer check(Stock>=0));
```

**Output:**

<img width="1297" height="311" alt="image" src="https://github.com/user-attachments/assets/ba1245f8-c032-4e70-9d3f-ed6c4338a90b" />


**Question 7**
---
-- Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

```sql
-- alter table books add column ISBN varchar(30);
alter table books add column domain_dept varchar(30);
```

**Output:**

<img width="1215" height="455" alt="image" src="https://github.com/user-attachments/assets/370cfa5f-19a9-4d6b-9d69-fab5797a89c1" />


**Question 8**
---
--Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME

```sql
-- create table Customers(
CustomerID  INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME);
```

**Output:**

<img width="1231" height="442" alt="image" src="https://github.com/user-attachments/assets/c22a6158-b531-4688-9e5a-c240998cead0" />


**Question 9**
---
-- Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
-- create table contacts(
contact_id  INTEGER  primary key,
first_name  TEXT  not NULL,
last_name  TEXT  not NULL,
email  TEXT,
phone text not null check(length(phone)>=10));
```

**Output:**

<img width="1227" height="373" alt="image" src="https://github.com/user-attachments/assets/40301384-01a3-4648-8747-9829298c17fc" />


**Question 10**
---
--Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
--insert into Products (
ProductID,ProductName,Price,Stock)
select ProductID,ProductName,Price,Stock
from Discontinued_products ;
```

**Output:**

<img width="1277" height="341" alt="image" src="https://github.com/user-attachments/assets/1eecbd18-3eab-46c8-af1b-6d95523b49e0" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
