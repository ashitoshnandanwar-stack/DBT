## 🔹 Introduction to NoSQL Databases

- NoSQL (Not Only SQL) databases are designed to handle large volumes of data that may be structured, <br>
semi-structured, or unstructured. They provide high scalability, flexibility, and performance, <br>
especially for big data and real-time web applications.
- Used in: social media apps, IoT, e-commerce, real-time analytics, cloud systems.
- Examples: MongoDB, Cassandra, Redis, CouchDB, Neo4j.

### 🔹 Features of NoSQL Databases
```
Schema-less or flexible schema
Horizontal scalability (scale-out using multiple servers)
High performance for read/write operations
Handles big data and distributed systems
Fault tolerance & replication
Supports unstructured and semi-structured data
Suitable for real-time applications
```

### 🔹 Structured vs Semi-Structured vs Unstructured Data

| Type                | Description                     | Example                      |
| ------------------- | ------------------------------- | ---------------------------- |
| **Structured**      | Fixed schema, tabular format    | RDBMS tables, CSV            |
| **Semi-Structured** | No rigid schema, uses tags/keys | JSON, XML                    |
| **Unstructured**    | No predefined format            | Images, videos, emails, text |

- RDBMS → Structured
- NoSQL → Semi-structured & Unstructured

### 🔹 Difference Between RDBMS and NoSQL

| Feature      | RDBMS               | NoSQL                     |
| ------------ | ------------------- | ------------------------- |
| Schema       | Fixed               | Flexible / Dynamic        |
| Data Type    | Structured          | Structured + Unstructured |
| Scalability  | Vertical (scale-up) | Horizontal (scale-out)    |
| Transactions | ACID                | BASE                      |
| Joins        | Supported           | Limited / Not supported   |
| Examples     | MySQL, Oracle       | MongoDB, Cassandra        |

### Scalability
- Scalability means the ability of a database to handle growing data and users efficiently.

*🔹 SQL (RDBMS) Scalability*
- SQL databases like MySQL, Oracle, SQL Server mainly use Vertical Scaling (Scale Up).
- Increase power of a single server (more RAM, CPU, storage)
- Works well for small to medium applications
- Has a limit (hardware max)
- Complex and expensive for very large systems

- Example: Upgrading a server from 8 GB RAM → 64 GB RAM

- So, SQL = Vertical Scalability

*🔹 NoSQL Scalability*
- NoSQL databases like MongoDB, Cassandra, Redis use Horizontal Scaling (Scale Out).
- Add more machines (nodes/servers)
- Data is distributed across servers
- Handles big data & high traffic easily
- Cheaper and flexible for large-scale apps

- Example: Add 5 more servers to handle millions of users
- So, NoSQL = Horizontal Scalability

📌 Comparison
| Feature      | SQL (RDBMS)           | NoSQL                  |
| ------------ | --------------------- | ---------------------- |
| Scaling Type | Vertical (Scale Up)   | Horizontal (Scale Out) |
| Cost         | Expensive             | Cost-effective         |
| Flexibility  | Limited               | Highly flexible        |
| Best for     | Structured data, ACID | Big data, high traffic |

In short: <br>
- SQL → Scale by making one machine stronger
- NoSQL → Scale by adding more machines

### 🔹 CAP Theorem
- In a distributed system, only two of the following three can be guaranteed at the same time:
```
C – Consistency: Every read gets the latest data (All nodes show the same data at the same time.)
A – Availability: Every request gets a response, , even if some nodes fail.
P – Partition Tolerance: System works even if network fails

NoSQL systems usually choose AP or CP instead of CA.
```
According to CAP Theorem, a distributed database can provide only two out of the three at any moment:
```
CP (Consistency + Partition Tolerance)
Example: HBase, MongoDB (in strict mode)
→ Data is always correct, but system may become unavailable during failure.

AP (Availability + Partition Tolerance)
Example: Cassandra, DynamoDB
→ System is always available, but data may be temporarily inconsistent.

CA (Consistency + Availability)
Example: Traditional SQL databases (single-node)
→ Works when there is no partition; not suitable for large distributed systems.
```

### 🔹 BASE Model
- Opposite of ACID, used in NoSQL:
```
B – Basically Available
A – Soft state
S – Eventually consistent

It allows temporary inconsistency for better availability and performance.
```
```
B – Basically Available
System is always available and responds, even during failures.

S – Soft State
Data may change over time, even without new input (due to replication, sync, etc.).

E – Eventual Consistency
Data becomes consistent after some time.
All nodes will have the same data eventually.

BASE focuses on high availability and scalability, not strict consistency.
```
ACID vs BASE
| ACID (SQL)          | BASE (NoSQL)         |
| ------------------- | -------------------- |
| Strict consistency  | Eventual consistency |
| Strong transactions | Weak transactions    |
| Less scalable       | Highly scalable      |
| Banking systems     | Big data, web apps   |

```
So,
SQL → ACID (strong consistency)
NoSQL → BASE (high availability + eventual consistency)
```

### 🔹 Categories of NoSQL Databases
*1️⃣ Key-Value Store*
- Data stored as key → value
- Very fast access
- Used in caching, sessions
- Examples: Redis, DynamoDB
```
"user101" → "Ashitosh"
```

*2️⃣ Document Store*
- Stores data in JSON/XML-like documents
- Flexible schema
- Examples: MongoDB, CouchDB
```
{
  "id": 1,
  "name": "Ashitosh",
  "course": "DBMS"
}
```

3️⃣ Column-Oriented Store
- Data stored in columns instead of rows
- High performance for analytics
- Examples: Cassandra, HBase
- Used in big data systems.

4️⃣ Graph Database
- Data stored as nodes and edges
- Best for relationships
- Examples: Neo4j
- Used in social networks, recommendation systems.

<hr><hr>

## MongoDB

### 🔹 Introduction to MongoDB
MongoDB is a popular NoSQL document-oriented database.<br>
It stores data in flexible, JSON-like documents instead of tables and rows.<br>
It is designed for high performance, scalability, and ease of development. <br>

Used in: Web apps, mobile apps, real-time analytics, IoT, cloud-based systems.

*🔹 Features of MongoDB*
```
Schema-less (flexible structure)
Stores data in JSON-like format
High performance for read/write
Horizontal scalability (sharding)
Built-in replication & fault tolerance
Rich query language
Supports indexing
Easy integration with modern applications
```

### 🔹 MongoDB Command Interface & MongoDB Compass

*1️⃣ MongoDB Command Interface (Shell)*
- Command-line tool to interact with MongoDB
- Execute queries using JavaScript-like syntax

- Example:
```
show databases
use college
db.students.find()
```

*2️⃣ MongoDB Compass*
- GUI tool for MongoDB
- Visual view of databases, collections, and documents
- Easy to insert, update, delete, and analyze data
- Useful for beginners and debugging

### 🔹 MongoDB Documents & Collections
- Document: A single record stored in JSON/BSON format
- Collection: Group of documents (similar to a table)

- Example document:
```
{
  "_id": 1,
  "name": "Ashitosh",
  "course": "DBMS",
  "marks": 85
}
```
### 🔹 RDBMS & MongoDB Analogies
| RDBMS       | MongoDB    |
| ----------- | ---------- |
| Database    | Database   |
| Table       | Collection |
| Row / Tuple | Document   |
| Column      | Field      |
| Primary Key | _id        |

### 🔹 JSON and BSON Documents
- JSON: Text-based data format
- BSON (Binary JSON): Binary form of JSON used internally by MongoDB
- BSON is faster, smaller, and supports more data types (Date, Int, ObjectId)

- Example:
```
{
  "name": "Ravi",
  "age": 22,
  "city": "Pune"
}
```

| Feature        | JSON (JavaScript Object Notation) | BSON (Binary JSON)                                 |
| -------------- | --------------------------------- | -------------------------------------------------- |
| Format         | Text-based                        | Binary format                                      |
| Human Readable | Yes                               | No (machine readable)                              |
| Storage Size   | Larger                            | Smaller & efficient                                |
| Speed          | Slower to parse                   | Faster to parse                                    |
| Data Types     | Limited (string, number, boolean) | Supports more types (Date, Binary, ObjectId, etc.) |
| Usage          | Data exchange (APIs, web apps)    | Internal storage in MongoDB                        |
| Example Use    | REST APIs, configuration files    | NoSQL databases (MongoDB)                          |
| Schema         | Flexible                          | Flexible                                           |

In short: <br>
```
JSON → Used for data transfer, easy for humans to read
BSON → Used for storage, optimized for speed and efficiency in NoSQL databases like MongoDB
In MongoDB, the conversion from JSON to BSON is done automatically by the MongoDB driver.
```

### 🔹 CRUD Operations in MongoDB
CREATE
```
db.students.insertOne({ name: "Amit", marks: 90 })
db.students.insertMany([{ name: "Ravi" }, { name: "Neha" }])
```
READ
```
db.students.find()
db.students.find({ marks: { $gt: 80 } })
```
UPDATE
```
db.students.updateOne(
  { name: "Amit" },
  { $set: { marks: 95 } }
)
```
DELETE
```
db.students.deleteOne({ name: "Ravi" })
```
UPSERT (Update + Insert)
```
If record exists → update
If not → insert

db.students.updateOne(
  { name: "Rahul" },
  { $set: { marks: 88 } },
  { upsert: true }
)
```

### 🔹 MongoDB Operators

Comparison Operators
```
$eq – equal

$gt – greater than

$lt – less than

$gte, $lte, $ne

db.students.find({ marks: { $gt: 80 } })
```

Logical Operators
```
$and, $or, $not

db.students.find({
  $and: [{ marks: { $gt: 70 } }, { city: "Pune" }]
})
```

### 🔹 Sorting
```
db.students.find().sort({ marks: 1 })   // Ascending
db.students.find().sort({ marks: -1 })  // Descending
```

### 🔹 Indexing in MongoDB

- Indexes improve query performance.

Create index:
```
db.students.createIndex({ name: 1 })
```
View indexes:
```
db.students.getIndexes()
```

Benefits:
```
Faster search
Efficient sorting
Improves performance on large data
```
