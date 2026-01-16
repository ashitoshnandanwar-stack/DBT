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


<hr>

## Group by

GROUP BY is used in SQL to group rows that have the same values in a column and apply aggregate functions like: <br>
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX() <br>

Suppose we have a table Employee:
| emp_id | dept  | salary |
| ------ | ----- | ------ |
| 1      | IT    | 30000  |
| 2      | HR    | 25000  |
| 3      | IT    | 35000  |
| 4      | HR    | 20000  |
| 5      | Sales | 40000  |
```
SELECT dept, SUM(salary) AS total_salary
FROM Employee
GROUP BY dept;
```
Result:
| dept  | total_salary |
| ----- | ------------ |
| IT    | 65000        |
| HR    | 45000        |
| Sales | 40000        |

```
Important Rules
Every column in SELECT that is not an aggregate must appear in GROUP BY.
WHERE filters rows before grouping.
HAVING filters groups after grouping
```
```
SELECT dept, COUNT(*) AS emp_count
FROM Employee
GROUP BY dept
HAVING COUNT(*) > 1;
This returns only departments having more than one employee.
```

### 🔹 LIKE Operator

Used for pattern matching.<br>

| Symbol | Meaning                  |
| ------ | ------------------------ |
| `%`    | Any number of characters |
| `_`    | Single character         |

```
SELECT * FROM Student WHERE name LIKE 'A%';   -- starts with A
SELECT * FROM Student WHERE name LIKE '_a%';  -- second letter is 'a'
```

### 🔹 DISTINCT
- Removes duplicate values.
```
SELECT DISTINCT city FROM Student;
```

### 🔹 ORDER BY (Sorting)
- Used to sort result set.
```
SELECT * FROM Student ORDER BY marks ASC;   -- ascending
SELECT * FROM Student ORDER BY marks DESC;  -- descending
```
- in default - ascending
  
🔹 BETWEEN … AND
- Used to select values within a range.
```
SELECT * FROM Student WHERE marks BETWEEN 50 AND 80;
```

🔹 IS NULL / IS NOT NULL
- Used to compare NULL values.
```
SELECT * FROM Employee WHERE email IS NULL;
SELECT * FROM Employee WHERE email IS NOT NULL;
```

🔹 IN / NOT IN
- Used to match multiple values.
```
SELECT * FROM Student WHERE city IN ('Pune', 'Mumbai');
SELECT * FROM Student WHERE city NOT IN ('Delhi', 'Chennai');
```

<hr>

### Relation Algebra

- Relational Algebra is a procedural query language used in DBMS.
It works on relations (tables) and always produces a new relation as output.

1. Selection ( σ )
– Selects rows (tuples) based on a condition.
```
Syntax:
σ_condition(Relation)

Example:
σ_marks > 60(Student)
(SQL: SELECT * FROM Student WHERE marks > 60;)
```

2.Projection ( π ) 
– Selects specific columns (attributes).
```
Syntax:
π_column1, column2(Relation)

Example:
π_name, city(Student)
(SQL: SELECT name, city FROM Student;)
```

3. Union ( ∪ )
– Combines tuples from two relations.

Conditions:<br>
- Same number of attributes
- Same data type
- Same order of attributes
```
Syntax:
R ∪ S

Example:
Student_A ∪ Student_B
(SQL: SELECT * FROM A UNION SELECT * FROM B;)
```

4. Intersection ( ∩ )
– Returns common tuples from both relations.
```
Syntax:
R ∩ S

(SQL: SELECT * FROM A INTERSECT SELECT * FROM B;)
```

5. Minus / Set Difference ( − )
– Tuples in R but not in S.
```
Syntax:
R − S

(SQL: SELECT * FROM R MINUS SELECT * FROM S;
or EXCEPT)
```

6. Cross / Cartesian Product ( × )
– Combines every tuple of R with every tuple of S.
```
Syntax:
R × S

If R has m rows and S has n rows → Result has m × n rows.

Example:
Student × Course

(SQL: SELECT * FROM Student, Course;)
```

```
One-line Summary (for exam):
Selection (σ) → filters rows
Projection (π) → selects columns
Union (∪) → all tuples from both relations
Intersection (∩) → common tuples
Minus (−) → tuples in R not in S
Cartesian (×) → all possible combinations
```

<hr>

## Copying Table Structure / Data in SQL

- SQL provides different ways to copy a table’s structure, data, or both.

1) Copy Only Structure (No Data)
```
CREATE TABLE NewTable AS
SELECT * FROM OldTable WHERE 1=0;
```
- Creates NewTable with same columns.
- No records are copied.

(Alternative in MySQL) <br>
```
CREATE TABLE NewTable LIKE OldTable;
```

2) Copy Structure + Data
```
CREATE TABLE NewTable AS
SELECT * FROM OldTable;
```
Copies both table design and all rows.

3) Copy Only Data (Table Already Exists)
```
INSERT INTO NewTable
SELECT * FROM OldTable;
```

5) Copy Selected Columns / Rows
```
CREATE TABLE NewTable AS
SELECT id, name
FROM OldTable
WHERE marks > 60;
```
Copies only required columns and filtered rows.

<hr>

## Sequences / AUTO_INCREMENT

- A sequence (or AUTO_INCREMENT) automatically generates unique numbers, usually for Primary Key.
- In MySQL (AUTO_INCREMENT)
```
CREATE TABLE Student (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50),
    marks INT
);
```

Insert without giving id:
```
INSERT INTO Student(name, marks) VALUES ('Amit', 75);
INSERT INTO Student(name, marks) VALUES ('Neha', 82);
```

Output:
```
id   name   marks
1    Amit   75
2    Neha   82
```

<hr>

## UNION vs UNION ALL in SQL

- Both UNION and UNION ALL are used to combine the result of two or more SELECT queries.

Rules (for both): <br>
- Same number of columns
- Same data type
- Same order of columns

#### 🔹 UNION

- Combines results and removes duplicate rows.
- Performs sorting to eliminate duplicates → slower. 

- Syntax:
```
SELECT column1, column2 FROM Table1
UNION
SELECT column1, column2 FROM Table2;
```

- Example:
```
SELECT city FROM Student_A
UNION
SELECT city FROM Student_B;
```
- Result: Each city appears only once.

#### 🔹 UNION ALL

- Combines results and keeps all rows (including duplicates).
- No duplicate check → faster.

- Syntax:
```
SELECT column1, column2 FROM Table1
UNION ALL
SELECT column1, column2 FROM Table2;
```

- Example:
```
SELECT city FROM Student_A
UNION ALL
SELECT city FROM Student_B;
```
- Result: Duplicate cities are not removed

| Feature     | UNION                      | UNION ALL        |
| ----------- | -------------------------- | ---------------- |
| Duplicates  | Removed                    | Kept             |
| Performance | Slower                     | Faster           |
| Sorting     | Yes (to remove duplicates) | No               |
| Use When    | Need unique result         | Need all records |

#### INTERSECT in SQL

- INTERSECT is used to return only the common rows from two SELECT queries.

Rules: <br>
- Same number of columns
- Same data types
- Same order of columns

- Syntax:
```
SELECT column1, column2 FROM Table1
INTERSECT
SELECT column1, column2 FROM Table2;
```

Example:
```
SELECT city FROM Student_A
INTERSECT
SELECT city FROM Student_B;
```

- Result: Only the cities that exist in both Student_A and Student_B will be shown.

- Key Points:
```
Returns common records from both queries

Removes duplicates automatically

Similar to set intersection in mathematics

Not supported in MySQL directly (can be achieved using INNER JOIN or IN)
```

<hr>

## Subquery

- A Subquery is a query written inside another SQL query.
- It is used to fetch data that will be used by the main (outer) query.

- It is also called a nested query.

- Syntax
```
SELECT column_name
FROM table_name
WHERE column_name OPERATOR (
    SELECT column_name
    FROM table_name
    WHERE condition
);
```
- Example
```
Find employees whose salary is greater than the average salary:

SELECT name, salary
FROM Employee
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee
);
```

Here: <br>
- Inner query → SELECT AVG(salary) FROM Employee
- Outer query uses that result

### Types of Subqueries
*1️⃣ Single-row subquery – returns one value*
```
SELECT * FROM Employee
WHERE salary = (SELECT MAX(salary) FROM Employee);
```

*2️⃣ Multi-row subquery – returns multiple values (use IN, ANY, ALL)*
- A Multi-row subquery returns more than one value, so we cannot use =.
- We use operators like IN, ANY, and ALL. <br>

Assume tables:
```
Employee(emp_id, name, salary, dept)
Department(dept_name, location)
```
**🔹 Using IN**
- Used when you want to match any value from the subquery result.
```
SELECT name
FROM Employee
WHERE dept IN (
    SELECT dept_name
    FROM Department
    WHERE location = 'Pune'
);

👉 Returns employees who work in any department located in Pune.
```
**🔹 Using ANY**

- Compares a value with any one value returned by subquery.
```
SELECT name, salary
FROM Employee
WHERE salary > ANY (
    SELECT salary
    FROM Employee
    WHERE dept = 'HR'
);

Meaning:
Salary is greater than at least one HR employee’s salary.

(Equivalent to: greater than the minimum salary in HR)
```

**🔹 Using ALL**
- Compares a value with all values returned by subquery.
```
SELECT name, salary
FROM Employee
WHERE salary > ALL (
    SELECT salary
    FROM Employee
    WHERE dept = 'HR'
);

Meaning:
Salary is greater than every HR employee’s salary.

(Equivalent to: greater than the maximum salary in HR)
```

*3️⃣ Correlated subquery – depends on outer query*
```
SELECT e1.*
FROM Employee e1
WHERE salary > (
    SELECT AVG(salary)
    FROM Employee e2
    WHERE e2.dept = e1.dept
);
```

| Operator | Meaning                                   |
| -------- | ----------------------------------------- |
| `IN`     | Matches any value in the list             |
| `ANY`    | Condition true for **at least one** value |
| `ALL`    | Condition true for **every** value        |


<hr>

## EXISTS / NOT EXISTS

- EXISTS is used to check whether a subquery returns any row.

Syntax:
```
SELECT column
FROM Table1 t1
WHERE EXISTS (SELECT 1 FROM Table2 t2 WHERE condition);
```

- EXISTS → TRUE if subquery returns at least one row
- NOT EXISTS → TRUE if subquery returns no rows

Example:
```
SELECT name
FROM Student s
WHERE EXISTS (
    SELECT 1
    FROM Result r
    WHERE r.id = s.id
);

SELECT name
FROM Student s
WHERE NOT EXISTS (
    SELECT 1
    FROM Result r
    WHERE r.id = s.id
);
```

<hr>

## TCL Commands (Transaction Control Language)
- Used to manage transactions in database.

| Command   | Use                            |
| --------- | ------------------------------ |
| COMMIT    | Save changes permanently       |
| ROLLBACK  | Undo changes                   |
| SAVEPOINT | Set a point inside transaction |

Example:
```
SAVEPOINT A;
INSERT INTO Student VALUES (1,'Amit');
ROLLBACK TO A;
COMMIT;
```
| Command    | Effect                      |
| ---------- | --------------------------- |
| `ROLLBACK` | Cancels uncommitted changes |
| `COMMIT`   | Saves changes permanently   |

- ROLLBACK is useful when an error occurs and you want to restore the table to its previous state.

<hr>

## DCL Commands (Data Control Language)
- Used to control access/permissions.

| Command      | Use                                      |
| ------------ | ---------------------------------------- |
| GRANT        | Give permission                          |
| REVOKE       | Remove permission                        |
| GRANT OPTION | Allow user to grant permission to others |

Example:
```
GRANT SELECT ON Student TO user1;
GRANT SELECT ON Student TO user1 WITH GRANT OPTION;
REVOKE SELECT ON Student FROM user1;
```

<hr>

## Views
- A View is a virtual table created from a query.
- It does not store data physically.

- Syntax:
```
CREATE VIEW MyView AS
SELECT column1, column2 FROM Table WHERE condition;
```
*Types of Views*
1) Simple View
- Based on one table
- No JOIN, GROUP BY, or functions
- Updatable

- Example:
```
CREATE VIEW SimpleView AS
SELECT id, name FROM Student;

call: SELECT * FROM SimpleView;

```


2) Complex View
- Based on multiple tables
- Uses JOIN, GROUP BY, functions
- Not always updatable

- Example:
```
CREATE VIEW ComplexView AS
SELECT d.dept, COUNT(e.id)
FROM Dept d JOIN Emp e ON d.id = e.did
GROUP BY d.dept;

call : SELECT * FROM ComplexView;
```

<hr>

## Indexes

- An Index is a database object used to speed up data retrieval from a table.
- It works like an index in a book – helps find records faster.

- Syntax:
```
CREATE INDEX idx_name ON Student(name);
```
- Benefits of Indexes
```
Faster SELECT queries
Improves search performance
Speeds up WHERE, JOIN, ORDER BY, GROUP BY
Reduces full table scan
```
- Note:
```
Uses extra storage
Slows down INSERT, UPDATE, DELETE (because index must be updated)
```
- Types of Indexes
```
Primary Index – created on primary key (unique & not null)
Unique Index – does not allow duplicate values
Single Column Index – on one column
Composite Index – on multiple columns
Clustered Index – data stored in same order as index (InnoDB PK)
Non-Clustered Index – separate from table data
```
- Example:
```
CREATE UNIQUE INDEX idx_email ON User(email);
CREATE INDEX idx_name_city ON Student(name, city);
```

<hr>

## Temporary Tables
- A Temporary Table exists only for the current session.
```
CREATE TEMPORARY TABLE TempStudent (
    id INT,
    name VARCHAR(50)
);
```
- Automatically dropped when session ends
- Used for intermediate results
- Faster for complex queries

<hr>

## ACID Properties

- ACID ensures reliable transactions.

| Property    | Meaning                              |
| ----------- | ------------------------------------ |
| Atomicity   | All or nothing                       |
| Consistency | Data remains valid                   |
| Isolation   | Transactions don’t affect each other |
| Durability  | Data is saved permanently            |

- Example:
```
If money transfer fails → rollback (Atomicity)
Balance rules always correct (Consistency)
Two users can’t update same row wrongly (Isolation)
After commit, data stays even after crash (Durability)
```

<hr>

## MySQL Storage Engines

1) InnoDB (Default)
```
Supports Transactions
Supports ACID
Supports Foreign Keys
Row-level locking
Crash recovery
Used in modern applications
```

2) MyISAM
```
No transactions
No foreign keys
Faster for read-only data
Table-level locking
Used for reporting / static data
```

- Other Engines
```
MEMORY – Data stored in RAM (very fast, temporary)
ARCHIVE – For storing large logs
CSV – Stores data in CSV format
```

<hr>

## Stored Procedures
- A Stored Procedure is a group of SQL statements stored in the database and executed as a single unit.

- Syntax:
```
DELIMITER //
CREATE PROCEDURE getAllStudents()
BEGIN
    SELECT * FROM Student;
END //
DELIMITER ;

Call the procedure: CALL getAllStudents();
```
- Benefits of Stored Procedures
```
Faster execution (precompiled)
Reduces network traffic
Reusable code
Better security (hide table structure)
Centralized business logic
Easier maintenance
```
- Exam line: Stored Procedure = Predefined SQL logic stored in DB for reuse and performance.

### Procedure Parameters (IN, OUT, INOUT)

1) IN Parameter (Input)
- Used to pass value into procedure (default).
```
CREATE PROCEDURE getStudent(IN sid INT)
BEGIN
    SELECT * FROM Student WHERE id = sid;
END;

Call: CALL getStudent(5);
```

2) OUT Parameter (Output)
- Used to return value from procedure.
```
CREATE PROCEDURE countStudents(OUT total INT)
BEGIN
    SELECT COUNT(*) INTO total FROM Student;
END;

Call:
CALL countStudents(@t);
SELECT @t;
```

3) INOUT Parameter (Both)
- Used for input and output.
```
CREATE PROCEDURE squareNum(INOUT n INT)
BEGIN
    SET n = n * n;
END;

Call:
SET @x = 4;
CALL squareNum(@x);
SELECT @x;   -- Output: 16
```

### Flow Control Statements in MySQL

- Flow control statements are used inside Stored Procedures / Functions to repeat or control execution of SQL logic.

1) LOOP
- Runs continuously until LEAVE is used.
```
DELIMITER //
CREATE PROCEDURE loop_example()
BEGIN
    DECLARE i INT DEFAULT 1;

    myloop: LOOP
        INSERT INTO Numbers VALUES (i);
        SET i = i + 1;

        IF i > 5 THEN
            LEAVE myloop;
        END IF;
    END LOOP;
END //
DELIMITER ;

Call: CALL loop_example();
```

2) WHILE
- Runs while condition is true.
```
DELIMITER //
CREATE PROCEDURE while_example()
BEGIN
    DECLARE i INT DEFAULT 1;

    WHILE i <= 5 DO
        INSERT INTO Numbers VALUES (i);
        SET i = i + 1;
    END WHILE;
END //
DELIMITER ;
```

3) REPEAT
- Runs at least once, then checks condition.
```
DELIMITER //
CREATE PROCEDURE repeat_example()
BEGIN
    DECLARE i INT DEFAULT 1;

    REPEAT
        INSERT INTO Numbers VALUES (i);
        SET i = i + 1;
    UNTIL i > 5
    END REPEAT;
END //
DELIMITER ;
```

### Conditional Statements

1) IF
 ```
IF marks >= 40 THEN
    SET result = 'PASS';
END IF;
```
3) IF–ELSE
```
IF marks >= 40 THEN
    SET result = 'PASS';
ELSE
    SET result = 'FAIL';
END IF;
```
4) IF–ELSEIF–ELSE
```
IF marks >= 75 THEN
    SET grade = 'A';
ELSEIF marks >= 60 THEN
    SET grade = 'B';
ELSE
    SET grade = 'C';
END IF;
```
5) SWITCH / CASE
```
CASE grade
    WHEN 'A' THEN SET msg = 'Excellent';
    WHEN 'B' THEN SET msg = 'Good';
    ELSE SET msg = 'Average';
END CASE;
```

<hr>

- In MySQL, TIMESTAMP is used to store date and time together in the format:
```
YYYY-MM-DD HH:MM:SS
```
- It is commonly used to track:
```
Record creation time
Last updated time
Login time, order time, etc.

Example: Create Table with TIMESTAMP
CREATE TABLE Orders (
    id INT,
    product VARCHAR(50),
    created_at TIMESTAMP
);


Insert data:

INSERT INTO Orders VALUES (1, 'Laptop', NOW());


NOW() inserts the current date and time.

Auto Current Time (Most Used)
CREATE TABLE Users (
    id INT,
    name VARCHAR(30),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Automatically stores the current time when a row is inserted.


Auto Update on Modification
CREATE TABLE Logs (
    id INT,
    message VARCHAR(100),
    updated_at TIMESTAMP 
        DEFAULT CURRENT_TIMESTAMP 
        ON UPDATE CURRENT_TIMESTAMP
);


On insert → current time
On update → time automatically changes

So, TIMESTAMP in MySQL is mainly used for automatic date-time tracking of records.
```

<hr>

## MySQL Built-in Functions

### 🔹 String Functions

| Function      | Use           | Example                  |
| ------------- | ------------- | ------------------------ |
| `UPPER()`     | Uppercase     | `UPPER('sql') → SQL`     |
| `LOWER()`     | Lowercase     | `LOWER('SQL')`           |
| `LENGTH()`    | String length | `LENGTH('Hello')`        |
| `SUBSTRING()` | Extract part  | `SUBSTRING('Hello',2,3)` |
| `CONCAT()`    | Join strings  | `CONCAT('My','SQL')`     |

### 🔹 Numeric Functions

| Function  | Use              | Example       |
| --------- | ---------------- | ------------- |
| `ABS()`   | Absolute value   | `ABS(-10)`    |
| `ROUND()` | Round number     | `ROUND(12.5)` |
| `CEIL()`  | Next integer     | `CEIL(4.2)`   |
| `FLOOR()` | Previous integer | `FLOOR(4.9)`  |
| `MOD()`   | Remainder        | `MOD(10,3)`   |

### 🔹 Date / Time Functions

| Function     | Use                 | Example                               |
| ------------ | ------------------- | ------------------------------------- |
| `NOW()`      | Current date & time | `NOW()`                               |
| `CURDATE()`  | Current date        | `CURDATE()`                           |
| `YEAR()`     | Extract year        | `YEAR(NOW())`                         |
| `MONTH()`    | Extract month       | `MONTH(NOW())`                        |
| `DATEDIFF()` | Difference in days  | `DATEDIFF('2026-01-16','2026-01-01')` |

<hr>

## Cursors in MySQL

- A Cursor is used inside Stored Procedures to process query results row by row.
- Normally SQL works on a complete set of rows, but when you need to handle each row individually (like in loops), cursors are used.

### Types of Cursor
| Type              | Meaning                                                                    |
| ----------------- | -------------------------------------------------------------------------- |
| **Asensitive**    | Cursor may or may not reflect changes made to the table after it is opened |
| **Insensitive**   | Cursor does **not** reflect changes made by other transactions             |
| **Read Only**     | Data fetched by cursor cannot be updated                                   |
| **Nonscrollable** | Cursor moves only **forward** (cannot move backward)                       |

Cursor Syntax in MySQL
```
Steps to use a cursor:
Declare cursor
Declare handler for end of data
Open cursor
Fetch rows in loop
Close cursor
Cursor Example
```

Suppose we have a table:
```
Student(id INT, name VARCHAR(50), marks INT);

We want to read each student and count how many have marks > 60.

DELIMITER //
CREATE PROCEDURE cursor_example()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE s_marks INT;
    DECLARE count_pass INT DEFAULT 0;

    DECLARE cur1 CURSOR FOR
        SELECT marks FROM Student;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

    OPEN cur1;

    read_loop: LOOP
        FETCH cur1 INTO s_marks;

        IF done = 1 THEN
            LEAVE read_loop;
        END IF;

        IF s_marks > 60 THEN
            SET count_pass = count_pass + 1;
        END IF;
    END LOOP;

    CLOSE cur1;

    SELECT count_pass AS Passed_Students;
END //
DELIMITER ;

Call: CALL cursor_example();
```

<hr>

## Triggers in MySQL

- A Trigger is a special program that automatically executes when an event
- INSERT, UPDATE, or DELETE occurs on a table.

- Types based on time:
```
BEFORE Trigger – Executes before the event
AFTER Trigger – Executes after the event

Syntax:

CREATE TRIGGER trigger_name
BEFORE | AFTER INSERT | UPDATE | DELETE
ON table_name
FOR EACH ROW
BEGIN
    -- logic
END;

NEW and OLD Trigger Variables

Used to access row values inside a trigger.

Event	Use
| Event  | Use                        |
| ------ | -------------------------- |
| INSERT | `NEW.column`               |
| UPDATE | `OLD.column`, `NEW.column` |
| DELETE | `OLD.column`               |


Example:
NEW.name → new value being inserted/updated
OLD.salary → old value before update/delete

Trigger Examples
1) BEFORE INSERT Trigger

Automatically set default marks if not given.

DELIMITER //
CREATE TRIGGER before_student_insert
BEFORE INSERT ON Student
FOR EACH ROW
BEGIN
    IF NEW.marks IS NULL THEN
        SET NEW.marks = 0;
    END IF;
END //
DELIMITER ;

2) AFTER UPDATE Trigger

Store old and new salary in audit table.

DELIMITER //
CREATE TRIGGER after_salary_update
AFTER UPDATE ON Employee
FOR EACH ROW
BEGIN
    INSERT INTO Salary_Audit(emp_id, old_sal, new_sal, changed_on)
    VALUES (OLD.id, OLD.salary, NEW.salary, NOW());
END //
DELIMITER ;


3) BEFORE DELETE Trigger

Prevent deletion of admin user.

DELIMITER //
CREATE TRIGGER prevent_admin_delete
BEFORE DELETE ON Users
FOR EACH ROW
BEGIN
    IF OLD.role = 'ADMIN' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Admin cannot be deleted';
    END IF;
END //
DELIMITER ;
```
```
Real-Time Uses of Triggers
Automatically update stock after sales
Maintain audit logs (who changed what & when)
Enforce business rules (no negative balance)
Validate data before insert/update
Prevent unauthorized delete/update
Auto-update summary tables
```
- Exam Lines:
```
Trigger → Automatically executes on table events
BEFORE → Runs before data change
AFTER → Runs after data change
NEW → New row values
OLD → Old row values
```

<hr>

| Query       | Meaning                |
| ----------- | ---------------------- |
| `LIMIT 1`   | First row only         |
| `LIMIT 2`   | First two rows         |
| `LIMIT 1,1` | Skip first, get second |
| `LIMIT 2,1` | Skip two, get third    |


Correct condition:
```
WHERE salary IS NULL;


Incorrect (will not work):

WHERE salary = NULL;   -- ❌ Always false
```

Reason: <br>
- NULL means “unknown”
- Comparisons using = or != do not work with NULL
- SQL provides special operators: IS NULL and IS NOT NULL <br>

So, the correct way to check for a NULL salary is:
```
SELECT * 
FROM emp 
WHERE salary IS NULL;
```

```
Which subquery is correlated? 
A. 
SELECT * FROM emp WHERE salary > (SELECT AVG(salary) FROM emp); 
B. 
SELECT * FROM emp e WHERE salary > (SELECT AVG(salary) FROM emp WHERE dept=e.dept); 
C. 
SELECT * FROM emp WHERE dept IN (10,20); 
D. 
SELECT * FROM emp WHERE salary > 30000;


The correct answer is:
B

SELECT * 
FROM emp e 
WHERE salary > (
    SELECT AVG(salary) 
    FROM emp 
    WHERE dept = e.dept
);
This is a correlated subquery because:
The inner query depends on the outer query.
It uses e.dept from the outer query.
The subquery is executed once for each row of the outer query.
Why others are not correlated:

A
SELECT * FROM emp WHERE salary > (SELECT AVG(salary) FROM emp);
→ Independent subquery (runs once).

C
SELECT * FROM emp WHERE dept IN (10,20);
→ No subquery.

D
SELECT * FROM emp WHERE salary > 30000;
→ No subquery.
```

GRANT is used to give privileges to a user on database objects like tables, views, procedures, etc. <br>

General syntax:
```
GRANT privilege_name ON object_name TO user_name;

Examples:
GRANT SELECT ON emp TO amit;        -- read data
GRANT INSERT ON emp TO amit;        -- insert data
GRANT UPDATE ON emp TO amit;        -- update data
GRANT DELETE ON emp TO amit;        -- delete data

GRANT EXECUTE ON GetEmployee TO amit;  -- run procedure/function


So, GRANT is given to:
Allow a user to access data
Allow a user to modify data
Allow a user to execute procedures/functions

Opposite command:
REVOKE privilege_name ON object_name FROM user_name;
```

```
REPEAT is a post-test loop.
The condition is checked after executing the loop body.
So, the loop body executes at least once, even if the condition is false.

Example (MySQL):

REPEAT
    SET x = x + 1;
UNTIL x > 5
END REPEAT;

Here, the statements inside REPEAT run at least one time.
```

```
LEAVE → exits the loop immediately

ITERATE → skips the current iteration and continues with the next one
```

```
A Non-scrollable cursor allows movement only in the forward direction.
You cannot move backward or jump to previous rows.

Other options:
Scrollable → allows moving forward and backward
Insensitive → does not reflect changes made by other users
Read-only → data cannot be modified, but movement may still be allowed
```
