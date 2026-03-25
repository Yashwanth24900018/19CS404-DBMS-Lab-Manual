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
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK (Stock >= 0)
);

```

**Output:**

<img width="1225" height="371" alt="image" src="https://github.com/user-attachments/assets/53e6667e-676c-4bd2-b96a-697fdccb2f1a" />


**Question 2**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```sql
ALTER TABLE Employees
ADD COLUMN salary INTEGER CHECK (salary > 0);

```

**Output:**

<img width="1230" height="383" alt="image" src="https://github.com/user-attachments/assets/8b6372b9-3348-4de0-be33-bc56bb03c090" />

**Question 3**
---
Insert the following employees into the Employee table:

```sql
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES
(2, 'John Smith', 'Developer', 'IT', 75000),
(3, 'Anna Bell', 'Designer', 'Marketing', 68000);
```

**Output:**

<img width="864" height="441" alt="image" src="https://github.com/user-attachments/assets/e2592e66-f9bf-4f83-8463-22323d99668e" />


**Question 4**
---
Create a table named Bonuses with the following constraints:

```sql
CREATE TABLE Bonuses (
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK (BonusAmount > 0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

```

**Output:**

<img width="868" height="368" alt="image" src="https://github.com/user-attachments/assets/e77cc5c4-ca31-4b21-92c0-44ebe3005dcf" />


**Question 5**
---
Create a new table named item with the following specifications and constraints:

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4),
    FOREIGN KEY (icom_id)
        REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);
```

**Output:**

<img width="860" height="438" alt="image" src="https://github.com/user-attachments/assets/f665780c-eba8-4339-a8f1-e7c1dfdc8dce" />

**Question 6**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```sql
CREATE TABLE Shipments (
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID)
        REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID)
        REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="864" height="319" alt="image" src="https://github.com/user-attachments/assets/fc8c4d9a-3444-4bb2-ab46-cdabbdae6cc0" />


**Question 7**
---
Insert all students from Archived_students table into the Student_details table.

```sql
INSERT INTO Student_details
SELECT *
FROM Archived_students;
```

**Output:**

<img width="854" height="382" alt="image" src="https://github.com/user-attachments/assets/c274a164-ae4f-4727-b8ab-9dcac8030cb1" />


**Question 8**
---
Write an SQL command can to add a column named email of type TEXT to the customers table


```sql
ALTER TABLE Customers
ADD COLUMN email TEXT;
```

**Output:**

<img width="871" height="381" alt="image" src="https://github.com/user-attachments/assets/04cac048-57c6-4b35-8baa-9d4713fb02c8" />


**Question 9**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
INSERT INTO Products
SELECT * 
FROM Discontinued_products;

```

**Output:**

<img width="859" height="375" alt="image" src="https://github.com/user-attachments/assets/002d053f-be67-414f-9414-ed9f6f999fff" />

**Question 10**
---
Create a new table named products with the following specifications:
```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL(10, 2) NOT NULL,
    discount DECIMAL(10, 2) NOT NULL DEFAULT 0,
    CHECK (
        list_price >= discount AND
        discount >= 0 AND
        list_price >= 0
    )
);
```

**Output:**

<img width="885" height="367" alt="image" src="https://github.com/user-attachments/assets/20c54326-d0ec-43be-9bac-f306dc8dcf5c" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
