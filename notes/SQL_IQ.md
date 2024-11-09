# Structural Query Language:
--------------------------------------------------
## Primary key vs Foreign Key:
When discussing primary keys and foreign keys in SQL, it's important to understand their roles and differences:

1. **Primary Key**:
- **Definition**: A primary key is a column or a set of columns that uniquely identifies each row in a table. It ensures that there are no duplicate rows in the table.
- **Usage**: Typically, a primary key is used as a unique identifier for each record in the table. It's also used as a reference point for establishing relationships with other tables through foreign keys.
   - **Example**:
     ```sql
     CREATE TABLE students (
         student_id INT PRIMARY KEY,
         student_name VARCHAR(50)
     );
     ```
- In SQL, a unique key constraint ensures that the values in a column or a group of columns are unique, but it allows one or more of those values to be NULL unless the column is also marked as NOT NULL.

- **Efficient Answer**: "A primary key is a unique identifier for each record in a table. It ensures data integrity by preventing duplicate rows."

2. **Foreign Key**:
- **Definition**: A foreign key is a column or a set of columns in a table that refers to the primary key or a unique key in another table. It establishes a relationship between two tables.
- **Usage**: Foreign keys are used to enforce referential integrity, ensuring that data in related tables remains consistent. They define the relationships between tables, such as one-to-one, one-to-many, or many-to-many relationships.
   - **Example**:
     ```sql
     CREATE TABLE orders (
         order_id INT PRIMARY KEY,
         customer_id INT,
         FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
     );
     ```
- **Efficient Answer**: "A foreign key establishes a relationship between two tables by referencing the primary key or a unique key in another table. It helps maintain data consistency and enforce referential integrity."
---------------------------------------
## 2. Primary key vs Unique key:
The primary key and unique key are both constraints used in SQL to enforce data integrity and uniqueness within a table, but they have distinct purposes and differences:

1. **Primary Key**:
   - **Purpose**: The primary key uniquely identifies each record in a table.
   - **Uniqueness**: Values in the primary key column(s) must be unique and cannot contain null values.
   - **Constraints**: There can be only one primary key constraint per table.
   - **Automatic Indexing**: Primary keys typically have an associated index automatically created by the database system.
   - **Usage**: Primary keys are often used as foreign keys in other tables to establish relationships.

2. **Unique Key**:
   - **Purpose**: The unique key constraint ensures that values in the specified column(s) are unique across all rows in the table.
   - **Uniqueness**: Values in the unique key column(s) must be unique, but they can contain null values unless the column is marked as `NOT NULL`.
   - **Constraints**: A table can have multiple unique key constraints, each ensuring uniqueness within its defined columns.
   - **Indexing**: Unique keys can also have indexes for performance optimization, but they are not automatic like primary keys.
   - **Usage**: Unique keys are used to enforce uniqueness on columns that are not primary keys but still require unique values.

Here's a summary of the differences:

- **Uniqueness and Null Values**: Primary keys cannot contain null values and enforce uniqueness, while unique keys can allow null values (unless marked as `NOT NULL`) but still enforce uniqueness.
  
- **Number of Constraints**: A table can have only one primary key constraint, whereas it can have multiple unique key constraints.
  
- **Indexing**: Primary keys usually have an associated index for performance optimization, whereas unique keys may or may not have indexes depending on the database design.
-------------------------------------------------------
## Indexing?
Indexing in databases is a technique used to improve the speed of data retrieval operations, such as querying, searching, and sorting, by creating data structures that allow for efficient access to specific rows or columns in a table. Here are some key points about indexing:

1. **Purpose**:
   - Indexing is used to speed up data retrieval operations by creating a sorted data structure (index) that contains pointers to rows in a table.
   - It helps reduce the time it takes to search for, filter, and sort data based on specific criteria.

2. **How It Works**:
   - An index is created on one or more columns of a table.
   - The index contains key-column values from the table along with pointers to the actual rows in the table.
   - When a query is executed that involves the indexed columns, the database can use the index to quickly locate the relevant rows without scanning the entire table.

3. **Types of Indexes**:
   - **Primary Index**: Automatically created for primary key columns. Ensures fast access to rows based on the primary key values.
   - **Unique Index**: Enforces uniqueness on columns and speeds up searches for unique values.
   - **Non-Unique Index**: Allows duplicate values in indexed columns but still speeds up search operations.
   - **Composite Index**: Created on multiple columns. Useful for queries that involve multiple conditions or join operations.
   - **Clustered Index**: Organizes the data physically on disk based on the indexed column(s), which can improve performance for range queries.
   - **Non-Clustered Index**: Stores index entries separately from the actual data, allowing for faster access to specific rows but not affecting the physical order of data.

4. **Benefits**:
   - Faster data retrieval: Indexing reduces the number of disk accesses needed to fetch data, resulting in faster query performance.
   - Efficient sorting and filtering: Indexes make sorting and filtering operations more efficient, especially for large datasets.
   - Improved join performance: Indexes on join columns can speed up join operations between tables.


In summary, indexing is a crucial optimization technique in databases that enhances query performance and overall system efficiency by providing fast access paths to data based on specified criteria.
------------------------------
## Can a one table have both Primary and Foreign Key?
```java
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50)
);

CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```
--------------------------------------
