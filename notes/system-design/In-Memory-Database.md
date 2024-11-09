### Simple In-Memory Database in Java: Detailed Documentation

#### Overview

This simple in-memory database implementation allows for basic CRUD (Create, Read, Update, Delete) operations on tables, without persistent storage. The core components include `Database`, `Table`, and `Row` classes.

#### Components

1. **Row**: Represents a single record with a map of column names to values.
2. **Table**: Manages a list of rows and provides methods for CRUD operations.
3. **Database**: Manages multiple tables and provides an interface for CRUD operations on those tables.

#### Class: Row

The `Row` class represents a single record in a table.

##### Attributes
- `Map<String, Object> data`: Stores the column-value pairs for a row.

##### Methods
- **Constructor**: Initializes a row with given data.
  ```java
  public Row(Map<String, Object> data)
  ```

- **getData**: Returns a copy of the row's data.
  ```java
  public Map<String, Object> getData()
  ```

- **update**: Updates the row's data with new values.
  ```java
  public void update(Map<String, Object> newValues)
  ```

##### Code
```java
import java.util.HashMap;
import java.util.Map;

public class Row {
    private Map<String, Object> data;

    public Row(Map<String, Object> data) {
        this.data = new HashMap<>(data);
    }

    public Map<String, Object> getData() {
        return new HashMap<>(data);
    }

    public void update(Map<String, Object> newValues) {
        for (String key : newValues.keySet()) {
            data.put(key, newValues.get(key));
        }
    }
}
```

#### Class: Table

The `Table` class manages rows and provides methods for CRUD operations.

##### Attributes
- `List<Row> rows`: Stores the rows in the table.

##### Methods
- **Constructor**: Initializes an empty table.
  ```java
  public Table()
  ```

- **insert**: Inserts a new row into the table.
  ```java
  public void insert(Map<String, Object> record)
  ```

- **select**: Retrieves all rows in the table.
  ```java
  public List<Map<String, Object>> select()
  ```

- **update**: Updates rows that match a condition.
  ```java
  public void update(Map<String, Object> newValues, Map<String, Object> condition)
  ```

- **delete**: Deletes rows that match a condition.
  ```java
  public void delete(Map<String, Object> condition)
  ```

- **rowMatchesCondition**: Helper method to check if a row matches a condition.
  ```java
  private boolean rowMatchesCondition(Row row, Map<String, Object> condition)
  ```

##### Code
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

public class Table {
    private List<Row> rows;

    public Table() {
        this.rows = new ArrayList<>();
    }

    public void insert(Map<String, Object> record) {
        rows.add(new Row(record));
    }

    public List<Map<String, Object>> select() {
        List<Map<String, Object>> result = new ArrayList<>();
        for (Row row : rows) {
            result.add(row.getData());
        }
        return result;
    }

    public void update(Map<String, Object> newValues, Map<String, Object> condition) {
        for (Row row : rows) {
            if (rowMatchesCondition(row, condition)) {
                row.update(newValues);
            }
        }
    }

    public void delete(Map<String, Object> condition) {
        rows.removeIf(row -> rowMatchesCondition(row, condition));
    }

    private boolean rowMatchesCondition(Row row, Map<String, Object> condition) {
        for (String key : condition.keySet()) {
            if (!condition.get(key).equals(row.getData().get(key))) {
                return false;
            }
        }
        return true;
    }
}
```

#### Class: Database

The `Database` class manages multiple tables and provides an interface for CRUD operations on those tables.

##### Attributes
- `Map<String, Table> tables`: Stores the tables in the database.

##### Methods
- **Constructor**: Initializes an empty database.
  ```java
  public Database()
  ```

- **createTable**: Creates a new table in the database.
  ```java
  public void createTable(String tableName)
  ```

- **insert**: Inserts a record into a specified table.
  ```java
  public void insert(String tableName, Map<String, Object> record)
  ```

- **select**: Retrieves all records from a specified table.
  ```java
  public List<Map<String, Object>> select(String tableName)
  ```

- **update**: Updates records in a specified table based on a condition.
  ```java
  public void update(String tableName, Map<String, Object> newValues, Map<String, Object> condition)
  ```

- **delete**: Deletes records from a specified table based on a condition.
  ```java
  public void delete(String tableName, Map<String, Object> condition)
  ```

##### Code
```java
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Database {
    private Map<String, Table> tables;

    public Database() {
        this.tables = new HashMap<>();
    }

    public void createTable(String tableName) {
        tables.put(tableName, new Table());
    }

    public void insert(String tableName, Map<String, Object> record) {
        Table table = tables.get(tableName);
        if (table != null) {
            table.insert(record);
        }
    }

    public List<Map<String, Object>> select(String tableName) {
        Table table = tables.get(tableName);
        if (table != null) {
            return table.select();
        }
        return null;
    }

    public void update(String tableName, Map<String, Object> newValues, Map<String, Object> condition) {
        Table table = tables.get(tableName);
        if (table != null) {
            table.update(newValues, condition);
        }
    }

    public void delete(String tableName, Map<String, Object> condition) {
        Table table = tables.get(tableName);
        if (table != null) {
            table.delete(condition);
        }
    }
}
```

#### Example Usage

Here's an example of how to use the in-memory database:

```java
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        Database db = new Database();
        db.createTable("Users");

        // Insert data
        Map<String, Object> user1 = new HashMap<>();
        user1.put("id", 1);
        user1.put("name", "John Doe");
        user1.put("email", "john@example.com");
        db.insert("Users", user1);

        Map<String, Object> user2 = new HashMap<>();
        user2.put("id", 2);
        user2.put("name", "Jane Doe");
        user2.put("email", "jane@example.com");
        db.insert("Users", user2);

        // Select data
        List<Map<String, Object>> users = db.select("Users");
        System.out.println(users);

        // Update data
        Map<String, Object> newValues = new HashMap<>();
        newValues.put("email", "john.doe@example.com");
        Map<String, Object> condition = new HashMap<>();
        condition.put("id", 1);
        db.update("Users", newValues, condition);

        // Select data after update
        users = db.select("Users");
        System.out.println(users);

        // Delete data
        Map<String, Object> deleteCondition = new HashMap<>();
        deleteCondition.put("id", 2);
        db.delete("Users", deleteCondition);

        // Select data after delete
        users = db.select("Users");
        System.out.println(users);
    }
}
```

#### Summary

This simple in-memory database implementation allows for basic CRUD operations on multiple tables, with a focus on straightforward functionality and ease of use. It demonstrates the fundamental concepts of table management, row manipulation, and querying data, providing a foundation for more advanced database features.