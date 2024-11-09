# Core Java Interview Questions:2
-----------------------------------------------------------------
## 1. Garbage Collection:

### 1. **How does garbage collection work in Java? What is the role of the `finalize` keyword?**

- Garbage collection in Java is a process by which the Java Virtual Machine (JVM) automatically manages memory by reclaiming unused objects.
- The basic principle is to identify objects that are no longer reachable or referenced by any active part of the program and free up the memory occupied by those objects.

Here's how garbage collection typically works in Java:
- The JVM periodically runs a `garbage collector thread` that identifies and marks objects that are reachable (i.e., still in use) through references from active parts of the program, such as local variables, instance variables, and static variables.
- *Objects that are not reachable, either directly or indirectly, are considered garbage.*
- The garbage collector then reclaims the memory occupied by these garbage objects, making it available for new allocations.

#### `finalize`
- The `finalize` method in Java is a mechanism provided by the `Object` class that allows an object to perform cleanup actions before it is garbage collected.
- The `finalize` method is called by the garbage collector before reclaiming an object's memory.
- However, it's important to note that the `finalize` method is generally not recommended for critical cleanup tasks or resource management in Java, as its execution timing is not guaranteed and it may not be called promptly or at all.

##### Cleanup tasks: 
- Clean-up actions refer to tasks or operations that need to be performed before an object is garbage collected or when resources associated with an object need to be released.
- These actions are typically related to resource management, such as `closing files`, `releasing database connections`, or `freeing native resources`.
-----------------------------------------------------------------------------
### 2. **What algorithm does the JVM use for garbage collection?**
- The JVM typically uses a combination of garbage collection algorithms to manage memory efficiently.

Some common garbage collection algorithms used by modern JVM implementations include:
#### **Young Generation Collection (Minor GC):** 
- Uses algorithms like the **Copying** or **Mark-Sweep-Compact** algorithm for the young generation, where newly created objects reside.
- The goal is to quickly reclaim short-lived objects.

#### **Old Generation Collection (Major GC or Full GC):** 
- Uses algorithms like the **Mark-Sweep** or **Mark-Sweep-Compact** algorithm for the old generation, where long-lived objects reside.
- This process is triggered less frequently and involves reclaiming memory from long-lived objects.

#### **Generational Garbage Collection:** 
- The JVM utilizes generational garbage collection strategies, where objects are categorized based on their age (young generation and old generation), allowing for more efficient garbage collection.
-----------------------------------------------------------------------
### 3. **How can memory leaks occur in Java even with automatic garbage collection?**

Memory leaks in Java can occur despite having automatic garbage collection due to various reasons:
#### **Unclosed Resources:** 
- Failing to close resources such as files, streams, database connections, or network sockets after use can lead to memory leaks.
- These resources may hold native memory or system resources that are not managed by the JVM's garbage collector.

#### **Static References:** 
- Objects referenced by static variables or long-lived data structures may unintentionally prevent them from being garbage collected, leading to memory leaks if these references are not properly managed or released.


### To avoid memory leaks, it's important to:
- Properly manage and close resources using `try-with-resources` or `finally` blocks.
- Minimize the use of static variables and ensure they are released when no longer needed.
- Use efficient data structures and avoid unnecessary object retention.
- Pay attention to native memory usage and ensure proper cleanup and management when interfacing with native code.
-----------------------------------------------------------------------------------------------------
### Static and memory relation: 
- In Java, the `static` keyword is used to create static variables, methods, and blocks. 
- Static members are associated with the class itself rather than with specific instances of the class.

Here's the relationship between `static` and memory in Java:

##### 1. **Static Variables (Class Variables):** 
- Static variables are stored in the **`method area`** (also known as the "`Class Area`" or "`Static Area`") of the JVM's memory.
- This area is shared among all instances of the class and is used to store class-level data, including static variables, constant pool information, method bytecode, and other metadata related to the class.

   ```java
   public class MyClass {
       static int count; // Static variable
   }
   ```

In this example, the `count` static variable is stored in the method area and is shared among all instances of the `MyClass` class.

##### 2. **Static Methods:** 
- Static methods are also stored in the **`method area`** along with static variables.
- They can be called using the class name (e.g., `MyClass.staticMethod()`) without requiring an instance of the class.

   ```java
   public class MyClass {
       static void staticMethod() {
           // Static method implementation
       }
   }
   ```

Static methods do not operate on instance-specific data and are often used for utility methods or operations that do not require access to instance variables.

##### 3. **Static Blocks:** 
- Static initialization blocks (`static { ... }`) are used to initialize static variables or perform static initialization tasks when the class is loaded into memory.
- These blocks are executed once when the class is first loaded.

   ```java
   public class MyClass {
       static {
           // Static initialization block
       }
   }
   ```

Static blocks are executed in the order they appear in the class and are typically used for initializing static variables or setting up static resources.
| The garbage collector does not manage the Class area of the Java Virtual Machine (JVM). The Class area, also known as the method area or static area, is a part of the JVM's memory where class-level data and metadata are stored. This area is primarily responsible for storing information related to classes, methods, static variables, constant pool data, and other static structures.    | 
| -------------------------------------------------------------------------------------------------------------------------------------|

| The garbage collector in Java primarily deals with the memory used for object instances, which includes the heap memory.The heap memory is divided into different generations, such as the Young Generation and the Old Generation (Tenured Generation), where objects are allocated and managed by the garbage collector based on their age and usage patterns. |
|-------------------------------------------------------------------------------------------------------------------------------------|
### Generations:
Regarding the memory species in Java, the JVM manages memory in different generations, primarily the Young Generation and the Old Generation (also known as the Tenured Generation):

1. **Young Generation:** The Young Generation is where newly allocated objects are initially placed. It consists of two spaces:
   - **Eden Space:** Newly created objects are allocated in the Eden space. Most objects die young and are garbage collected from the Eden space.
   - **Survivor Spaces (S0 and S1):** After surviving a garbage collection in the Eden space, objects are moved to one of the Survivor spaces. The Survivor spaces are used for minor garbage collection and for aging objects before they are promoted to the Old Generation.

2. **Old Generation (Tenured Generation):** The Old Generation (Tenured Generation) is where long-lived objects reside. Objects that survive multiple garbage collections in the Young Generation are eventually promoted to the Old Generation. Major garbage collections (Full GC) are performed in the Old Generation.

The JVM uses generational garbage collection strategies, such as the Young Generation Collection (Minor GC) and Old Generation Collection (Major GC), to efficiently manage memory and reclaim unused objects. Objects that are no longer reachable are garbage collected, freeing up memory for new allocations.
-------------------------------------------------------------------------------------------------------------------------
## 4. Immutable Class
- An immutable class in Java is a class whose instances cannot be modified after they are created. This means that once an object of an immutable class is created, its state (i.e., its instance variables or fields) cannot be changed.
- Immutable classes are often used for objects whose state should remain constant throughout their lifetime, providing benefits such as thread safety, simplicity, and ease of understanding.

To create an immutable class in Java, follow these guidelines:

- 1. **Make the class final**: This prevents the class from being subclassed, which could potentially lead to mutable behavior if the subclass overrides methods.

- 2. **Make fields private and final**: Private fields ensure encapsulation, and final fields prevent them from being modified after object creation.

- 3. **Do not provide setter methods**: Since the fields are final, there's no need for setter methods. Initialization should be done through the constructor.

- 4. **Avoid returning mutable objects**: If your immutable class contains references to mutable objects (e.g., collections), make sure to return copies or immutable views of these objects to maintain immutability.

Here's an example of an immutable class representing a Person:

```java
public final class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

In this example:

- `Person` is declared as `final` to prevent subclassing.
- `name` and `age` fields are declared as `private final` to make them immutable.
- Constructor initializes these fields.
- Getter methods provide `read-only` access to the fields.
- There are no setter methods, ensuring the fields cannot be modified once an object is created.

Immutable classes like `Person` are thread-safe by default because their state cannot change, making them safe to use in concurrent environments without synchronization concerns.
------------------------------
- In an immutable class, the usual approach is to provide only getter methods for accessing the fields and not provide setter methods for modifying the fields.
- This is because the main characteristic of an immutable class is that its state cannot be changed after instantiation.
----------------------------------------------------------------------------------
## 5. Second largest element in an array:
```java
public static int printNum(int... nums) {
        int Max = nums[0];
        int prevmax = Integer.MIN_VALUE;

        for (int i = 1; i < nums.length; i++) {
            if (Max < nums[i]) {
                prevmax = Max;
                Max = nums[i];
            }
        }
        return prevmax;
}
```
-------------------------------------------------------------------------
## 6. Java 11 features:

1. **Local-Variable Syntax for Lambda Parameters (var)**: Allows using `var` in lambda expressions to infer the type of parameters.
   
2. **String Methods for Empty, Blank, and Lines**: Added methods to the `String` class for checking emptiness, blankness, and handling lines.

3. **HTTP Client (java.net.http)**: New built-in HTTP client to make HTTP requests and handle responses.

4. **Single-File Source-Code Execution**: Run Java code directly from a single source file without compiling it.

5. **Nest-Based Access Control**: Allows classes that are logically part of the same code entity to be nested and accessed privately.

These features, along with others like enhancements in garbage collection, updates to the Java Flight Recorder, and improvements in the JDK itself, make Java 11 a significant release in terms of developer productivity and performance.

-----------------------------------------------------------------------------------
## 8. MEthods of JPA Repository:
In Spring Data JPA, the `JpaRepository` interface provides several methods out of the box for performing CRUD (Create, Read, Update, Delete) operations on entities. Here are some of the commonly used methods of `JpaRepository`:

1. **Save**:
   - `save(S entity)` and `saveAll(Iterable<S> entities)`: Saves one entity or a collection of entities. If the entity already exists (based on the primary key), it updates the existing entity; otherwise, it inserts a new entity.

2. **Find**:
   - `findById(ID id)`: Finds an entity by its primary key (ID).
   - `findAll()`: Retrieves all entities from the database.
   - `findAllById(Iterable<ID> ids)`: Retrieves entities by their primary keys (IDs).

3. **Count and Existence Check**:
   - `count()`: Returns the number of entities in the database.
   - `existsById(ID id)`: Checks if an entity with the specified ID exists in the database.

4. **Delete**:
   - `deleteById(ID id)`: Deletes an entity by its primary key (ID).
   - `delete(T entity)` and `deleteAll(Iterable<T> entities)`: Deletes one entity or a collection of entities.
   - `deleteAll()`: Deletes all entities from the database.

5. **Query Methods**:
   - Spring Data JPA allows you to define query methods based on method names. For example:
     ```java
     List<User> findByLastName(String lastName);
     List<User> findByAgeGreaterThan(int age);
     ```

6. **Derived Queries**:
   - You can create derived queries by using keywords like `And`, `Or`, `Like`, `IsNotNull`, `IsNull`, `OrderBy`, etc., in the method names. For example:
     ```java
     List<User> findByFirstNameAndLastName(String firstName, String lastName);
     List<User> findByAgeGreaterThanAndCityOrderByLastNameAsc(int age, String city);
     ```

7. **Custom Queries**:
   - You can define custom query methods using `@Query` annotation and write JPQL (Java Persistence Query Language) or native SQL queries. For example:
     ```java
     @Query("SELECT u FROM User u WHERE u.age >= :minAge")
     List<User> findByMinAge(@Param("minAge") int minAge);
     ```

These are some of the commonly used methods provided by the `JpaRepository` interface. They allow you to interact with the underlying database and perform CRUD operations on entities without writing boilerplate SQL queries.

----------------------------------------------------
## 9. 5. How to send status code to client from springboot backend?

`ResponseEntity` in Spring is a class that represents an HTTP response. It provides more flexibility and control over the response that your Spring MVC or Spring Boot application sends back to the client compared to returning a simple object directly from a controller method. Here's a brief explanation of `ResponseEntity`:

1. **Customized HTTP Response**:
   - `ResponseEntity` allows you to customize various aspects of the HTTP response, such as status code, headers, and response body.

2. **Status Code**:
   - You can set the HTTP status code (e.g., 200 OK, 404 Not Found, 500 Internal Server Error) using methods like `ok()`, `status(HttpStatus status)`, `status(int statusCode)`, etc.

3. **Headers**:
   - You can add custom HTTP headers to the response using methods like `header(String headerName, String headerValue)`, `headers(HttpHeaders headers)`, etc.

4. **Response Body**:
   - You can set the response body by passing an object or data to the constructor or using methods like `body(T body)`.

5. **Usage in Controllers**:
   - In Spring MVC or Spring Boot controllers, you can return `ResponseEntity` from handler methods to send customized HTTP responses.

6. **Example**:
   ```java
   import org.springframework.http.HttpStatus;
   import org.springframework.http.ResponseEntity;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.RestController;

   @RestController
   public class MyController {

       @GetMapping("/api/data")
       public ResponseEntity<String> getData() {
           String responseData = "Hello from the backend!";
           return ResponseEntity.ok(responseData); // Returns 200 OK with response body
       }

       @GetMapping("/api/error")
       public ResponseEntity<String> getError() {
           return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Resource not found"); // Returns 404 with response body
       }
   }
   ```

In this example:
- The `getData` method returns a response with status 200 OK and a response body "Hello from the backend!" using `ResponseEntity.ok()`.
- The `getError` method returns a response with status 404 Not Found and a response body "Resource not found" using `ResponseEntity.status(HttpStatus.NOT_FOUND).body()`.

Overall, `ResponseEntity` is a powerful tool in Spring for creating custom HTTP responses with specific status codes, headers, and response bodies based on your application's requirements.

------------------------------------------------------

## 10. Exception handling with 10 different test cases of different exception types
Certainly! Exception handling is crucial in Java to handle unexpected situations or errors gracefully. Here are 10 different test cases demonstrating how to handle various exception types in Java:

1. **NullPointerException**:
   ```java
   public void testNullPointerException() {
       try {
           String str = null;
           str.length(); // This will throw NullPointerException
       } catch (NullPointerException e) {
           // Handle NullPointerException
           System.out.println("Caught NullPointerException: " + e.getMessage());
       }
   }
   ```

2. **NumberFormatException**:
   ```java
   public void testNumberFormatException() {
       try {
           String str = "abc";
           int num = Integer.parseInt(str); // This will throw NumberFormatException
       } catch (NumberFormatException e) {
           // Handle NumberFormatException
           System.out.println("Caught NumberFormatException: " + e.getMessage());
       }
   }
   ```

3. **ArrayIndexOutOfBoundsException**:
   ```java
   public void testArrayIndexOutOfBoundsException() {
       try {
           int[] arr = {1, 2, 3};
           int num = arr[3]; // This will throw ArrayIndexOutOfBoundsException
       } catch (ArrayIndexOutOfBoundsException e) {
           // Handle ArrayIndexOutOfBoundsException
           System.out.println("Caught ArrayIndexOutOfBoundsException: " + e.getMessage());
       }
   }
   ```

4. **FileNotFoundException**:
   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;

   public void testFileNotFoundException() {
       try {
           File file = new File("nonexistent.txt");
           FileInputStream fis = new FileInputStream(file); // This will throw FileNotFoundException
       } catch (FileNotFoundException e) {
           // Handle FileNotFoundException
           System.out.println("Caught FileNotFoundException: " + e.getMessage());
       }
   }
   ```

5. **ArithmeticException**:
   ```java
   public void testArithmeticException() {
       try {
           int result = 10 / 0; // This will throw ArithmeticException
       } catch (ArithmeticException e) {
           // Handle ArithmeticException
           System.out.println("Caught ArithmeticException: " + e.getMessage());
       }
   }
   ```

6. **ClassNotFoundException**:
   ```java
   public void testClassNotFoundException() {
       try {
           Class.forName("com.example.NonExistentClass"); // This will throw ClassNotFoundException
       } catch (ClassNotFoundException e) {
           // Handle ClassNotFoundException
           System.out.println("Caught ClassNotFoundException: " + e.getMessage());
       }
   }
   ```

7. **IOException**:
   ```java
   import java.io.IOException;
   import java.nio.file.Files;
   import java.nio.file.Paths;

   public void testIOException() {
       try {
           Files.readAllLines(Paths.get("nonexistent.txt")); // This will throw IOException
       } catch (IOException e) {
           // Handle IOException
           System.out.println("Caught IOException: " + e.getMessage());
       }
   }
   ```

8. **IndexOutOfBoundsException**:
   ```java
   public void testIndexOutOfBoundsException() {
       try {
           String str = "abc";
           char ch = str.charAt(10); // This will throw IndexOutOfBoundsException
       } catch (IndexOutOfBoundsException e) {
           // Handle IndexOutOfBoundsException
           System.out.println("Caught IndexOutOfBoundsException: " + e.getMessage());
       }
   }
   ```

9. **IllegalArgumentException**:
   ```java
   public void testIllegalArgumentException() {
       try {
           int num = -5;
           if (num < 0) {
               throw new IllegalArgumentException("Number cannot be negative");
           }
       } catch (IllegalArgumentException e) {
           // Handle IllegalArgumentException
           System.out.println("Caught IllegalArgumentException: " + e.getMessage());
       }
   }
   ```

10. **RuntimeException**:
    ```java
    public void testRuntimeException() {
        try {
            int[] arr = {1, 2, 3};
            int num = arr[3]; // This will throw ArrayIndexOutOfBoundsException (a type of RuntimeException)
        } catch (RuntimeException e) {
            // Handle RuntimeException
            System.out.println("Caught RuntimeException: " + e.getMessage());
        }
    }
    ```

Each test case demonstrates catching and handling a specific type of exception. You can customize the handling logic as per your application's requirements in the catch block of each test case.

--------------------------------------------------------------------
## 11. Comparable and Comparator interfaces
In Java, the concepts of `Comparator` and `Comparable` are fundamental for sorting and ordering objects. Let's break down each concept step by step with examples:

### Comparable Interface:
The `Comparable` interface is used to define the natural ordering of objects. If a class implements the `Comparable` interface, it means its instances can be compared with each other. The `Comparable` interface has one method, `compareTo()`, which returns a negative integer, zero, or a positive integer as this object is less than, equal to, or greater than the specified object.

#### Example:
Let's say we have a class `Student` and we want to compare students based on their roll numbers.

```java
public class Student implements Comparable<Student> {
    private int rollNumber;

    // Constructor
    public Student(int rollNumber) {
        this.rollNumber = rollNumber;
    }

    // Getter for rollNumber
    public int getRollNumber() {
        return rollNumber;
    }

    @Override
    public int compareTo(Student otherStudent) {
        return this.rollNumber - otherStudent.rollNumber;
    }
}
```

In this example, the `Student` class implements the `Comparable` interface and overrides the `compareTo()` method to compare two `Student` objects based on their roll numbers.

### Comparator Interface:
The `Comparator` interface is used to define custom comparison logic for objects that do not have a natural ordering or for defining alternative orderings. Unlike `Comparable`, which is implemented by the object being compared, `Comparator` is implemented by a separate class.

#### Example:
Let's say we have a class `Employee` and we want to compare employees based on their salaries.

```java
import java.util.Comparator;

public class Employee {
    private String name;
    private double salary;

    // Constructor and other methods...

    // Getter for salary
    public double getSalary() {
        return salary;
    }

    // Comparator for comparing employees by salary
    public static Comparator<Employee> SalaryComparator = new Comparator<Employee>() {
        @Override
        public int compare(Employee emp1, Employee emp2) {
            return Double.compare(emp1.getSalary(), emp2.getSalary());
        }
    };
}
```

In this example, we define a `Comparator` named `SalaryComparator` which compares `Employee` objects based on their salaries.

### Usage:
Now let's see how we can use both `Comparable` and `Comparator`:

```java
import java.util.Arrays;
import java.util.List;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        // Example with Comparable
        List<Student> students = Arrays.asList(
            new Student(3),
            new Student(1),
            new Student(2)
        );
        Collections.sort(students);
        System.out.println("Sorted Students (by roll number):");
        for (Student student : students) {
            System.out.println(student.getRollNumber());
        }

        // Example with Comparator
        List<Employee> employees = Arrays.asList(
            new Employee("Alice", 50000),
            new Employee("Bob", 30000),
            new Employee("Charlie", 40000)
        );
        Collections.sort(employees, Employee.SalaryComparator);
        System.out.println("Sorted Employees (by salary):");
        for (Employee employee : employees) {
            System.out.println(employee.getName() + ": " + employee.getSalary());
        }
    }
}
```

In this example, we have sorted a list of `Student` objects using the natural ordering defined by the `Comparable` interface, and a list of `Employee` objects using the custom ordering defined by the `Comparator` interface.

This demonstrates how `Comparable` and `Comparator` interfaces provide flexibility in sorting objects based on either their natural ordering or custom criteria.
------------------------------------------------------------------------------------

-----------------------------------------------------------------------------
## 14. try with multicatch::?
Multicatch, introduced in Java 7, allows you to catch multiple types of exceptions in a single catch block. This feature simplifies exception handling by reducing code duplication. Instead of having separate catch blocks for each type of exception, you can catch them all at once.

Here's the basic syntax:

```java
try {
    // Some code that may throw exceptions
} catch (ExceptionType1 | ExceptionType2 | ... | ExceptionTypeN e) {
    // Handle the exception
}
```

Each exception type in the catch block is separated by a vertical bar (`|`). When an exception occurs within the try block, Java checks if the thrown exception matches any of the specified types. If it does, the corresponding catch block is executed.

Here's an example:

```java
import java.io.*;

public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            // Some code that may throw exceptions
            BufferedReader reader = new BufferedReader(new FileReader("file.txt"));
            String line = reader.readLine();
            System.out.println("First line: " + line);
            reader.close();
        } catch (FileNotFoundException | IOException e) {
            // Handle file-related exceptions
            System.err.println("File not found or I/O error: " + e.getMessage());
        }
    }
}
```

In this example, the `main()` method attempts to read the first line from a file (`file.txt`). It catches both `FileNotFoundException` and `IOException` in the same catch block.

However, there are a few rules to consider when using multicatch:

1. **Ordering**: The order of the exception types matters. If a superclass and subclass are caught, the catch block for the superclass must appear after the subclass. Otherwise, it will result in a compile-time error because the catch for the superclass would catch all exceptions, making the catch for the subclass unreachable.

2. **Unreachable Catch Blocks**: If an exception type is a subclass of another exception type already caught, the catch block for the subclass will be unreachable and will result in a compile-time error.

Here's an example illustrating these rules:

```java
try {
    // Some code that may throw exceptions
} catch (FileNotFoundException | IOException e) { // OK
    // Handle file-related exceptions
} catch (IOException | FileNotFoundException e) { // Error: Unreachable catch block
    // Handle file-related exceptions
}
```

In this case, the second catch block will result in a compilation error because `FileNotFoundException` is a subclass of `IOException`, and the first catch block already catches `IOException`. Therefore, the second catch block is unreachable.
--------------------------------------------------------
## 14. Weak references vs soft references vs strong references in java?
In Java, references are used to refer to objects in memory. Understanding the differences between weak references, soft references, and strong references is crucial for proper memory management in Java applications.

### Strong References:
- **Strong references** are the most common type of reference in Java.
- When an object is referenced by a strong reference, it won't be garbage collected as long as the reference exists.
- Most objects in Java are accessed through strong references.
- Strong references are created when you assign an object to a variable using the assignment operator (`=`) or when an object is passed as an argument to a method.
- Example:
  ```java
  Object obj = new Object(); // Strong reference
  ```

### Weak References:
- **Weak references** allow objects to be garbage collected as soon as they are no longer strongly reachable.
- Objects referenced only by weak references are eligible for garbage collection even if the JVM determines that memory is not low.
- Weak references are useful for implementing caches or mappings where you don't want to prevent objects from being garbage collected when they are no longer in use.
- Weak references are created using the `WeakReference` class.
- Example:
  ```java
  WeakReference<Object> weakRef = new WeakReference<>(obj);
  ```

### Soft References:
- **Soft references** are similar to weak references but are only garbage collected when memory is low.
- Objects referenced by soft references are retained until the JVM determines that memory is low and the objects are not strongly referenced elsewhere in the application.
- Soft references are useful for implementing memory-sensitive caches or data structures.
- Soft references are created using the `SoftReference` class.
- Example:
  ```java
  SoftReference<Object> softRef = new SoftReference<>(obj);
  ```

### Comparison:
|                  | Strong References  | Weak References    | Soft References    |
|------------------|--------------------|--------------------|--------------------|
| Garbage Collection | Not eligible for GC until no longer referenced | Eligible for GC as soon as no strong references | Garbage collected when memory is low |
| Use Cases       | Regular object access | Implementing caches or mappings | Memory-sensitive caching |
| Creation        | Default, via assignment or method parameters | Using `WeakReference` class | Using `SoftReference` class |
| Cache Behavior  | Objects remain in cache until explicitly removed | Objects quickly removed from cache | Objects retained until memory pressure |

In summary, strong references keep objects in memory until they are no longer needed, while weak references and soft references provide more flexible memory management options, allowing objects to be garbage collected under specific conditions. Weak references are suitable for short-lived caches or mappings, while soft references are more appropriate for long-lived caches where you want objects to be retained until memory pressure increases.
--------------------------------------------------------
## 15. can we create a server in java without using spring framewprk?
Yes, you can create a server in Java without using the Spring Framework. Java provides built-in APIs for networking that allow you to create servers and handle client connections. One of the most commonly used APIs for this purpose is the `java.net` package.

Here's a simple example of how you can create a basic server using Java's `ServerSocket` class:

```java
import java.io.*;
import java.net.*;

public class SimpleServer {
    public static void main(String[] args) {
        int port = 8080; // Port number to listen on
        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("Server started on port " + port);
            
            while (true) {
                // Wait for a client to connect
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client connected: " + clientSocket.getInetAddress());

                // Handle client request in a new thread
                Thread clientThread = new Thread(() -> {
                    try {
                        // Create input and output streams for communication with the client
                        BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                        PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

                        // Read client request and send response
                        String request = in.readLine();
                        System.out.println("Received request from client: " + request);
                        out.println("Hello, client! You said: " + request);

                        // Close streams and socket
                        in.close();
                        out.close();
                        clientSocket.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                });
                clientThread.start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we create a server that listens for client connections on port 8080. When a client connects, the server creates a new thread to handle the client's request. The server then reads the request from the client, sends a response, and closes the connection.

You can compile and run this code using standard Java tools (`javac` to compile and `java` to run). This simple server demonstrates the basic principles of socket programming in Java without relying on any external frameworks like Spring.

-------------------------------------------------------------
## 16. Is Java 100% OOPS?
Java is often described as an "object-oriented programming (OOP) language," but whether it is 100% OOP depends on how strictly you define "object-oriented."

Java is heavily influenced by the principles of OOP, and it was designed to support object-oriented programming paradigms. Many of its features, such as classes, objects, inheritance, polymorphism, encapsulation, and abstraction, align with the core principles of OOP. Additionally, Java encourages the use of OOP concepts to write modular, reusable, and maintainable code.

However, Java also incorporates elements from other programming paradigms, such as procedural programming and functional programming. For example, Java supports procedural programming through static methods and fields, and it has introduced functional programming features such as lambda expressions and the Stream API in more recent versions.

Therefore, while Java is predominantly an object-oriented language and encourages developers to follow OOP principles, it is not strictly 100% object-oriented due to the inclusion of features from other paradigms. Nonetheless, it remains one of the most popular languages for object-oriented programming.
----------------------------------------------------------------------
## 17. Usecases of OOPS in enterprise projects?
Object-oriented programming (OOP) is widely used in enterprise projects due to its ability to model complex systems in a modular and maintainable way. Here are some common use cases of OOP in enterprise projects:

1. **Modularity and Reusability**: OOP allows developers to break down complex systems into smaller, more manageable modules called classes. These classes encapsulate data and behavior related to specific entities or concepts within the system. This modularity promotes code reuse, as classes can be easily reused in different parts of the system or in other projects.

2. **Abstraction and Encapsulation**: OOP encourages the use of abstraction to represent real-world entities as objects with well-defined interfaces. Abstraction hides the implementation details of an object's behavior, allowing developers to focus on how objects interact with each other rather than the specifics of their implementation. Encapsulation ensures that an object's internal state is protected from unauthorized access, enhancing data security and preventing unintended modifications.

3. **Inheritance and Polymorphism**: Inheritance allows classes to inherit properties and behavior from parent classes, enabling code reuse and promoting a hierarchical organization of classes. Polymorphism allows objects of different classes to be treated interchangeably through a common interface, simplifying code and promoting flexibility. These features facilitate the creation of flexible and extensible systems that can easily adapt to changing requirements.

4. **Design Patterns**: OOP provides a foundation for implementing and applying design patterns, which are proven solutions to common software design problems. Design patterns encapsulate best practices for structuring and organizing code, promoting code maintainability, scalability, and flexibility. Some commonly used design patterns in enterprise projects include the Factory, Singleton, Observer, and Strategy patterns.

5. **User Interface Development**: OOP is widely used in the development of user interfaces (UIs) for enterprise applications. UI frameworks such as JavaFX and Swing leverage OOP concepts to create reusable UI components (e.g., buttons, text fields, and menus) and facilitate event-driven programming. OOP enables the creation of modular and extensible UIs that can be easily customized and adapted to meet user needs.

6. **Database Modeling**: OOP concepts are often used to model database schemas and represent data entities in enterprise applications. Object-relational mapping (ORM) frameworks such as Hibernate and JPA allow developers to map Java classes to database tables, enabling seamless interaction between object-oriented code and relational databases. OOP promotes a natural mapping between business objects and database entities, simplifying database access and manipulation.

Overall, OOP plays a crucial role in the development of enterprise projects by providing a robust and flexible framework for building scalable, maintainable, and extensible software systems. Its principles and features are widely adopted across various industries and domains, making it an indispensable tool for modern software development.
------------------------------------------------------------------
## 18. Runnable in java:
- Runnable is a functional interface in Java that represents a task that can be executed by a thread.
- It is defined in the `java.lang` package and has single method `run` that does not take any arguments and does not return any value. 

Here's a basic example of how to use `Runnable`:

### Example 1: Basic Runnable Implementation

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an instance of MyRunnable
        Runnable runnable = new MyRunnable();
        
        // Create a thread and pass the runnable to it
        Thread thread = new Thread(runnable);
        
        // Start the thread
        thread.start();
    }
}
```

### Example 2: Runnable Using Lambda Expression

With Java 8, you can use lambda expressions to make the code more concise.

```java
public class Main {
    public static void main(String[] args) {
        // Create a runnable using lambda expression
        Runnable runnable = () -> {
            System.out.println("Runnable is running using lambda expression");
        };
        
        // Create a thread and pass the runnable to it
        Thread thread = new Thread(runnable);
        
        // Start the thread
        thread.start();
    }
}
```

### Example 3: Runnable with Multiple Threads

This example shows how to use multiple threads with `Runnable`.

```java
class MyRunnable implements Runnable {
    private String message;
    
    public MyRunnable(String message) {
        this.message = message;
    }

    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(message + " - " + i);
            try {
                Thread.sleep(500); // Sleep for 500 milliseconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Create two runnable instances
        Runnable runnable1 = new MyRunnable("Thread 1");
        Runnable runnable2 = new MyRunnable("Thread 2");
        
        // Create two threads
        Thread thread1 = new Thread(runnable1);
        Thread thread2 = new Thread(runnable2);
        
        // Start the threads
        thread1.start();
        thread2.start();
    }
}
```

In these examples, you can see how to define a `Runnable`, create a `Thread` with that `Runnable`, and start the `Thread`. The `Runnable` interface provides a way to encapsulate a task that can be executed concurrently by a thread, allowing you to perform multiple tasks simultaneously.

--------------------------------------------------------------
## 19. Serializable in Java:
- `Serializable` is a `marker interface` in java that is used to indocate that a class can be serialized.
- **Serialization is the process of converting an object into a byte stream, which can then be stored in a file, sent over the network.**
- The byte stream has all the information about the object.
- `DeSerializable` is the reverse process, where the byte stream is used to recreate the actual java object in memory.

Here is a basic guide and examples on how to use `Serializable` in Java:

### Basic Example of Serializable

1. **Define a Class that Implements `Serializable`:**

```java
import java.io.Serializable;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L; // This is used for version control

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

2. **Serialize an Object:**

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class SerializeExample {
    public static void main(String[] args) {
        Person person = new Person("John Doe", 30);

        try (FileOutputStream fileOut = new FileOutputStream("person.ser");
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
            out.writeObject(person);
            System.out.println("Serialized data is saved in person.ser");
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

3. **Deserialize an Object:**

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;

public class DeserializeExample {
    public static void main(String[] args) {
        Person person = null;

        try (FileInputStream fileIn = new FileInputStream("person.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            person = (Person) in.readObject();
        } catch (IOException i) {
            i.printStackTrace();
        } catch (ClassNotFoundException c) {
            System.out.println("Person class not found");
            c.printStackTrace();
        }

        System.out.println("Deserialized Person...");
        System.out.println(person);
    }
}
```

### Important Points

- **`serialVersionUID`:** This is a unique identifier for each class. It is used during the deserialization process to ensure that the sender and receiver of a serialized object have loaded classes for that object that are compatible with respect to serialization. If you do not explicitly declare a `serialVersionUID`, JVM will do it for you automatically, based on various aspects of the class. However, it is strongly recommended that you declare it explicitly to avoid unexpected `InvalidClassException` during deserialization.

- **Transient Fields:** If there are fields in your class that you do not want to serialize, you can mark them as `transient`. These fields will not be included in the serialized form of the object.

```java
import java.io.Serializable;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    
    private String name;
    private int age;
    private transient String password; // This field will not be serialized

    public Person(String name, int age, String password) {
        this.name = name;
        this.age = age;
        this.password = password;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + ", password='" + password + "'}";
    }
}
```

### Custom Serialization

If you need to control the serialization process more closely, you can provide your own `writeObject` and `readObject` methods in your class:

```java
private void writeObject(ObjectOutputStream oos) throws IOException {
    oos.defaultWriteObject();
    // custom code for serialization if needed
}

private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
    ois.defaultReadObject();
    // custom code for deserialization if needed
}
```

This allows you to perform additional tasks during serialization and deserialization, such as encrypting the serialized data or initializing transient fields.

----------------------------------------------------------------


# Java

# Sort custom object using Java8
# Object class and its methods
# Multithreading -> sleep vs wait
# Equals hashcode contract
# Hashset vs Arraylist
# Comparable and comparator
# How to handle and manage exceptions
# What is concurrentexception and how to fx it?
# How to make HashMap synchronized
# Count occurance of each character in a string using stream API
# Garbage Collection -> How to make objects unreferenced for garbage collection
# 


# SB 
## Write API to retrieve userdata based on userId
## Autowire username and password
## 2 RestTemplate and timeout 20 and 50s
## What is cyclic dependency and how to resolve
## How to extract uniqie key from JSON object -> return type set of strings
## How to do logging within your project? -> 
## If there is a multithreaded environment, how will you achieve synchronisation?
## Why cache threadpool is used?


# UNIT TESTING
## How did you optimize the code?
## What is average coverage in your project ? generally above 85%
## 

## Design Pattern:
->Singleton
->Factory
->Adapter

# Managerial Round:

## Project **
## Explain your any work
## What challenges did you face?
## What steps did you take to solve the issue?
## How do you implement test cases in the code?
##  Do you also do deployment
## Have you done any blunder in the code?
## How do you convience your teammates your ideas?
## 
