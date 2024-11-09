# Object Oriented Programming System:
--------------------------------------------------------------------------------------

## 1. What will be the output for below code?
```java
import java.util.*;
import java.lang.*;
import java.io.*;

// The main method must be in a class named "Main".

class Base {
    public void print() {
        System.out.println("Base");
    }
}

class Derived extends Base {
    public void print() {
        System.out.print("Derived");
    }
}
class Main {
    public static void main(String[] args) {
       Base x = new Base();
       Base y = new Derived();
       Derived z = new Derived();
      x.print(); // Base
      y.print(); // Derived
      z.print(); //Derived
    }
}
```
__________________________________________________________
## 2. What is Base class?

A base class, also known as a parent class or superclass, is a class from which other classes derive or inherit properties and behavior. In object-oriented programming (OOP) languages like Java, a base class serves as a blueprint for creating other classes.

Key points about base classes:

1. **Inheritance**: Base classes are used in inheritance hierarchies. When a class inherits from a base class, it gains access to the base class's fields, methods, and other members, which can be used directly or overridden.

2. **Code Reusability**: Base classes promote code reusability by allowing common functionalities to be defined in one place (the base class) and reused by multiple derived classes.

3. **Abstractness**: `Base classes can be abstract`, meaning they may have abstract methods that must be implemented by derived classes. Abstract base classes are used to define common interfaces and behaviors without providing specific implementations.

4. **Example**:
   ```java
   // Base class
   public class Shape {
       protected int width;
       protected int height;

       public void setWidth(int width) {
           this.width = width;
       }

       public void setHeight(int height) {
           this.height = height;
       }

       public int area() {
           return width * height;
       }
   }

   // Derived class
   public class Rectangle extends Shape {
       // Additional members and methods specific to Rectangle
   }
   ```

In this example, `Shape` is the base class with `width`, `height`, `setWidth`, `setHeight`, and `area` methods. `Rectangle` is a derived class that inherits these members from `Shape` and can also have its own additional members and methods specific to rectangles.

In summary, a base class provides a foundation for creating related classes with shared properties and behaviors, facilitating code organization, and promoting code reusability in object-oriented programming.

__________________________________________________________
## 3. Base class vs Abstract class?

The main difference between a base class and an abstract class lies in their intended use and implementation:

1. **Base Class**:
   - **A base class, also known as a parent class or superclass, is a regular class that can be instantiated (i.e., objects can be created from it).**
   - It can have both abstract and concrete methods.
   - Concrete methods in a base class have implementations.
   - A base class can be used as a blueprint for creating objects directly.
   - Objects can be created from a base class, and its methods and properties can be accessed and used directly.

2. **Abstract Class**:
   - **An abstract class is a class that cannot be instantiated on its own; it's meant to be extended by other classes.**
   - It can have abstract methods (methods without implementations) as well as concrete methods (methods with implementations).
   - **Abstract methods in an abstract class define a contract that derived classes must implement.**
   - An abstract class is used to define a common interface or behavior that multiple derived classes can share.
   - It serves as a blueprint for other classes but cannot be directly instantiated.

**Example**:

Base Class Example:
```java
public class Animal {
    public void eat() {
        System.out.println("Animal is eating.");
    }
}

// Usage
Animal animal = new Animal();
animal.eat(); // Output: Animal is eating.
```

Abstract Class Example:
```java
public abstract class Shape {
    abstract void draw(); // Abstract method

    public void display() {  //Concrete method: the method which is already implemented
        System.out.println("Displaying shape.");
    }
}

// Derived class
public class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle.");
    }
}

// Usage
Shape shape = new Circle();
shape.draw(); // Output: Drawing circle.
shape.display(); // Output: Displaying shape.
```

In summary, a base class can be instantiated and used directly, while an abstract class cannot be instantiated and is meant to be extended by other classes, providing a common structure and behavior through abstract and concrete methods.



| Aspect                  | Base Class                               | Abstract Class                                 |
|-------------------------|------------------------------------------|------------------------------------------------|
| Instantiation           | Can be instantiated to create objects.   | Cannot be instantiated directly.               |
| Methods                 | Can have both abstract and concrete methods. | Can have abstract methods (without implementation) and concrete methods (with implementation). |
| Usage                   | Used as a blueprint for creating objects. | Used as a blueprint for other classes, defining a common interface or behavior. |
| Abstract Methods        | Not required to have abstract methods.    | Can have abstract methods that must be implemented by derived classes. |
| Concrete Methods        | All methods have implementations.         | Can have concrete methods with implementations. |
| Object Creation          | Directly creates objects of its type.    | Cannot directly create objects of its type; must be extended by other classes. |
__________________________________________________________

## 4. Abstract vs interface 

Here's a comparison between abstract classes and interfaces in Java, along with code examples for each:

1. **Abstract Class**:
   - An abstract class is a class that cannot be instantiated on its own and may contain both abstract and concrete methods.
   - Abstract methods are declared without an implementation and must be implemented by derived classes.
   - Concrete methods in an abstract class have implementations and can be directly used by derived classes.
   - Abstract classes can have `constructors`, `instance variables`, and `non-abstract methods`.

Example of an abstract class:
```java
abstract class Animal {
    String name;

    Animal(String name) {
        this.name = name;
    }

    abstract void makeSound();

    void eat() {
        System.out.println(name + " is eating.");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println(name + " barks.");
    }
}

public class AbstractClassExample {
    public static void main(String[] args) {
        Animal dog = new Dog("Buddy");
        dog.makeSound(); // Output: Buddy barks.
        dog.eat(); // Output: Buddy is eating.
    }
}
```

2. **Interface**:
   - An interface is a reference type in Java that contains only `abstract methods`, `constant variables`, and `default methods` (with implementations starting from Java 8).
   - Interfaces define a contract that classes must adhere to by implementing all the methods defined in the interface.
   - Multiple interfaces can be implemented by a single class, enabling multiple inheritances of behavior.

Example of an interface:
```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing circle.");
    }
}

class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle.");
    }
}

public class InterfaceExample {
    public static void main(String[] args) {
        Shape circle = new Circle();
        circle.draw(); // Output: Drawing circle.

        Shape rectangle = new Rectangle();
        rectangle.draw(); // Output: Drawing rectangle.
    }
}
```

In summary, an abstract class provides a partial implementation and can contain both abstract and concrete methods, while an interface only defines a contract without any implementation and can be implemented by multiple classes.

| Feature             | Interface                                | Abstract Class                                |
|---------------------|------------------------------------------|-----------------------------------------------|
| Definition          | Contains method signatures only, no implementation           | Can contain both method declarations (including abstract methods) and method implementations           |
| Inheritance         | Supports multiple inheritance (can implement multiple interfaces)  | Supports single inheritance (can extend only one abstract class) |
| Constructor         | Cannot have constructors               | Can have constructors                         |
| Fields              | Can only have public static final fields (constants) | Can have fields of any access modifier and type |
| Implementation      | Classes implement interfaces using the `implements` keyword | Subclasses extend abstract classes using the `extends` keyword |
| Multiple Interfaces | A class can implement multiple interfaces | A class can extend only one abstract class but can implement multiple interfaces |
| Purpose             | Used for defining contracts or behavior specifications that classes must follow | Used for code reuse and defining common functionality among related classes |
__________________________________________________________
## 5.functional interface vs Abstract class:

The main difference between a functional interface and an abstract class lies in their purpose, structure, and usage:

1. **Functional Interface**:
- A functional interface is an interface that contains exactly `one abstract method` (SAM), `along with optional default methods and static methods` (starting from Java 8).
- The purpose of a functional interface is to provide a single method for implementation, making it suitable for use with lambda expressions and method references.
- Functional interfaces are used to enable functional programming paradigms in Java, such as passing behavior as arguments and enabling concise code syntax.
- Java provides the `@FunctionalInterface` annotation to explicitly mark an interface as a functional interface, although it's not mandatory.

Example of a functional interface:
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        Calculator add = (a, b) -> a + b;
        System.out.println("Addition: " + add.calculate(5, 3)); // Output: Addition: 8
    }
}
```

2. **Abstract Class**:
- An abstract class is a class that cannot be instantiated on its own and may contain abstract methods (without implementation) as well as concrete methods (with implementation).
- Abstract classes are used to provide a partial implementation and serve as a base for other classes to extend and override methods.
- Unlike functional interfaces, abstract classes can have constructors, instance variables, and non-abstract methods.
- Abstract classes are used when you want to define common behavior and attributes for a group of related classes.

Example of an abstract class:
```java
abstract class Shape {
    abstract void draw();

    void display() {
        System.out.println("Displaying shape.");
    }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle.");
    }
}

public class AbstractClassExample {
    public static void main(String[] args) {
        Shape circle = new Circle();
        circle.draw(); // Output: Drawing circle.
        circle.display(); // Output: Displaying shape.
    }
}
```

In summary, a functional interface is specifically designed for functional programming with a single abstract method, while an abstract class is more general and provides a partial implementation along with the ability to have constructors, variables, and non-abstract methods.
__________________________________________________________
## 6. Marker interface:

**A marker interface in Java is an interface that doesn't declare any methods**. 
- It serves as a marker or tag to indicate a certain capability or characteristic of classes that implement it. The presence of a marker interface on a class indicates to the compiler or runtime environment that the class should be treated in a specific way or should have some special behavior.

Some common uses of marker interfaces include:

#### 1. **Serialization**:
- Java's `Serializable` interface is a marker interface. Classes that implement `Serializable` indicate to Java's serialization mechanism that instances of those classes can be serialized and deserialized.
   - Example:
     ```java
     import java.io.Serializable;

     public class MyClass implements Serializable {
         // Class members and methods
     }
     ```

####2. **Cloning**:
- Java's `Cloneable` interface is another marker interface. It indicates to the `clone()` method that objects of classes implementing `Cloneable` can be cloned using shallow copy semantics.
   - Example:
     ```java
     class Person implements Cloneable {
         // Class members and methods
     }
     ```

#### 3. **Special Processing**:
- Marker interfaces can also be used for indicating that certain classes should undergo special processing or should be handled differently by frameworks or libraries.
   - Example:
     ```java
     public interface Auditable {
         // Marker interface for classes that need auditing
     }

     class Employee implements Auditable {
         // Class members and methods
     }
     ```

In my projects, I've used marker interfaces like `Serializable` and custom marker interfaces for specific purposes. For instance, I've used marker interfaces to indicate that certain classes should be treated differently during serialization or that they require special handling in custom frameworks or modules.

Marker interfaces are a simple yet effective way to convey metadata or characteristics about classes to the Java compiler or runtime environment, enabling more controlled and specialized behavior.

### can you create custom market interface?
Yes, you can create custom marker interfaces in Java. A custom marker interface is an interface that doesn't declare any methods but serves as a marker or tag to indicate a specific capability or characteristic of classes that implement it.

Here's an example of how you can create a custom marker interface:

```java
// Custom marker interface
public interface Auditable {
    // Marker interface doesn't declare any methods
}

// Class implementing the custom marker interface
class Employee implements Auditable {
    private String name;
    private int id;

    // Constructor, getters, setters, and other methods
}

public class CustomMarkerInterfaceExample {
    public static void main(String[] args) {
        Employee emp1 = new Employee("John Doe", 101);
        if (emp1 instanceof Auditable) {
            System.out.println(emp1.getName() + " is auditable.");
        } else {
            System.out.println(emp1.getName() + " is not auditable.");
        }
    }
}
```

In this example, `Auditable` is a custom marker interface that doesn't declare any methods. The `Employee` class implements the `Auditable` interface, indicating that instances of `Employee` are auditable.

You can use custom marker interfaces like `Auditable` to mark certain classes for specific processing or behavior within your application or framework. For example, you might have classes representing entities that require auditing, and by implementing the `Auditable` interface, you signal that these classes should undergo auditing or have specific auditing-related functionalities.
__________________________________________________________
## 7. Method overloading vs overriding?


| Feature               | Method Overloading     Compile Time Polimorphism                | Method Overriding  Run Time Polimorphism                          |
|-----------------------|------------------------------------------|-----------------------------------------------|
| Definition            | Multiple methods with the same name but different parameters or types within the same class | Subclass provides a specific implementation for a method defined in its superclass |
| Inheritance           | Not dependent on inheritance              | Occurs in a subclass inheriting from a superclass |
| Signature             | Methods must have different signatures (determined by parameter types or number) | Method signature (name, parameters) must be the same in the superclass and subclass |
| Return Type           | Can have the same or different return types | Must have the same return type or a covariant subtype in the subclass |
| Access Modifiers      | Can have different access modifiers       | Access modifiers cannot be more restrictive in the subclass |
| Exception Handling    | Can throw different exceptions            | Subclass can throw the same exceptions or a subclass of the exceptions thrown by the superclass |
| Purpose               | Used for creating methods with the same name but different functionality | Used for modifying or extending the behavior of a superclass method in a subclass |

### Method Overloading Example:
- Method overloading occurs when a class has multiple methods with the same name but different parameters.

```java
class Calculator {
    // Method to add two integers
    int add(int a, int b) {
        return a + b;
    }

    // Overloaded method to add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("Sum of 2 numbers: " + calc.add(5, 10));
        System.out.println("Sum of 3 numbers: " + calc.add(5, 10, 15));
    }
}
```

In this example, `Calculator` class has two `add` methods with different parameter lists (`add(int a, int b)` and `add(int a, int b, int c)`), demonstrating method overloading.

### Method Overriding Example:
- Method overriding occurs when a subclass provides a specific implementation for a method that is already defined in its superclass.

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // Overriding the sound method from Animal class
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // Creating a Dog object but using Animal reference
        myAnimal.sound(); // Calls the sound() method of Dog class due to method overriding
    }
}
```

In this example, `Dog` class extends `Animal` class and overrides the `sound` method. When a `Dog` object is created and referenced by an `Animal` reference variable, calling `sound()` invokes the overridden method in the `Dog` class, demonstrating method overriding and runtime polymorphism.

----------------------------------------------------------------

### 8. functional interface: 

- A functional interface in Java is an interface that contains exactly one abstract method **`(SAM)-Single Abstract Method`** along with zero or more default methods or static methods.
- These interfaces are designed to represent behaviors or functionalities as a single unit, making them suitable for use with lambda expressions and method references.

Key characteristics of functional interfaces:

1. **Single Abstract Method (SAM)**:
- A functional interface must have only one abstract method that defines its core functionality.
- Example of a functional interface:
     ```java
     @FunctionalInterface
     interface Calculator {
         int calculate(int a, int b);
     }
     ```

2. **@FunctionalInterface Annotation**:
- The `@FunctionalInterface` annotation is optional but recommended for functional interfaces to ensure they adhere to the single abstract method rule.
- If a functional interface has more than one abstract method, or if it inherits an abstract method from another interface, a compilation error occurs.
   - Example usage:
     ```java
     @FunctionalInterface
     interface Calculator {
         int calculate(int a, int b);
     }
     ```

3. **Lambda Expressions**:
- Functional interfaces are commonly used with lambda expressions, allowing for concise and expressive code for implementing behaviors.
- Example of using a lambda expression with a functional interface:
     ```java
     Calculator add = (a, b) -> a + b;
     System.out.println(add.calculate(5, 3)); // Output: 8
     ```

4. **Default and Static Methods**:
- Functional interfaces can have default methods (with implementations) and static methods, which do not count toward the single abstract method rule.
- Default methods allow adding new methods to existing interfaces without breaking implementations.
- Static methods provide utility methods related to the interface.
- Example with default method:
     ```java
     @FunctionalInterface
     interface Calculator {
         int calculate(int a, int b);

         default void displayResult(int result) {
             System.out.println("Result: " + result);
         }
     }
     ```
# **Example of functional interface with lambda expression:**

- Functional interfaces are fundamental to Java's support for functional programming paradigms introduced in Java 8 and later versions. They provide a standardized way to represent behaviors as objects, facilitating code reuse, modularity, and improved readability.

------------------------------------
### 9. Optional Classes:

- The `Optional` class in Java is a container object that may or may not contain a non-null value. It is primarily used to represent optional values and to avoid null pointer exceptions when working with potentially null objects.

Key points about the `Optional` class:

1. **Avoiding Null Pointer Exceptions**:
- One of the main purposes of `Optional` is to provide a safer alternative to handling potentially null values.
- By using `Optional`, you can check if a value is present before accessing it, reducing the risk of null pointer exceptions.

2. **Creation of Optional Objects**:
- You can create an `Optional` object using static factory methods such as `of`, `ofNullable`, and `empty`.
- Example of creating an `Optional` object:
     ```java
     Optional<String> optionalName = Optional.of("Alice");
     ```

3. **Accessing Optional Values**:
   - You can retrieve the value from an `Optional` object using methods like `get`, `orElse`, `orElseGet`, and `orElseThrow`.
   - Example of accessing an optional value:
     ```java
     Optional<String> optionalName = Optional.of("Alice");
     String name = optionalName.orElse("Unknown");
     System.out.println(name); // Output: Alice
     ```

4. **Checking Presence of Value**:
   - You can check if a value is present in an `Optional` object using methods like `isPresent` and `ifPresent`.
   - Example of checking presence and using `ifPresent`:
     ```java
     Optional<String> optionalName = Optional.ofNullable(null);
     if (optionalName.isPresent()) {
         System.out.println("Name is present: " + optionalName.get());
     } else {
         System.out.println("Name is not present.");
     }
     ```

5. **Chaining Optional Operations**:
   - `Optional` supports chaining of operations using methods like `map`, `flatMap`, `filter`, and `orElseThrow`.
   - Chaining allows for more expressive and concise code when working with optional values.
   - Example of chaining operations:
     ```java
     Optional<String> optionalName = Optional.ofNullable("Alice");
     String upperCaseName = optionalName.map(String::toUpperCase).orElse("Unknown");
     System.out.println(upperCaseName); // Output: ALICE
     ```

6. **Avoiding Null Checks**:
   - Using `Optional` helps avoid excessive null checks in code and promotes a more declarative and expressive style of programming.

Overall, the `Optional` class is a useful tool in Java for handling optional values and dealing with nulls in a more structured and safe manner. It encourages better practices in handling potential absence of values, leading to more robust and readable code.
-------------------------------------------

### 10. Method reference:

A method reference in Java is a shorthand syntax for referring to an existing method or a constructor by its name. It is a way to pass behavior or functionality as an argument to another method, particularly useful when working with lambda expressions and functional interfaces.

Key points about method references:

1. **Syntax**:
   - Method references use the `::` operator to reference a method or a constructor.
   - Syntax: `ClassName::methodName` for static methods, `instance::methodName` for instance methods, `ClassName::new` for constructors.
  
2. **Types of Method References**:
   - **Static Method Reference**: Refers to a static method of a class.
     ```java
     // Example of a static method reference
     Function<Integer, String> intToString = String::valueOf;
     String str = intToString.apply(123); // Equivalent to String.valueOf(123)
     ```

   - **Instance Method Reference**: Refers to an instance method of an object.
     ```java
     // Example of an instance method reference
     List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
     names.forEach(System.out::println); // Equivalent to name -> System.out.println(name)
     ```

   - **Constructor Reference**: Refers to a constructor of a class.
     ```java
     // Example of a constructor reference
     Supplier<List<String>> listSupplier = ArrayList::new;
     List<String> newList = listSupplier.get(); // Equivalent to new ArrayList<>()
     ```

3. **Simplifying Lambda Expressions**:
   - Method references provide a more concise and readable alternative to lambda expressions when the lambda body simply calls a method.
   - Example comparing lambda expression and method reference:
     ```java
     // Lambda expression
     Function<Integer, String> intToStringLambda = (num) -> String.valueOf(num);

     // Method reference
     Function<Integer, String> intToStringReference = String::valueOf;
     ```

4. **Compatible Functional Interfaces**:
   - Method references are compatible with functional interfaces, which are interfaces with a single abstract method.
   - They can be used anywhere a functional interface is expected, such as in stream operations, comparator definitions, etc.

5. **Types of Method References**:
   - **Method Reference to a Static Method**: `ClassName::staticMethodName`
   - **Method Reference to an Instance Method of an Object**: `instance::instanceMethodName`
   - **Method Reference to an Instance Method of a Class**: `ClassName::instanceMethodName`
   - **Constructor Reference**: `ClassName::new`

Overall, method references provide a more compact and readable way to pass behavior around in Java code, especially in the context of functional programming and lambda expressions. They help reduce boilerplate code and improve code maintainability.

###### example of using method references with a custom class:

Let's say we have a `Person` class with an instance method `getName()`:

```java
class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

Now, we can use method references to refer to the `getName()` method of the `Person` class:

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Function;

public class MethodReferenceExample {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Alice"),
            new Person("Bob"),
            new Person("Charlie")
        );

        // Using method reference to refer to instance method getName()
        Function<Person, String> getNameFunction = Person::getName;

        // Applying the method reference to each person in the list
        for (Person person : people) {
            String name = getNameFunction.apply(person);
            System.out.println("Person's name: " + name);
        }
    }
}
```

In this example, `getNameFunction` is a `Function` that takes a `Person` object and returns their name using the `getName()` method. The method reference `Person::getName` is used to create this `Function` instance, and then we apply this `Function` to each `Person` in the list to get their names.
-------------------------------------
### 11. default and static keyword in interface:

Yes, I'm familiar with the `default` and `static` keywords in Java interfaces. These keywords were introduced in Java 8 as part of the enhancements to interfaces.

1. **Default Methods**:
- The `default` keyword is used to define default methods in interfaces. Default methods have a default implementation that can be used by implementing classes.
- Default methods allow interfaces to evolve without breaking existing implementations.
   - Syntax:
     ```java
     public interface MyInterface {
         default void defaultMethod() {
             // Default implementation
         }
     }
     ```
   - Example usage:
     ```java
     public interface Vehicle {
         default void start() {
             System.out.println("Vehicle is starting...");
         }
     }

     public class Car implements Vehicle {
         // No need to implement start() in Car
     }

     // Usage
     Car car = new Car();
     car.start(); // Output: Vehicle is starting...
     ```

2. **Static Methods**:
   - The `static` keyword is used to define static methods in interfaces. Static methods can be called on the interface itself, without requiring an instance of the interface.
   - Static methods in interfaces are often used for utility methods or factory methods.
   - Syntax:
     ```java
     public interface MyInterface {
         static void staticMethod() {
             // Static method implementation
         }
     }
     ```
   - Example usage:
     ```java
     public interface MathOperations {
         static int add(int a, int b) {
             return a + b;
         }
     }

     // Usage
     int result = MathOperations.add(5, 3); // Calling static method without an instance
     System.out.println("Result: " + result); // Output: Result: 8
     ```

Both `default` and `static` methods in interfaces provide additional flexibility and functionality to Java interfaces, making them more powerful and easier to work with, especially in scenarios where backward compatibility and utility methods are required.
------------------------------------------------

## 12. What is Dynamic Binding? [runtime polymorphism]
Dynamic binding, also known as late binding or runtime polymorphism, is a fundamental concept in object-oriented programming languages like Java. It refers to the process where the method or function call associated with a specific object is resolved at runtime rather than at compile time. This enables the selection of the appropriate method implementation based on the actual type of the object being referenced.

Key points about dynamic binding (runtime polymorphism) include:

1. **Method Overriding**:
   - Dynamic binding is closely tied to method overriding, where a subclass provides a specific implementation of a method that is already defined in its superclass.
   - The overridden method in the subclass should have the same name, return type, and parameters as the method in the superclass.

2. **Polymorphic Behavior**:
   - Dynamic binding allows for polymorphic behavior, where the same method call can behave differently based on the actual object type at runtime.
   - This enables flexibility and extensibility in object-oriented designs, as subclasses can customize behavior while adhering to a common interface defined by the superclass.

3. **Late Resolution**:
   - During runtime, the Java Virtual Machine (JVM) resolves method calls based on the actual type of the object rather than the reference type.
   - This late resolution ensures that the most appropriate method implementation (based on the runtime object type) is invoked, leading to dynamic behavior.

4. **Example**:
   Consider a scenario with a superclass `Animal` and subclasses `Dog` and `Cat`, both overriding a method `makeSound()`:
   ```java
   class Animal {
       public void makeSound() {
           System.out.println("Animal makes a sound");
       }
   }

   class Dog extends Animal {
       @Override
       public void makeSound() {
           System.out.println("Dog barks");
       }
   }

   class Cat extends Animal {
       @Override
       public void makeSound() {
           System.out.println("Cat meows");
       }
   }

   public class DynamicBindingExample {
       public static void main(String[] args) {
           Animal dog = new Dog();
           Animal cat = new Cat();

           dog.makeSound(); // Output: Dog barks
           cat.makeSound(); // Output: Cat meows
       }
   }
   ```
   In this example, `dog.makeSound()` and `cat.makeSound()` demonstrate dynamic binding, as the actual method implementations (`bark()` or `meow()`) are determined at runtime based on the runtime types of `dog` and `cat`.

___________
## 13. Singleton classes? how to create? is this thread safe?
A Singleton class in Java is a design pattern that ensures a class has only one instance and provides a global point of access to that instance. This pattern is commonly used in scenarios where you want to control object creation, limit the number of instances, and provide a single point of access to the instance across the application.

To create a Singleton class in Java, you typically follow these steps:

1. **Private Constructor:** Ensure that the class has a private constructor to prevent external instantiation.

2. **Private Static Instance:** Create a private static instance of the class within the class itself.

3. **Public Static Method:** Provide a public static method that returns the singleton instance. This method typically checks if the instance already exists and creates it if it doesn't.

```java
public class Singleton {
    private static final Singleton instance = new Singleton();
    
    // Private constructor to prevent instantiation
    private Singleton() {}
    
    // Public static method to get the singleton instance
    public static Singleton getInstance() {
        return instance;
    }
}
```
------------------------------------
### How to create threaf safe singleton class using double check locking?
To create a thread-safe Singleton class using double-checked locking, you can follow this approach:

```java
public class ThreadSafeSingleton {
    private static volatile ThreadSafeSingleton instance;

    // Private constructor to prevent instantiation
    private ThreadSafeSingleton() {}

    // Public static method to get the singleton instance
    public static ThreadSafeSingleton getInstance() {
        if (instance == null) {
            synchronized (ThreadSafeSingleton.class) {
                if (instance == null) {
                    instance = new ThreadSafeSingleton();
                }
            }
        }
        return instance;
    }
}
```

In this implementation:

- The `instance` variable is declared as `volatile`, ensuring that changes made to it are visible to all threads.
- The `getInstance()` method first checks if the `instance` is `null`. If it is, it enters a synchronized block to ensure that only one thread can create the instance at a time.
- Within the synchronized block, it checks again if the `instance` is `null`. This double check is necessary to prevent multiple threads from creating the instance if they all pass the initial null check simultaneously.

By using `volatile` for the `instance` variable and double-checked locking, this Singleton implementation ensures thread safety and lazy initialization (i.e., the instance is created only when `getInstance()` is called for the first time). However, note that starting from Java 5 and later versions, using `volatile` alone is sufficient for thread-safe lazy initialization without the need for double-checked locking due to improvements in the Java Memory Model.
-------------------------------------------------------------------------
14 43. Why the main method is public and static? public static void main(String args[])
The `main` method in Java is typically declared as `public static void main(String[] args)` for several reasons:

1. **Accessibility:** Declaring the `main` method as `public` allows it to be accessed from outside the class, which is necessary for the Java runtime to locate and execute the entry point of the program.

2. **Static Context:** The `main` method is declared as `static` because it is called by the Java Virtual Machine (JVM) without requiring an instance of the class. This is because the entry point of the program needs to be accessible even before any objects of the class are created.

3. **Return Type:** The return type of `void` indicates that the `main` method does not return any value. Instead, it performs tasks such as initializing the program, processing command-line arguments, and starting the execution flow.

4. **Parameter:** The `String[] args` parameter allows the `main` method to accept command-line arguments when the program is executed from the command line. These arguments can be used to customize the behavior of the program or pass input data.
-------------------------------
###  Can we override or overload main method?
In Java, you can overload the `main` method, but you cannot override it.

- **Overloading:** Overloading refers to defining multiple methods in the same class with the same name but different parameter lists. For example, you can have multiple `main` methods with different parameter types or numbers of parameters. However, only the standard `public static void main(String[] args)` method is recognized by the Java Virtual Machine (JVM) as the entry point of the program when you run the program from the command line.

Here's an example of overloading the `main` method:

```java
public class MainMethodOverloading {
    public static void main(String[] args) {
        System.out.println("This is the main method with String[] args.");
    }

    public static void main(String args) {
        System.out.println("This is an overloaded main method with a single String parameter.");
    }

    public static void main() {
        System.out.println("This is another overloaded main method with no parameters.");
    }
}
```

- **Overriding:** Overriding refers to providing a new implementation for a method in a subclass that is already defined in its superclass. However, since the `main` method is declared as `static`, it belongs to the class itself and not to any specific object instance. Therefore, it cannot be overridden in subclasses.

Attempting to override the `main` method in a subclass will result in a compile-time error, as shown in this example:

```java
public class SubClass extends MainMethodOverloading {
    @Override
    public static void main(String[] args) {
        // Compile-time error: Cannot override the static method from MainMethodOverloading
        System.out.println("This is an overridden main method in the subclass.");
    }
}
```

In summary, while you can overload the `main` method by providing different parameter lists, you cannot override it in subclasses because it is a static method associated with the class itself.
---------------------------------------------------------------------------------------------------

## Why Java doesn't support multiple inheritance?
Java does not support multiple inheritance through classes to avoid complexity and ambiguity known as the "Diamond Problem". The diamond problem arises when a class inherits from two classes that have a common base class, leading to potential conflicts and ambiguity.

### The Diamond Problem Explained

Consider the following scenario in a language that supports multiple inheritance:

```plaintext
       A
      / \
     B   C
      \ /
       D
```

- Class `B` and class `C` both inherit from class `A`.
- Class `D` inherits from both `B` and `C`.

If both `B` and `C` have overridden a method from `A`, and `D` inherits from both `B` and `C`, there is ambiguity as to which version of the method `D` should inherit. This situation creates complexity and potential errors in the program.

### Ambiguity Example

```java
class A {
    void display() {
        System.out.println("Display in A");
    }
}

class B extends A {
    void display() {
        System.out.println("Display in B");
    }
}

class C extends A {
    void display() {
        System.out.println("Display in C");
    }
}

// If Java allowed multiple inheritance
class D extends B, C {
    // Which display() method should D inherit?
}
```

In the hypothetical class `D`, it’s unclear whether `D` should inherit the `display()` method from `B` or `C`. This ambiguity can lead to errors and makes the language more complex to use and understand.

### How Java Addresses This

Java avoids this problem by not allowing multiple inheritance through classes. Instead, Java provides interfaces to achieve a form of multiple inheritance without the associated ambiguities.

### Using Interfaces for Multiple Inheritance

By using interfaces, Java allows a class to inherit from multiple sources without the diamond problem because interfaces only declare methods without providing implementations. This shifts the responsibility of defining the method behavior to the implementing class.

```java
interface InterfaceA {
    void display();
}

interface InterfaceB {
    void display();
}

class ConcreteClass implements InterfaceA, InterfaceB {
    // Must provide an implementation for display()
    public void display() {
        System.out.println("Display in ConcreteClass");
    }
}

public class MultipleInheritanceExample {
    public static void main(String[] args) {
        ConcreteClass obj = new ConcreteClass();
        obj.display();  // Outputs: Display in ConcreteClass
    }
}
```

### Benefits of Using Interfaces

1. **Avoids Ambiguity**: Since interfaces do not have method implementations, there is no ambiguity about which method to inherit.
2. **Decouples Implementation**: Interfaces allow classes to provide their own implementations, promoting flexibility and decoupling.
3. **Supports Multiple Inheritance**: A class can implement multiple interfaces, allowing it to inherit from multiple sources of behavior without the complexities of multiple class inheritance.

### Summary

- Java does not support multiple inheritance through classes to avoid the diamond problem and the associated complexity and ambiguity.
- Java uses interfaces to provide a form of multiple inheritance, allowing classes to inherit from multiple sources of behavior without the issues that arise with multiple class inheritance.
- This approach promotes clearer, more maintainable, and less error-prone code.

---------------------------------------------
## Are inheritance loosly coupled?
