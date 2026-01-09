# DBT
RDBMS and NoSQL

## What is a Foreign Key?
-  A foreign key is a column (or group of columns) in a child table that references the primary key of a parent table.
It enforces referential integrity in MySQL databases.

```
3️⃣ Example With Foreign Key (Correct Way)
🔹 Parent Table
CREATE TABLE Customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(50)
);

🔹 Child Table with Foreign Key
CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id)
  REFERENCES Customers(customer_id)
);


✅ Now MySQL rejects invalid customer_id values

4️⃣ Foreign Key with CASCADE (Most Important for Exams)
CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id)
  REFERENCES Customers(customer_id)
  ON DELETE CASCADE
  ON UPDATE CASCADE
);

🔹 What happens?
Deleting a customer → all related orders deleted automatically
Updating customer_id → orders updated automatically

5️⃣ Uses of Foreign Key (Point-wise – CCEE Style)
Maintains data consistency
Establishes parent–child relationship
Prevents invalid inserts
Avoids orphan records
Supports automatic cascading operations
Improves database reliability
Helps in normalization
Ensures business rules at database level

6️⃣ Where Foreign Keys Are Commonly Used
Customer → Orders
Department → Employees
Author → Books
User → Payments
Student → Enrollment

7️⃣ Important MySQL Rules (Exam Alert ⚠️)
Both tables must use InnoDB engine
Referenced column must be PRIMARY KEY or UNIQUE
Data types must be same
Index is automatically created on foreign key
```

## 🔍 Main Differences between Relational database management system and Object RDBMS

| Feature            | RDBMS                   | ORDBMS                  |
| ------------------ | ----------------------- | ----------------------- |
| Data Model         | Tables (rows & columns) | Tables + Objects        |
| OOP Support        |  No                     |  Yes                    |
| User-Defined Types |  Not supported          |  Supported              |
| Inheritance        |  No                     |  Yes                    |
| Methods            |  No                     |  Yes                    |
| Complex Data       |  Difficult              |  Easy                   |
| SQL Support        | Standard SQL            | SQL + Object extensions |
| Performance        | Faster for simple data  | Better for complex data |
| Example Use        | Banking, Sales          | Multimedia, GIS         |

<hr>

##  1️⃣ Data Redundancy
- 🔹 Definition : Data Redundancy means unnecessary duplication of data in a database.
  
## 2️⃣ Data Anomalies
- 🔹 Definition
Data Anomalies are errors or inconsistencies that occur due to data redundancy.
types
1. insertion
2. updatation
3. deletion

## 3️⃣ Functional Dependency (FD)
- A Functional Dependency exists when one attribute uniquely determines another attribute.

## Normalization
- it is performed to reduce the data redundancy in a database. It cause anamolies in database.

#### Normalization Flow
```
UNF   →   1NF    →   2NF   →   3NF
     (repeating)   (partial)  (transitive)
```
