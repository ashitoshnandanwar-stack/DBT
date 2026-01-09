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
#### What is BCNF?
```
A relation is in BCNF if for every functional dependency X → Y, X is a super key.

Rule: Determinant must be a candidate key.
```
#### 4NF
removes multivalued dependency

#### 5NF
no unnecessary join dependency(last table divided into small table)
```
1NF → Atomic values
2NF → No partial dependency
3NF → No transitive dependency
BCNF → Determinant is a super key
4NF → No multivalued dependency
5NF → No join dependency
```

## Unique Key
```
🔹 What is a UNIQUE Key?
A UNIQUE key is a constraint that ensures all values in a column (or group of columns) are unique across the table.
👉 It prevents duplicate values but allows NULL values (DBMS-dependent).

🔍 Why UNIQUE Key is Used
To avoid duplicate data
To maintain data integrity
To identify records uniquely (not as primary key)
To enforce business rules

UNIQUE Constraint on Email
CREATE TABLE Student (
  StudentId INT PRIMARY KEY,
  Email VARCHAR(100) UNIQUE,
  Mobile VARCHAR(10)
);
❌ Duplicate email not allowed
```
| StudentId | Email                                   | Mobile     |
| --------- | --------------------------------------- | ---------- |
| 101       | [amit@gmail.com](mailto:amit@gmail.com) | 9876543210 |
| 102       | [ravi@gmail.com](mailto:ravi@gmail.com) | 9123456789 |

```
🔁 Composite UNIQUE Key
A UNIQUE key can be created on multiple columns.
UNIQUE (StudentId, Course)

➡ Combination must be unique.
```

| Feature         | UNIQUE Key    | PRIMARY Key     |
| --------------- | ------------- | --------------- |
| Uniqueness      |  Yes          |  Yes            |
| NULL allowed    |  Yes*         |  No             |
| Count per table | Multiple      | Only one        |
| Purpose         | Alternate key | Main identifier |
| Index created   | Yes           | Yes             |

* MySQL allows multiple NULLs in UNIQUE key.

## Joins
<img width="480" height="360" alt="image" src="https://github.com/user-attachments/assets/3914a43c-fd57-4522-8b5c-e938dfe5eb04" />

<img width="966" height="760" alt="image" src="https://github.com/user-attachments/assets/46d15e28-ec2e-4c56-a89e-4e0fd8f10b50" />


### 3️⃣ Union ( ∪ )
```
🔹 Purpose
Combines tuples/rows from two relations
Removes duplicates

🔹 Conditions
Same number of attributes
Same data types
Same order

✅ Result contains all unique rows from both tables

🧠 Simple Example
Table 1: Student_A
ID | Name
---------
1  | Rahul
2  | Amit
3  | Sneha

Table 2: Student_B
ID | Name
---------
3  | Sneha
4  | Priya
5  | Neha

🔸 SQL Query Using UNION
SELECT ID, Name FROM Student_A
UNION
SELECT ID, Name FROM Student_B;

🔹 Result
ID | Name
---------
1  | Rahul
2  | Amit
3  | Sneha
4  | Priya
5  | Neha


✔ Duplicate row (3, Sneha) appears only once
```
<img width="563" height="261" alt="image" src="https://github.com/user-attachments/assets/b46ea433-78af-4a72-8660-efd67b5f5223" />


### 4️⃣ Intersection ( ∩ ) 
```
🔹 Purpose
Returns common tuples/rows from both relations

🔹 Conditions
(Same as UNION)

✅ Rules of INTERSECT
Same number of columns in both SELECT
Same or compatible data types
Duplicates are removed automatically
Order of columns must match

🧠 Simple Example
Table: Student_A
ID | Name
---------
1  | Rahul
2  | Amit
3  | Sneha

Table: Student_B
ID | Name
---------
3  | Sneha
4  | Priya
5  | Neha

🔸 SQL Query Using INTERSECT
SELECT ID, Name FROM Student_A
INTERSECT
SELECT ID, Name FROM Student_B;

🔹 Result (Common Records Only)
ID | Name
---------
3  | Sneha

✔ Only Sneha exists in both tables
✔ All non-common rows are excluded
```
## Union All
| Feature            | UNION             | UNION ALL        |
| ------------------ | ----------------- | ---------------- |
| Removes duplicates |  Yes              |  No              |
| Performance        | Slower            | Faster           |
| Use case           | Clean merged data | Keep all records |

```
 example are same like union only difference sneha record print once time but in union all print double
```
##
| Relational Algebra | SQL Equivalent |
| ------------------ | -------------- |
| Selection (σ)      | WHERE          |
| Projection (π)     | SELECT columns |
| Union (∪)          | UNION          |
| Intersection (∩)   | INTERSECT      |
| Minus (−)          | EXCEPT / MINUS |
| Cartesian (×)      | CROSS JOIN     |

## NoSQL and MongoDB

### ⚖️ CAP Theorem
```
Proposed by Eric Brewer
CAP = Consistency + Availability + Partition Tolerance
A distributed system can guarantee only two of the three at the same time.
```

| Property                    | Meaning                       |
| --------------------------- | ----------------------------- |
| **Consistency (C)**         | All nodes see same data       |
| **Availability (A)**        | Every request gets response   |
| **Partition Tolerance (P)** | Works despite network failure |
🔹 NoSQL systems choose CP or AP
