

1. Draw database design for song app -> perform normalization

2. Types of keys in Database table ->
- In our database tables we have different types of keys like Primary key, Unique key, foreign key
- **Primary Key** -> defines a row of the database table, primary key column has a type of unique keys.
- **Foreign Key->** In our table we have a foreign key constaint also which, which used to estabshish the relationship between two tables we use REFERENCES keywork to achieve this thing
- **Uniqie Key->** The uniqie key column means all values of that particular column are unique in nature

### 3. ACID principles ->
- A -> Atomicity -> Either all or null -> if commit is successfull thenn only perform it, if fails before commit then rollback the transaction.

- C -> Consistency -> Before the transaction starts and after the transaction completed 

- I -> Isolation -> trying to convert a parellel schedule into single schedule

- D -> Durability -> All changes we are doing the databases should be permanent.

ACID properties are a set of principles that ensure reliable processing of database transactions. They stand for Atomicity, Consistency, Isolation, and Durability. Here's an easy-to-understand explanation of each with a simple example:

### 1. Atomicity
**Definition**: Transactions are all-or-nothing. Either the entire transaction is completed, or none of it is.

**Example**: Imagine you are transferring money from your savings account to your checking account. The transaction has two steps:
1. Deduct money from your savings account.
2. Add money to your checking account.

Atomicity ensures that if one step fails (e.g., the deduction succeeds but the addition fails), the entire transaction is rolled back, and your money remains in your savings account.

### 2. Consistency
**Definition**: Transactions must leave the database in a consistent state. This means the database must follow all its rules (like data constraints) before and after the transaction.

**Example**: Suppose there’s a rule that your bank account balance cannot be negative. If you try to transfer more money than you have, consistency ensures the transaction is rejected, keeping the database consistent with its rules.

### 3. Isolation
**Definition**: Transactions should not interfere with each other. Intermediate states of a transaction are invisible to other transactions.

**Example**: If two people are transferring money at the same time (one transferring to you and one from you), isolation ensures these transactions don’t mess with each other. You won’t see an incorrect balance at any point during the transfers.

### 4. Durability
**Definition**: Once a transaction is committed, it will remain so, even in the event of a power failure, crash, or error.

**Example**: After transferring money and seeing the updated balance, durability ensures that even if the system crashes immediately after, the changes (the updated balance) are not lost. When the system comes back online, your balance reflects the transaction.

### Simple Example in Action

Imagine you are buying a book online:

1. **Atomicity**: 
   - Deduct $10 from your bank account.
   - Add the book to your order history.
   - If adding the book to your order history fails, the $10 is not deducted.

2. **Consistency**:
   - Ensure that your account balance remains consistent (cannot go negative).
   - Confirm the book is available in stock before deducting the amount.

3. **Isolation**:
   - If another customer is buying the last copy of the book at the same time, isolation ensures that both transactions don't interfere, preventing overselling.

4. **Durability**:
   - Once the transaction is complete, even if there’s a power failure, the system will remember that you’ve bought the book and the $10 has been deducted.

Understanding ACID properties helps ensure that database transactions are processed reliably and consistently, even in complex and concurrent environments.

----------------------------------------------------


Here are 20 advanced-level Database Management and Design (DBMD) interview questions along with their answers:

### 1. What is database normalization and why is it important?
**Answer:**
Database normalization is the process of organizing the columns (attributes) and tables (relations) of a database to reduce data redundancy and improve data integrity. It involves dividing a database into two or more tables and defining relationships between the tables. The main goal is to eliminate redundant data, ensure data dependencies make sense, and protect the database against certain types of logical or structural problems, such as data anomalies.

### 2. Explain the differences between SQL and NoSQL databases.
**Answer:**
SQL databases, also known as relational databases, use structured query language (SQL) for defining and manipulating data. They are table-based, follow ACID properties (Atomicity, Consistency, Isolation, Durability), and are suited for complex query operations. Examples include MySQL, PostgreSQL, and Oracle.

NoSQL databases, on the other hand, are designed for distributed data stores with large-scale data storage needs. They can be document-based, key-value pairs, wide-column stores, or graph databases. NoSQL databases are schema-less, follow BASE principles (Basically Available, Soft state, Eventual consistency), and are suited for unstructured data. Examples include MongoDB, Cassandra, and Redis.

### 3. What are ACID properties in a database?
**Answer:**
ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure reliable processing of database transactions.

- **Atomicity** ensures that all operations within a transaction are completed; otherwise, the transaction is aborted.
- **Consistency** ensures that the database remains in a consistent state before and after the transaction.
- **Isolation** ensures that transactions are executed in isolation, preventing concurrent transactions from affecting each other.
- **Durability** ensures that the results of a transaction are permanently stored in the database, even in the event of a system failure.

### 4. What is a database index and how does it improve performance?
**Answer:**
A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional storage space and maintenance overhead. Indexes are created on columns of a table and act like a pointer to data in a table, allowing the database engine to find rows much faster than scanning the entire table. Indexes can be unique, ensuring no duplicate values, or non-unique, allowing duplicates.

### 5. Describe the different types of database joins.
**Answer:**
Joins are used to combine rows from two or more tables based on a related column. Common types of joins include:

- **Inner Join:** Returns only the rows that have matching values in both tables.
- **Left Join (Left Outer Join):** Returns all rows from the left table and the matched rows from the right table. If no match is found, NULL values are returned for columns from the right table.
- **Right Join (Right Outer Join):** Returns all rows from the right table and the matched rows from the left table. If no match is found, NULL values are returned for columns from the left table.
- **Full Join (Full Outer Join):** Returns rows when there is a match in one of the tables. If there is no match, the result is NULL on the side that does not have a match.
- **Cross Join:** Returns the Cartesian product of the two tables, combining all rows from the first table with all rows from the second table.

### 6. What is a foreign key constraint and why is it important?
**Answer:**
A foreign key is a field (or collection of fields) in one table that uniquely identifies a row of another table. The foreign key constraint is used to ensure referential integrity of the data, meaning it ensures that the relationship between two tables remains consistent. It prevents actions that would destroy links between tables, ensuring that any foreign key value points to an existing, valid record in the referenced table.

### 7. Explain the concept of sharding in databases.
**Answer:**
Sharding is a database architecture pattern related to horizontal partitioning. It involves breaking up large databases into smaller, more manageable pieces, called shards, which are distributed across multiple servers. Each shard contains a subset of the data. Sharding improves performance and scalability by distributing the load across multiple servers, thus handling more transactions and larger data volumes more efficiently.

### 8. What are the differences between OLTP and OLAP systems?
**Answer:**
OLTP (Online Transaction Processing) systems are designed to manage transactional data, characterized by a large number of short online transactions. They are optimized for speed and efficiency in terms of query processing and data modification (insert, update, delete). Examples include banking and retail transaction systems.

OLAP (Online Analytical Processing) systems, on the other hand, are designed to handle complex queries and analysis, usually for decision-making purposes. They are optimized for read-heavy operations, allowing for the rapid execution of multidimensional queries. Examples include data warehouses and business intelligence systems.

### 9. What is a stored procedure and what are its advantages?
**Answer:**
A stored procedure is a precompiled set of one or more SQL statements stored on the database server. It can be executed by calling it explicitly within a database session. Advantages of stored procedures include:

- Improved performance due to precompilation.
- Reduced network traffic as multiple SQL statements are executed in a single call.
- Enhanced security by encapsulating logic and controlling access to data.
- Easier maintenance and code reusability by centralizing business logic in the database.

### 10. How does database partitioning work and what are its benefits?
**Answer:**
Database partitioning is the process of dividing a large database into smaller, more manageable pieces called partitions. Each partition can be managed and accessed separately, but they collectively represent the whole database. Partitioning can be done based on ranges, lists, or hashes.

Benefits include improved performance, as queries can be executed on specific partitions instead of scanning the entire database; better management of large tables; increased availability, as partitions can be stored on different disks or servers; and easier maintenance, such as backup and recovery operations.

### 11. What is the difference between a primary key and a unique key?
**Answer:**
A primary key is a field (or combination of fields) that uniquely identifies each record in a table. It enforces entity integrity by ensuring that no two rows have the same primary key value, and it cannot contain NULL values.

A unique key also enforces uniqueness of the column values, ensuring no duplicates, but unlike the primary key, a table can have multiple unique keys, and they can contain NULL values (though typically only one NULL value).

### 12. Explain the concept of database transactions and transaction management.
**Answer:**
A database transaction is a sequence of one or more SQL operations executed as a single unit of work. Transactions are governed by ACID properties to ensure reliability and consistency. Transaction management involves ensuring that transactions are processed reliably and that the database remains consistent even in the event of a failure.

Key operations in transaction management include:
- **BEGIN TRANSACTION:** Starts a new transaction.
- **COMMIT:** Saves the changes made by the transaction to the database.
- **ROLLBACK:** Reverts the changes made by the transaction, restoring the database to its previous state.

### 13. What are materialized views and how do they differ from regular views?
**Answer:**
A materialized view is a database object that contains the results of a query and stores them physically on disk. Unlike regular views, which are virtual tables that dynamically compute their result sets upon each query execution, materialized views improve performance by storing precomputed results. They can be periodically refreshed to reflect changes in the underlying data.

### 14. How do you handle deadlocks in a database?
**Answer:**
Deadlocks occur when two or more transactions are waiting for each other to release locks, resulting in a cycle of dependencies that prevents any of the transactions from proceeding. Handling deadlocks involves:

- **Detection:** Using database mechanisms to detect deadlock situations. The database can periodically check for deadlocks and resolve them.
- **Resolution:** The database can automatically resolve deadlocks by aborting one of the involved transactions, allowing the other to proceed.
- **Prevention:** Implementing strategies such as lock ordering (acquiring locks in a predefined order) or using timeouts (aborting transactions that wait too long for a lock) to prevent deadlocks from occurring.

### 15. What is a database cursor and when would you use it?
**Answer:**
A database cursor is a database object used to retrieve, traverse, and manipulate the result set of a query row by row. Cursors are typically used when a query returns multiple rows and you need to perform operations on each row individually.

Cursors can be useful for tasks such as:
- Performing complex logic on each row of a result set.
- Processing result sets that are too large to fit into memory.
- Implementing row-by-row validations or calculations.

### 16. What is data warehousing and how does it differ from traditional databases?
**Answer:**
Data warehousing involves collecting and managing data from various sources to provide meaningful business insights. It is designed to handle large volumes of data, support complex queries and analysis, and provide historical context for decision-making.

Differences from traditional databases include:
- **Purpose:** Traditional databases are optimized for transaction processing (OLTP), while data warehouses are optimized for analysis and reporting (OLAP).
- **Data Structure:** Data warehouses often use denormalized schemas (e.g., star or snowflake schema) for efficient querying, whereas traditional databases use normalized schemas.
- **Query Performance:** Data warehouses are optimized for read-heavy operations, allowing for fast execution of complex queries across large datasets.

### 17. How do you optimize SQL queries for performance?
**Answer:**
Optimizing SQL queries for performance involves several strategies, including:

1. **Indexing:** Create appropriate indexes on columns that are frequently used in WHERE clauses, JOIN conditions, and ORDER BY clauses.
2. **Query Rewriting:** Rewrite complex queries to simplify them or break them into smaller, more manageable parts.
3. **Use of Joins Efficiently:** Avoid unnecessary joins and use appropriate join types. Use INNER JOIN instead of OUTER JOIN when possible.
4. **Avoiding SELECT *:** Select only the columns that are needed rather than using SELECT * to reduce the amount of data transferred.
5. **Filtering Early:** Apply filters as early as possible in the query to reduce the number of rows processed.
6. **Normalization and Denormalization:** Normalize tables to eliminate redundancy and denormalize where necessary to reduce the number of joins.
7. **Analyze Execution Plans:** Use the database's execution plan to understand how queries are executed and identify performance bottlenecks.
8. **Use of Caching:** Implement caching strategies for frequently accessed data.
9. **Partitioning:** Use table partitioning to divide large tables into smaller, more manageable pieces.
10. **Database Configuration:** Optimize database configuration settings like memory allocation, buffer pool size, and connection pooling.

### 18. Explain the concept of referential integrity and how it is enforced in a database.
**Answer:**
Referential integrity ensures that relationships between tables remain consistent. It is enforced using foreign keys, which link columns in one table to primary keys in another table. The database ensures that any foreign key value must match a primary key value in the referenced table, preventing orphaned records and ensuring data consistency.

Enforcement mechanisms include:
- **Cascading Actions:** Actions such as CASCADE DELETE or CASCADE UPDATE can be defined to automatically propagate changes from parent rows to child rows.
- **Constraints:** Defining foreign key constraints in the database schema to enforce referential integrity rules.

### 19. What are triggers and what are their uses in a database?
**Answer:**
Triggers are special types of stored procedures that automatically execute in response to certain events on a particular table or view. They can be used for:

- **Enforcing Business Rules:** Automatically enforcing complex business rules that cannot be enforced by constraints alone.
- **Auditing:** Recording changes or actions performed on the data for auditing purposes.
- **Data Validation:** Validating data before it is inserted, updated, or deleted.
- **Complex Data Integrity Checks:** Ensuring data integrity by performing checks and balances that go beyond standard constraints.

### 20. Describe the concept of a relational database schema and its components.
**Answer:**
A relational database schema is the blueprint that defines the structure of a relational database. It includes the definitions of tables, columns, data types, and the relationships between tables. Components of a relational database schema include:

- **Tables:** Collections of related data entries, organized in rows and columns.
- **Columns:** Attributes of the table that define the type of data stored.
- **Primary Keys:** Unique identifiers for each row in a table.
- **Foreign Keys:** Columns that create a relationship between tables by referencing primary keys in other tables.
- **Indexes:** Data structures that improve the speed of data retrieval.
- **Constraints:** Rules enforced on data columns to ensure data integrity (e.g., NOT NULL, UNIQUE, CHECK, PRIMARY KEY, FOREIGN KEY).
- **Views:** Virtual tables created by querying one or more tables.
- **Stored Procedures and Functions:** Predefined SQL code that can be invoked to perform specific operations.
- **Triggers:** Procedures that automatically execute in response to certain events.

These advanced-level questions and answers should help in preparing for a DBMD interview. If you have any specific areas you'd like to delve deeper into, let me know!

# Normalization: 
Normalization in SQL is the process of organizing the columns (attributes) and tables (relations) of a database to reduce data redundancy and improve data integrity. The primary goal is to isolate data so that additions, deletions, and modifications can be made in just one table and then propagated through the rest of the database via defined relationships.

### Normal Forms

Normalization typically involves dividing a database into two or more tables and defining relationships between the tables. Each table should have a single purpose, and each column should store a single type of data. The steps to achieve this are called normal forms (NF), and the most common ones are:

1. **First Normal Form (1NF)**: Ensures that the table is a valid relation by:
    - Eliminating repeating groups and ensuring that each column contains atomic (indivisible) values.
    - Ensuring that each column contains only one value per row.

2. **Second Normal Form (2NF)**: Builds on 1NF by:
    - Ensuring that all non-key attributes are fully functionally dependent on the primary key.
    - Removing partial dependencies, which means no attribute should depend on only part of the primary key if the primary key is composite.

3. **Third Normal Form (3NF)**: Builds on 2NF by:
    - Removing transitive dependencies, meaning non-key attributes should not depend on other non-key attributes.
    - Ensuring that all attributes are only dependent on the primary key.
