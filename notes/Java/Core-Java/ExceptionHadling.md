# Exception Handling:

## Exception order:
![image](https://github.com/user-attachments/assets/80c07235-15fb-4ed2-b709-e684d2875e6a)



### 1. Exception Declaration

In Java, exceptions are declared using the `throws` keyword in the method signature. This indicates that a method can throw certain types of exceptions that need to be handled by the calling method or class.

```java
public void myMethod() throws IOException, SQLException {
    // Code that might throw IOException or SQLException
}
```

### 2. Checked and Unchecked Exceptions

#### Checked Exceptions
Checked exceptions are those that the compiler forces you to handle, either by using a `try-catch` block or by declaring them in the method signature with `throws`. They are typically used for exceptional conditions that a program should anticipate and recover from.

**Examples:**
- `IOException`
- `SQLException`

**Example Usage:**

```java
public void readFile(String filePath) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    // Code that might throw IOException
}
```

#### Unchecked Exceptions
Unchecked exceptions are those that the compiler does not force you to handle. They are derived from `RuntimeException` and typically represent programming errors.

**Examples:**
- `NullPointerException`
- `ArrayIndexOutOfBoundsException`

**Example Usage:**

```java
public void accessArray(int[] array, int index) {
    // This might throw ArrayIndexOutOfBoundsException
    int value = array[index];
}
```

### 3. Method Overriding and Exceptions

In method overriding, the overriding method can throw only those exceptions that are specified in the superclass method or exceptions that are subclasses of those exceptions.

#### Superclass does not throw exceptions but derived class does:
- **Checked Exception**: This will work because the derived class is allowed to throw more exceptions.
    ```java
    class Superclass {
        public void myMethod() {
            // No exception
        }
    }

    class Subclass extends Superclass {
        @Override
        public void myMethod() throws IOException {
            // Throws a checked exception
        }
    }
    ```

- **Unchecked Exception**: This will also work for the same reason.
    ```java
    class Superclass {
        public void myMethod() {
            // No exception
        }
    }

    class Subclass extends Superclass {
        @Override
        public void myMethod() {
            throw new RuntimeException("Unchecked Exception");
        }
    }
    ```

#### Superclass throws exceptions but derived class does not:
- **Checked Exception**: This will not work because the derived class must handle the checked exceptions declared in the superclass.
    ```java
    class Superclass {
        public void myMethod() throws IOException {
            // Throws a checked exception
        }
    }

    class Subclass extends Superclass {
        @Override
        public void myMethod() {
            // Must handle IOException or declare it
        }
    }
    ```

- **Unchecked Exception**: This will work because the derived class is not required to handle unchecked exceptions.
    ```java
    class Superclass {
        public void myMethod() {
            throw new RuntimeException("Unchecked Exception");
        }
    }

    class Subclass extends Superclass {
        @Override
        public void myMethod() {
            // No exception handling needed
        }
    }
    ```

### 4. Creating Custom Exception

To create a custom exception, extend the `Exception` class or `RuntimeException` depending on whether you want it to be a checked or unchecked exception.

**Example:**

```java
// Checked Exception
public class MyCheckedException extends Exception {
    public MyCheckedException(String message) {
        super(message);
    }
}

// Unchecked Exception
public class MyUncheckedException extends RuntimeException {
    public MyUncheckedException(String message) {
        super(message);
    }
}
```

**Usage:**

```java
public void doSomething() throws MyCheckedException {
    throw new MyCheckedException("This is a custom checked exception");
}

public void doSomethingElse() {
    throw new MyUncheckedException("This is a custom unchecked exception");
}
```

### 5. Global Exception Handler in Spring Boot

In Spring Boot, you can handle exceptions globally using `@ControllerAdvice`. This allows you to handle exceptions across the whole application in one global handling component.

**Example:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAllExceptions(Exception ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
    
    @ExceptionHandler(MyCustomException.class)
    public ResponseEntity<String> handleCustomException(MyCustomException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
    }
}
```

### 6. Handling Exceptions at Controller Level

In Spring Boot, exceptions can also be handled at the controller level using `@ExceptionHandler` within a specific controller class.

**Example:**

```java
@RestController
public class MyController {
    
    @GetMapping("/test")
    public String test() throws MyCustomException {
        if (true) {
            throw new MyCustomException("Custom exception occurred");
        }
        return "Success";
    }
    
    @ExceptionHandler(MyCustomException.class)
    public ResponseEntity<String> handleCustomException(MyCustomException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
    }
}
```

### 7. Annotations for Exception Handling in Spring Boot

**Common Annotations:**
- `@ExceptionHandler`: Handles specific exceptions in a controller or globally.
- `@ControllerAdvice`: Provides global exception handling.
- `@ResponseStatus`: Specifies the HTTP status code to return for a particular exception.

**Example:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public String handleResourceNotFound(ResourceNotFoundException ex) {
        return ex.getMessage();
    }
}
```

This covers the key concepts related to exception handling in Java and Spring Boot. If you need further details or examples, feel free to ask!
