
# Design Patterns:
- Design patterns are the well proved solution of commonly occuring problems in software design.
- Design pattern represents an idea.

### Categories:
#### 1. Creational Design Pattern: 
- Factory, Builder, Singleton
#### 2. Structural Design Pattern:
- Proxy, Adapter
#### 3. Behavioural Design Pattern:
- Observer, State, Iterator


## Singleton Design Pattern:

The Singleton design pattern ensures that a class has only one instance and provides a global point of access to that instance. It's useful in scenarios where exactly one object is needed to coordinate actions across the system. 

Here’s a detailed explanation of the Singleton pattern in Java, including its various implementations:

### Key Points of Singleton Design Pattern
1. **Single Instance**: Only one instance of the class exists.
2. **Global Access**: Provides a global point of access to the instance.
3. **Lazy Initialization**: The instance is created only when it is needed.

### Implementations of Singleton Pattern in Java

#### 1. Eager Initialization
In this approach, the instance is created at the time of class loading.
- even if client does not need this it will create the object. 

```java
public class Singleton {
    private static final Singleton INSTANCE = new Singleton();

    // Private constructor to prevent instantiation
    private Singleton() {}

    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```

#### 2. Lazy Initialization
- The instance is created only when it is needed.

```java
public class Singleton {
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() {}

   //Method synchronization
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

   // Another way
   public static  Singleton getInstance() {
     synchronized(Singleton.class){
        if (instance == null) {
            instance = new Singleton();
        }
       }
      return instance;
    }
}
```

#### 3. Thread-Safe Singleton
To make the lazy initialization thread-safe, synchronization is used.

```java
public class Singleton {
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

#### 4. Double-Checked Locking
A more efficient thread-safe implementation using double-checked locking.

```java
public class Singleton {
    private static volatile Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

#### 5. Bill Pugh Singleton Design
Utilizes the inner static helper class for lazy initialization.

```java
public class Singleton {
    private Singleton() {}

    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```

#### 6. Enum Singleton
The simplest way to create a singleton in Java, providing serialization and thread-safety by default.

```java
public enum Singleton {
    INSTANCE;
    
    public void someMethod() {
        // Some method
    }
}
```

### Use Cases for Singleton Pattern
- Logging
- Caching
- Thread Pools
- Configuration Settings
- Database Connections

### Pros and Cons of Singleton Pattern

#### Pros
- Controlled access to the sole instance.
- Reduces memory footprint since only one instance is created.
- Can be used to implement caching or thread pools.

#### Cons
- Difficult to unit test due to global state.
- Can hide dependencies, making the code harder to understand.
- Potential issues with concurrent access in multithreaded applications.

### Example Usage

Here's an example demonstrating the use of a Singleton pattern for a Logger class:

```java
public class Logger {
    private static Logger instance;

    private Logger() {
        // Private constructor to prevent instantiation
    }

    public static Logger getInstance() {
        if (instance == null) {
            instance = new Logger();
        }
        return instance;
    }

    public void log(String message) {
        System.out.println(message);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Logger logger = Logger.getInstance();
        logger.log("Singleton Logger Example");
    }
}
```

In this example, the `Logger` class is a singleton, ensuring that only one instance of the logger exists and can be accessed globally to log messages.

By understanding and implementing the Singleton pattern, you can ensure controlled access to a single instance, making your applications more efficient and easier to manage in scenarios requiring a single point of coordination.


### 3 ways to break Singleton Design Pattern:

The Singleton design pattern ensures that a class has only one instance and provides a global point of access to it. However, there are several ways to break the Singleton pattern's integrity. Here are three common ways:

### 1. Reflection

Reflection can be used to bypass the private constructor of a Singleton class, thus creating multiple instances.

```java
import java.lang.reflect.Constructor;

public class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {
        // Preventing instance creation
        if (instance != null) {
            throw new RuntimeException("Use getInstance() method to get the single instance of this class.");
        }
    }

    public static Singleton getInstance() {
        return instance;
    }
}

// Breaking Singleton with Reflection
public class SingletonReflectionBreak {
    public static void main(String[] args) {
        Singleton instance1 = Singleton.getInstance();
        Singleton instance2 = null;

        try {
            Constructor<Singleton> constructor = Singleton.class.getDeclaredConstructor();
            constructor.setAccessible(true);
            instance2 = constructor.newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }

        System.out.println(instance1.hashCode());
        System.out.println(instance2.hashCode());
    }
}
```
- If object is there => throw exception inside constructor
- use enum
### 2. Serialization and Deserialization

When a Singleton class implements `Serializable`, deserialization can create a new instance, breaking the Singleton pattern.

```java
import java.io.*;

public class Singleton implements Serializable {
    private static final Singleton instance = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }

    // To prevent new instance creation during deserialization
    protected Object readResolve() {
        return instance;
    }
}

// Breaking Singleton with Serialization
public class SingletonSerializationBreak {
    public static void main(String[] args) {
        Singleton instance1 = Singleton.getInstance();
        Singleton instance2 = null;

        try (ObjectOutput out = new ObjectOutputStream(new FileOutputStream("singleton.ser"))) {
            out.writeObject(instance1);
        } catch (IOException e) {
            e.printStackTrace();
        }

        try (ObjectInput in = new ObjectInputStream(new FileInputStream("singleton.ser"))) {
            instance2 = (Singleton) in.readObject();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }

        System.out.println(instance1.hashCode());
        System.out.println(instance2.hashCode());
    }
}
```

### 3. Cloning

If a Singleton class implements `Cloneable`, the `clone()` method can be used to create a new instance.

```java
public class Singleton implements Cloneable {
    private static final Singleton instance = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // This will break the singleton pattern
    }
}

// Breaking Singleton with Cloning
public class SingletonCloningBreak {
    public static void main(String[] args) {
        Singleton instance1 = Singleton.getInstance();
        Singleton instance2 = null;

        try {
            instance2 = (Singleton) instance1.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }

        System.out.println(instance1.hashCode());
        System.out.println(instance2.hashCode());
    }
}
```

### Prevention Measures

To prevent breaking the Singleton pattern through these methods, you can use the following strategies:

1. **Reflection**: Throw an exception if the constructor is called more than once.
   ```java
   private Singleton() {
       if (instance != null) {
           throw new RuntimeException("Use getInstance() method to get the single instance of this class.");
       }
   }
   ```

2. **Serialization**: Implement `readResolve` method to return the same instance.
   ```java
   protected Object readResolve() {
       return getInstance();
   }
   ```

3. **Cloning**: Override `clone()` method to throw `CloneNotSupportedException`.
   ```java
   @Override
   protected Object clone() throws CloneNotSupportedException {
       throw new CloneNotSupportedException("Cloning of this singleton instance is not allowed");
   }
   ```

By applying these strategies, you can reinforce the integrity of the Singleton pattern and ensure that only one instance of the class is ever created.

--------------------------------------------------------
## Factory Design Pattern:
The Factory Design Pattern is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created. 
The essence of the Factory Pattern is to define an interface for creating an object but let subclasses decide which class to instantiate. 
 It promotes loose coupling by eliminating the need to bind application-specific classes into the code.

### Key Points of Factory Design Pattern
1. **Encapsulation**: Encapsulates the object creation code.
2. **Loose Coupling**: Promotes loose coupling by removing the need to bind specific classes into the code.
3. **Single Responsibility Principle**: A factory method is responsible for creating objects, allowing the rest of the code to focus on using these objects.

### Types of Factory Pattern

1. **Simple Factory**
2. **Factory Method**
3. **Abstract Factory**

#### 1. Simple Factory
A simple factory class that returns instances of different classes based on input.

```java
public class ShapeFactory {
    public Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("RECTANGLE")) {
            return new Rectangle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        }
        return null;
    }
}

// Shape Interface
public interface Shape {
    void draw();
}

// Concrete implementations
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Inside Circle::draw() method.");
    }
}

public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Inside Rectangle::draw() method.");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Inside Square::draw() method.");
    }
}

// Usage
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        Shape shape1 = shapeFactory.getShape("CIRCLE");
        shape1.draw();

        Shape shape2 = shapeFactory.getShape("RECTANGLE");
        shape2.draw();

        Shape shape3 = shapeFactory.getShape("SQUARE");
        shape3.draw();
    }
}
```

#### 2. Factory Method
Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created.

```java
// Creator abstract class
public abstract class ShapeFactory {
    public abstract Shape createShape();

    public void drawShape() {
        Shape shape = createShape();
        shape.draw();
    }
}

// Concrete creators
public class CircleFactory extends ShapeFactory {
    @Override
    public Shape createShape() {
        return new Circle();
    }
}

public class RectangleFactory extends ShapeFactory {
    @Override
    public Shape createShape() {
        return new Rectangle();
    }
}

public class SquareFactory extends ShapeFactory {
    @Override
    public Shape createShape() {
        return new Square();
    }
}

// Usage
public class FactoryMethodPatternDemo {
    public static void main(String[] args) {
        ShapeFactory circleFactory = new CircleFactory();
        circleFactory.drawShape();

        ShapeFactory rectangleFactory = new RectangleFactory();
        rectangleFactory.drawShape();

        ShapeFactory squareFactory = new SquareFactory();
        squareFactory.drawShape();
    }
}
```


### Pros and Cons of Factory Design Pattern

#### Pros
- **Encapsulation**: Object creation logic is encapsulated in the factory.
- **Loose Coupling**: The client code is decoupled from the concrete classes it needs to instantiate.
- **Single Responsibility Principle**: Separates the creation of objects from their usage.
- **Scalability**: Easy to introduce new types of products without altering existing code.

#### Cons
- **Complexity**: Can introduce an additional layer of complexity and require more code.
- **Overhead**: May result in a slight performance overhead due to additional object creation logic.

### Use Cases for Factory Pattern
- When the exact type and dependencies of the object are not known until runtime.
- When a class can't anticipate the class of objects it needs to create.
- When you want to provide a library of products and expose their creation logic.

By using the Factory pattern, you can achieve a flexible and maintainable code structure where object creation is handled systematically, leading to more robust and adaptable applications.


## Abstract Factory Design Pattern: [Add dofference table]
- It provides a concept of factory of factories.
The Abstract Factory design pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. 
This pattern is particularly useful when a system needs to be independent of how its objects are created, composed, and represented, and when the system needs to be configured with one of multiple families of objects.

### Key Points of Abstract Factory Design Pattern
1. **Family of Objects**: Provides a way to encapsulate a group of individual factories that have a common theme.
2. **Independence**: Helps in making the system independent of how its objects are created.
3. **Consistency**: Ensures that the objects created are compatible with each other.

### Structure

1. **Abstract Factory**: Declares a set of methods for creating abstract products.
2. **Concrete Factory**: Implements the operations to create concrete product objects.
3. **Abstract Product**: Declares an interface for a type of product object.
4. **Concrete Product**: Defines a product object to be created by the corresponding concrete factory.
5. **Client**: Uses only the interfaces declared by the abstract factory and abstract product classes.

### Example Scenario

Suppose we are designing a system that can create UI components (like buttons and text fields) for different operating systems (e.g., Windows and MacOS).

#### Step 1: Define Abstract Products
These are the common interfaces for products that can be created by the factory.

```java
// Abstract Product A
public interface Button {
    void paint();
}

// Abstract Product B
public interface TextField {
    void render();
}
```

#### Step 2: Define Concrete Products
These are the implementations of the abstract products for specific contexts (Windows, MacOS).

```java
// Concrete Product A1
public class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in Windows style.");
    }
}

// Concrete Product A2
public class MacOSButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in MacOS style.");
    }
}

// Concrete Product B1
public class WindowsTextField implements TextField {
    @Override
    public void render() {
        System.out.println("Rendering a text field in Windows style.");
    }
}

// Concrete Product B2
public class MacOSTextField implements TextField {
    @Override
    public void render() {
        System.out.println("Rendering a text field in MacOS style.");
    }
}
```

#### Step 3: Define Abstract Factory
This interface declares creation methods for all abstract products.

```java
public interface GUIFactory {
    Button createButton();
    TextField createTextField();
}
```

#### Step 4: Define Concrete Factories
These implement the creation methods for specific contexts.

```java
// Concrete Factory 1
public class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public TextField createTextField() {
        return new WindowsTextField();
    }
}

// Concrete Factory 2
public class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public TextField createTextField() {
        return new MacOSTextField();
    }
}
```

#### Step 5: Client Code
The client interacts with the factory to create products. It uses the abstract factory and abstract products interfaces.

```java
public class Application {
    private Button button;
    private TextField textField;

    public Application(GUIFactory factory) {
        button = factory.createButton();
        textField = factory.createTextField();
    }

    public void paint() {
        button.paint();
        textField.render();
    }
}

// Usage
public class AbstractFactoryPatternDemo {
    public static void main(String[] args) {
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("win")) {
            factory = new WindowsFactory();
        } else {
            factory = new MacOSFactory();
        }
        Application app = new Application(factory);
        app.paint();
    }
}
```

### Pros and Cons of Abstract Factory Design Pattern

#### Pros
- **Encapsulation of Object Creation**: The client code is decoupled from the actual object creation process.
- **Consistency**: Ensures that products created by the factories are compatible with each other.
- **Scalability**: Adding new product families is easier without modifying existing code.

#### Cons
- **Complexity**: Can increase the overall complexity of the code due to the many interfaces and classes involved.
- **Rigid Structure**: Can be difficult to introduce new kinds of products into the family.

### Use Cases for Abstract Factory Pattern
- When a system needs to be independent of how its products are created, composed, and represented.
- When a system needs to be configured with one of multiple families of products.
- When a family of related product objects is designed to be used together, and you need to enforce this constraint.
- When you want to provide a library of products, and you want to reveal just their interfaces, not their implementations.

By using the Abstract Factory pattern, you can create a system that is flexible, scalable, and easy to manage, especially when dealing with multiple families of related products.


## Builder Design Pattern:
- While creating object when object contain many attributes there are many problems exists:
   - 1. We have to pass many arguments to create object.
   - 2. Some parameters might be optional
   - 3. factory class takes all responsibility for creating object. if the object is heavy then all complexity is the part of factory class.
- So in builder pattern we create object step by step and finallyreturn final object with desired values of attributes.
  
The Builder design pattern is a creational pattern used to construct complex objects step by step. It separates the construction of a complex object from its representation so that the same construction process can create different representations. This pattern is particularly useful when an object needs to be created in multiple steps, with various combinations of options, or when the creation process involves a lot of parameters.

### Key Points of Builder Design Pattern
1. **Separation of Construction and Representation**: The construction of an object is separated from its representation.
2. **Step-by-Step Construction**: The object is constructed step by step.
3. **Immutable Object**: Typically, the constructed object is immutable once it has been built.

### Structure
1. **Builder Interface**: Declares the steps required to build the product.
2. **Concrete Builder**: Implements the Builder interface and provides specific implementations for the steps.
3. **Product**: The complex object that is being built.
4. **Director**: Constructs the product using the Builder interface. It is optional and can be used to enforce the order of steps.

### Example Scenario

Suppose we are building a complex `House` object with different parts such as walls, roof, windows, and doors.

#### Step 1: Define the Product

```java
public class House {
    private String walls;
    private String roof;
    private String windows;
    private String doors;

    public House() {
        // default constructor
    }

    public void setWalls(String walls) {
        this.walls = walls;
    }

    public void setRoof(String roof) {
        this.roof = roof;
    }

    public void setWindows(String windows) {
        this.windows = windows;
    }

    public void setDoors(String doors) {
        this.doors = doors;
    }

    @Override
    public String toString() {
        return "House [walls=" + walls + ", roof=" + roof + ", windows=" + windows + ", doors=" + doors + "]";
    }
}
```

#### Step 2: Define the Builder Interface

```java
public interface HouseBuilder {
    void buildWalls();
    void buildRoof();
    void buildWindows();
    void buildDoors();
    House getHouse();
}
```

#### Step 3: Implement Concrete Builders

```java
public class ConcreteHouseBuilder implements HouseBuilder {
    private House house;

    public ConcreteHouseBuilder() {
        this.house = new House();
    }

    @Override
    public void buildWalls() {
        house.setWalls("Concrete Walls");
    }

    @Override
    public void buildRoof() {
        house.setRoof("Concrete Roof");
    }

    @Override
    public void buildWindows() {
        house.setWindows("Double-glazed Windows");
    }

    @Override
    public void buildDoors() {
        house.setDoors("Wooden Doors");
    }

    @Override
    public House getHouse() {
        return this.house;
    }
}

public class WoodenHouseBuilder implements HouseBuilder {
    private House house;

    public WoodenHouseBuilder() {
        this.house = new House();
    }

    @Override
    public void buildWalls() {
        house.setWalls("Wooden Walls");
    }

    @Override
    public void buildRoof() {
        house.setRoof("Wooden Roof");
    }

    @Override
    public void buildWindows() {
        house.setWindows("Single-glazed Windows");
    }

    @Override
    public void buildDoors() {
        house.setDoors("Wooden Doors");
    }

    @Override
    public House getHouse() {
        return this.house;
    }
}
```

#### Step 4: Define the Director

```java
public class ConstructionDirector {
    private HouseBuilder houseBuilder;

    public ConstructionDirector(HouseBuilder houseBuilder) {
        this.houseBuilder = houseBuilder;
    }

    public void constructHouse() {
        houseBuilder.buildWalls();
        houseBuilder.buildRoof();
        houseBuilder.buildWindows();
        houseBuilder.buildDoors();
    }

    public House getHouse() {
        return this.houseBuilder.getHouse();
    }
}
```

#### Step 5: Client Code

```java
public class BuilderPatternDemo {
    public static void main(String[] args) {
        HouseBuilder concreteHouseBuilder = new ConcreteHouseBuilder();
        ConstructionDirector director = new ConstructionDirector(concreteHouseBuilder);
        director.constructHouse();
        House concreteHouse = director.getHouse();
        System.out.println("Concrete House built: " + concreteHouse);

        HouseBuilder woodenHouseBuilder = new WoodenHouseBuilder();
        director = new ConstructionDirector(woodenHouseBuilder);
        director.constructHouse();
        House woodenHouse = director.getHouse();
        System.out.println("Wooden House built: " + woodenHouse);
    }
}
```

### Pros and Cons of Builder Design Pattern

#### Pros
- **Separation of Concerns**: Separates the construction of a complex object from its representation.
- **Fluent Interface**: Provides a clear and fluent interface for building objects.
- **Immutable Object**: Often results in immutable objects, which are easier to manage.
- **Flexible and Scalable**: Easily accommodates new representations and modifications to the object construction process.

#### Cons
- **Complexity**: Can introduce additional complexity with many classes and interfaces.
- **Verbose Code**: May result in verbose code with multiple builder methods.

### Use Cases for Builder Pattern
- When an object needs to be created with a lot of optional parameters or steps.
- When constructing complex objects that require multiple steps to build.
- When the creation process needs to be independent of the parts that make up the object.
- When you need to create different representations of the same object.

### Fluent Builder Example

For more readability and ease of use, the Builder pattern can be implemented using a fluent interface:

```java
public class House {
    private String walls;
    private String roof;
    private String windows;
    private String doors;

    private House(HouseBuilder builder) {
        this.walls = builder.walls;
        this.roof = builder.roof;
        this.windows = builder.windows;
        this.doors = builder.doors;
    }

    public static class HouseBuilder {
        private String walls;
        private String roof;
        private String windows;
        private String doors;

        public HouseBuilder setWalls(String walls) {
            this.walls = walls;
            return this;
        }

        public HouseBuilder setRoof(String roof) {
            this.roof = roof;
            return this;
        }

        public HouseBuilder setWindows(String windows) {
            this.windows = windows;
            return this;
        }

        public HouseBuilder setDoors(String doors) {
            this.doors = doors;
            return this;
        }

        public House build() {
            return new House(this);
        }
    }

    @Override
    public String toString() {
        return "House [walls=" + walls + ", roof=" + roof + ", windows=" + windows + ", doors=" + doors + "]";
    }
}

// Usage
public class FluentBuilderPatternDemo {
    public static void main(String[] args) {
        House house = new House.HouseBuilder()
            .setWalls("Concrete Walls")
            .setRoof("Concrete Roof")
            .setWindows("Double-glazed Windows")
            .setDoors("Wooden Doors")
            .build();
        System.out.println("House built: " + house);
    }
}
```

By using the Builder pattern, you can construct complex objects in a clean and modular way, making your code more readable, maintainable, and flexible.


## Prototype Design Pattern:

The Prototype design pattern is a creational design pattern used to create new objects by copying an existing object, known as the prototype. This pattern is particularly useful when the cost of creating a new object is more expensive than copying an existing one or when creating an object involves complex configurations.

### Key Points of Prototype Design Pattern
1. **Cloning**: Creates new objects by copying an existing object (prototype).
2. **Shallow vs. Deep Copy**: Can perform either shallow or deep copies of objects.
3. **Flexibility**: Adds flexibility by decoupling the client code from the specifics of object creation.

### Structure
1. **Prototype**: Declares an interface for cloning itself.
2. **Concrete Prototype**: Implements the operation for cloning itself.
3. **Client**: Creates a new object by asking a prototype to clone itself.

### Example Scenario

Suppose we have a `Shape` class and want to create new shapes by copying existing ones rather than creating new instances from scratch.

#### Step 1: Define the Prototype Interface

```java
public interface Prototype {
    Prototype clone();
}
```

#### Step 2: Implement Concrete Prototypes

```java
public class Circle implements Prototype {
    private int radius;
    private String color;

    public Circle(int radius, String color) {
        this.radius = radius;
        this.color = color;
    }

    @Override
    public Circle clone() {
        return new Circle(this.radius, this.color); // Shallow copy
    }

    @Override
    public String toString() {
        return "Circle [radius=" + radius + ", color=" + color + "]";
    }
}

public class Rectangle implements Prototype {
    private int width;
    private int height;
    private String color;

    public Rectangle(int width, int height, String color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }

    @Override
    public Rectangle clone() {
        return new Rectangle(this.width, this.height, this.color); // Shallow copy
    }

    @Override
    public String toString() {
        return "Rectangle [width=" + width + ", height=" + height + ", color=" + color + "]";
    }
}
```

#### Step 3: Client Code

```java
public class PrototypePatternDemo {
    public static void main(String[] args) {
        Circle circle1 = new Circle(10, "red");
        Circle circle2 = circle1.clone();
        System.out.println("Original Circle: " + circle1);
        System.out.println("Cloned Circle: " + circle2);

        Rectangle rectangle1 = new Rectangle(20, 10, "blue");
        Rectangle rectangle2 = rectangle1.clone();
        System.out.println("Original Rectangle: " + rectangle1);
        System.out.println("Cloned Rectangle: " + rectangle2);
    }
}
```

### Deep Copy Example

If your prototype contains mutable objects and you need to perform a deep copy, the `clone` method should ensure all objects are duplicated.

```java
import java.util.ArrayList;
import java.util.List;

public class ShapeWithDetails implements Prototype {
    private String type;
    private List<String> details;

    public ShapeWithDetails(String type, List<String> details) {
        this.type = type;
        this.details = new ArrayList<>(details);
    }

    @Override
    public ShapeWithDetails clone() {
        List<String> clonedDetails = new ArrayList<>(this.details);
        return new ShapeWithDetails(this.type, clonedDetails);
    }

    @Override
    public String toString() {
        return "ShapeWithDetails [type=" + type + ", details=" + details + "]";
    }
}

// Usage
public class DeepCopyPrototypeDemo {
    public static void main(String[] args) {
        List<String> details = new ArrayList<>();
        details.add("Detail1");
        details.add("Detail2");

        ShapeWithDetails shape1 = new ShapeWithDetails("ComplexShape", details);
        ShapeWithDetails shape2 = shape1.clone();

        // Modify the original details
        details.add("Detail3");

        System.out.println("Original Shape: " + shape1);
        System.out.println("Cloned Shape: " + shape2);
    }
}
```

### Pros and Cons of Prototype Design Pattern

#### Pros
- **Performance**: Can significantly improve performance by cloning existing objects rather than creating new ones.
- **Flexibility**: Decouples the client code from the specifics of object creation.
- **Complex Object Creation**: Simplifies the creation of complex objects.

#### Cons
- **Cloning Complexity**: Cloning complex objects that have circular references or deep copying requirements can be tricky.
- **Clone Method Implementation**: Requires careful implementation of the `clone` method, especially for deep copies.

### Use Cases for Prototype Pattern
- When the cost of creating a new object is prohibitive.
- When creating an object involves a lot of configuration.
- When the objects to be created are almost identical but differ slightly.
- When an application needs to dynamically load classes and create objects at runtime.

### Java Built-in Support

Java provides built-in support for the Prototype pattern with the `Cloneable` interface and `clone` method in the `Object` class.

```java
public class PrototypeDemo implements Cloneable {
    private int x;
    private int y;

    public PrototypeDemo(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public String toString() {
        return "PrototypeDemo [x=" + x + ", y=" + y + "]";
    }

    public static void main(String[] args) {
        try {
            PrototypeDemo original = new PrototypeDemo(10, 20);
            PrototypeDemo cloned = (PrototypeDemo) original.clone();
            System.out.println("Original Object: " + original);
            System.out.println("Cloned Object: " + cloned);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

By using the Prototype pattern, you can create complex objects efficiently and flexibly, making it easier to manage and extend your code.


## Shallow Copy vs Deep copy:

In object-oriented programming, copying objects can be performed in two ways: shallow copy and deep copy. These methods determine how objects and their references are duplicated.

### Shallow Copy

A shallow copy of an object creates a new object, but instead of copying the actual objects that the original object references, it copies the references to those objects. This means that the shallow copy and the original object share references to the same objects.

#### Example:

```java
import java.util.ArrayList;

public class ShallowCopyExample implements Cloneable {
    private ArrayList<String> list;

    public ShallowCopyExample() {
        this.list = new ArrayList<>();
    }

    public void addItem(String item) {
        list.add(item);
    }

    public ArrayList<String> getList() {
        return list;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow copy
    }

    public static void main(String[] args) {
        try {
            ShallowCopyExample original = new ShallowCopyExample();
            original.addItem("Item1");
            ShallowCopyExample shallowCopy = (ShallowCopyExample) original.clone();

            System.out.println("Original List: " + original.getList());
            System.out.println("Shallow Copy List: " + shallowCopy.getList());

            // Modify the original list
            original.addItem("Item2");

            System.out.println("Original List after modification: " + original.getList());
            System.out.println("Shallow Copy List after original modification: " + shallowCopy.getList());

        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

Output:
```
Original List: [Item1]
Shallow Copy List: [Item1]
Original List after modification: [Item1, Item2]
Shallow Copy List after original modification: [Item1, Item2]
```

In this example, modifying the original list also affects the shallow copy because both the original and the copy share the same list reference.

### Deep Copy

A deep copy of an object creates a new object and recursively copies all objects referenced by the original object. This means that the deep copy and the original object do not share any references; they are entirely independent.

#### Example:

```java
import java.util.ArrayList;

public class DeepCopyExample implements Cloneable {
    private ArrayList<String> list;

    public DeepCopyExample() {
        this.list = new ArrayList<>();
    }

    public void addItem(String item) {
        list.add(item);
    }

    public ArrayList<String> getList() {
        return list;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        DeepCopyExample deepCopy = (DeepCopyExample) super.clone();
        deepCopy.list = new ArrayList<>(this.list); // Deep copy
        return deepCopy;
    }

    public static void main(String[] args) {
        try {
            DeepCopyExample original = new DeepCopyExample();
            original.addItem("Item1");
            DeepCopyExample deepCopy = (DeepCopyExample) original.clone();

            System.out.println("Original List: " + original.getList());
            System.out.println("Deep Copy List: " + deepCopy.getList());

            // Modify the original list
            original.addItem("Item2");

            System.out.println("Original List after modification: " + original.getList());
            System.out.println("Deep Copy List after original modification: " + deepCopy.getList());

        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

Output:
```
Original List: [Item1]
Deep Copy List: [Item1]
Original List after modification: [Item1, Item2]
Deep Copy List after original modification: [Item1]
```

In this example, modifying the original list does not affect the deep copy because each list is an independent copy.

### Key Differences

- **Shallow Copy**:
  - Creates a new object.
  - Copies the references to the objects.
  - Changes to mutable objects in the original object are reflected in the shallow copy.
  - Faster and requires less memory.

- **Deep Copy**:
  - Creates a new object.
  - Recursively copies all objects referenced by the original object.
  - Changes to the original object do not affect the deep copy.
  - Slower and requires more memory.

### Use Cases

- **Shallow Copy**: Useful when the objects being copied are not expected to be modified, or when the cost of deep copying is too high.
- **Deep Copy**: Essential when the objects being copied may be modified independently, ensuring complete separation between the original and the copied objects.

Choosing between shallow and deep copying depends on the specific requirements of your application and the behavior you need from the copied objects.



## Observer Design Pattern:

The Observer design pattern is a behavioral pattern used to establish a one-to-many dependency between objects so that when one object changes state, all its dependents (observers) are notified and updated automatically. This pattern is often used to implement distributed event-handling systems, ensuring that changes in one part of the system are communicated to all interested parties.

### Components of Observer Pattern

1. **Subject**: The object that holds the state and provides a mechanism to attach and detach observers.
2. **Observer**: The interface or abstract class for objects that should be notified of changes in the subject.
3. **ConcreteSubject**: A concrete implementation of the subject that stores state and notifies observers of changes.
4. **ConcreteObserver**: Concrete implementations of observers that get notified when the subject's state changes.

### Example Scenario

Let's consider an example of a weather station that notifies various display elements (observers) about the weather changes (subject).

#### Step 1: Define the Observer Interface

```java
interface Observer {
    void update(float temperature, float humidity, float pressure);
}
```

#### Step 2: Define the Subject Interface

```java
interface Subject {
    void registerObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}
```

#### Step 3: Implement ConcreteSubject

```java
import java.util.ArrayList;

class WeatherData implements Subject {
    private ArrayList<Observer> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherData() {
        observers = new ArrayList<>();
    }

    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }

    @Override
    public void removeObserver(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }

    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }

    public void measurementsChanged() {
        notifyObservers();
    }
}
```

#### Step 4: Implement ConcreteObservers

```java
class CurrentConditionsDisplay implements Observer {
    private float temperature;
    private float humidity;
    private Subject weatherData;

    public CurrentConditionsDisplay(Subject weatherData) {
        this.weatherData = weatherData;
        weatherData.registerObserver(this);
    }

    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        display();
    }

    public void display() {
        System.out.println("Current conditions: " + temperature + "F degrees and " + humidity + "% humidity");
    }
}

class StatisticsDisplay implements Observer {
    private float maxTemp = 0.0f;
    private float minTemp = 200;
    private float tempSum = 0.0f;
    private int numReadings;
    private Subject weatherData;

    public StatisticsDisplay(Subject weatherData) {
        this.weatherData = weatherData;
        weatherData.registerObserver(this);
    }

    @Override
    public void update(float temperature, float humidity, float pressure) {
        tempSum += temperature;
        numReadings++;

        if (temperature > maxTemp) {
            maxTemp = temperature;
        }

        if (temperature < minTemp) {
            minTemp = temperature;
        }

        display();
    }

    public void display() {
        System.out.println("Avg/Max/Min temperature = " + (tempSum / numReadings) + "/" + maxTemp + "/" + minTemp);
    }
}
```

#### Step 5: Demonstrate the Observer Pattern

```java
public class WeatherStation {
    public static void main(String[] args) {
        WeatherData weatherData = new WeatherData();

        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherData);
        StatisticsDisplay statisticsDisplay = new StatisticsDisplay(weatherData);

        weatherData.setMeasurements(80, 65, 30.4f);
        weatherData.setMeasurements(82, 70, 29.2f);
        weatherData.setMeasurements(78, 90, 29.2f);
    }
}
```

### Pros and Cons of the Observer Pattern

#### Pros
- **Loose Coupling**: Observers are decoupled from the subject, promoting low coupling.
- **Flexibility**: New observers can be added without modifying the subject.
- **Broadcast Communication**: Changes to the subject can be efficiently broadcast to all registered observers.

#### Cons
- **Memory Leaks**: If observers are not correctly removed, memory leaks can occur.
- **Update Overhead**: Frequent updates can cause performance overhead, especially if there are many observers.

### Use Cases
- **Event Handling**: GUI frameworks use the Observer pattern for event handling and callback mechanisms.
- **Distributed Systems**: Used in distributed systems to keep replicas synchronized.
- **Model-View-Controller (MVC)**: In MVC architecture, views can be observers of the model to update when the model changes.

The Observer pattern is a powerful tool for creating flexible and maintainable applications where components need to stay in sync with each other. By understanding and implementing this pattern, you can enhance your ability to manage dependencies and improve the overall design of your software.


## Iterator Design Pattern:

Sure! Let's delve into the Iterator and Adapter design patterns, which are part of the behavioral and structural patterns respectively in design pattern paradigms.

## Iterator Design Pattern

The Iterator design pattern provides a way to access the elements of a collection object sequentially without exposing its underlying representation. It abstracts the traversal process, allowing different collection structures to be iterated in a uniform way.

### Key Components
1. **Iterator**: An interface or abstract class that defines methods for traversing the elements.
2. **Concrete Iterator**: A concrete implementation of the Iterator interface for a specific collection.
3. **Aggregate**: An interface that defines a method to create an Iterator.
4. **Concrete Aggregate**: A concrete implementation of the Aggregate interface to return an instance of the Iterator.

### Example

Let's consider a collection of names and create an iterator to traverse it.

#### Step 1: Define the Iterator Interface

```java
interface Iterator {
    boolean hasNext();
    Object next();
}
```

#### Step 2: Implement Concrete Iterator

```java
class NameIterator implements Iterator {
    private String[] names;
    private int index;

    public NameIterator(String[] names) {
        this.names = names;
    }

    @Override
    public boolean hasNext() {
        return index < names.length;
    }

    @Override
    public Object next() {
        if (this.hasNext()) {
            return names[index++];
        }
        return null;
    }
}
```

#### Step 3: Define the Aggregate Interface

```java
interface Container {
    Iterator getIterator();
}
```

#### Step 4: Implement Concrete Aggregate

```java
class NameRepository implements Container {
    private String[] names = {"John", "Jane", "Robert", "Lucy"};

    @Override
    public Iterator getIterator() {
        return new NameIterator(names);
    }
}
```

#### Step 5: Demonstrate the Iterator Pattern

```java
public class IteratorPatternDemo {
    public static void main(String[] args) {
        NameRepository nameRepository = new NameRepository();

        for (Iterator iter = nameRepository.getIterator(); iter.hasNext();) {
            String name = (String) iter.next();
            System.out.println("Name: " + name);
        }
    }
}
```

Output:
```
Name: John
Name: Jane
Name: Robert
Name: Lucy
```

### Pros and Cons of the Iterator Pattern

#### Pros
- **Simplifies Collection Traversal**: Provides a simple way to traverse complex collections.
- **Encapsulates Iteration Logic**: Keeps the iteration logic encapsulated within the iterator, adhering to the Single Responsibility Principle.
- **Uniform Interface**: Allows traversal through different types of collections with a uniform interface.

#### Cons
- **Overhead**: Can introduce overhead for simple collections or single-use scenarios.
- **Exposure**: May expose collection elements that should remain hidden if not properly managed.

## Adapter Design Pattern

The Adapter design pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces by converting the interface of a class into another interface expected by the clients.

### Key Components
1. **Target**: Defines the domain-specific interface that clients use.
2. **Adapter**: Adapts the interface of the Adaptee to the Target interface.
3. **Adaptee**: Defines an existing interface that needs to be adapted.
4. **Client**: Uses the Target interface.

### Example

Let's consider a scenario where we have an audio player that can play MP3 files but we need to make it play VLC and MP4 formats as well.

#### Step 1: Define the Target Interface

```java
interface MediaPlayer {
    void play(String audioType, String fileName);
}
```

#### Step 2: Define the Adaptee Interfaces

```java
interface AdvancedMediaPlayer {
    void playVlc(String fileName);
    void playMp4(String fileName);
}

class VlcPlayer implements AdvancedMediaPlayer {
    @Override
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file. Name: " + fileName);
    }

    @Override
    public void playMp4(String fileName) {
        // Do nothing
    }
}

class Mp4Player implements AdvancedMediaPlayer {
    @Override
    public void playVlc(String fileName) {
        // Do nothing
    }

    @Override
    public void playMp4(String fileName) {
        System.out.println("Playing mp4 file. Name: " + fileName);
    }
}
```

#### Step 3: Implement the Adapter

```java
class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer = new VlcPlayer();
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer = new Mp4Player();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer.playVlc(fileName);
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMediaPlayer.playMp4(fileName);
        }
    }
}
```

#### Step 4: Implement the Client Class

```java
class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file. Name: " + fileName);
        } else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType + " format not supported");
        }
    }
}
```

#### Step 5: Demonstrate the Adapter Pattern

```java
public class AdapterPatternDemo {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("mp4", "video.mp4");
        audioPlayer.play("vlc", "movie.vlc");
        audioPlayer.play("avi", "animation.avi");
    }
}
```

Output:
```
Playing mp3 file. Name: song.mp3
Playing mp4 file. Name: video.mp4
Playing vlc file. Name: movie.vlc
Invalid media. avi format not supported
```

### Pros and Cons of the Adapter Pattern

#### Pros
- **Reusability**: Promotes the reusability of existing components.
- **Interoperability**: Allows interfaces that are incompatible to work together.
- **Flexibility**: Adds flexibility to the existing system, making it easier to extend and adapt.

#### Cons
- **Complexity**: Can add complexity to the codebase, especially when overused.
- **Performance**: May introduce a slight performance overhead due to additional layer of abstraction.

### Use Cases

- **Iterator Pattern**: When you need to provide a way to traverse through elements of a collection without exposing its underlying representation.
- **Adapter Pattern**: When you want to use an existing class but its interface is not compatible with the rest of your system, or when you want to create a reusable class that cooperates with unrelated or unforeseen classes.

Both the Iterator and Adapter design patterns play crucial roles in making software systems more flexible, reusable, and easy to maintain.


## Proxy Design Pattern:

Here's a detailed comparison table for the Singleton, Factory, Abstract Factory, Builder, Prototype, Adapter, and Iterator design patterns:

| Design Pattern       | Description                                                                                                                                                                                                                           | Benefits                                                                                                                                            | Use Cases                                                                                                                                                                         |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Singleton Pattern    | Ensures a class has only one instance and provides a global point of access to it.                                                                                                                                                     | - Controlled access to the single instance.<br>- Reduced resource usage.<br>- Ensures a single point of modification.                               | - Configuration settings managers.<br>- Logging classes.<br>- Connection pools.                                                                                                   |
| Factory Pattern      | Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.                                                                                                                        | - Encapsulates object creation.<br>- Promotes loose coupling.<br>- Enhances scalability and flexibility.                                         | - Managing and maintaining different types of objects within an application.<br>- Simplifying the creation of complex objects.                                                    |
| Abstract Factory Pattern | Provides an interface for creating families of related or dependent objects without specifying their concrete classes.                                                                                                                | - Promotes consistency among related objects.<br>- Isolates client code from concrete implementations.<br>- Facilitates the exchange of entire families of objects. | - GUI toolkit libraries.<br>- Plugin management systems.<br>- Document creation frameworks.                                                                                      |
| Builder Pattern      | Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.                                                                                   | - Promotes a step-by-step construction process.<br>- Provides control over the construction process.<br>- Facilitates the creation of immutable objects.   | - Constructing complex objects like houses, cars, or computer systems.<br>- Creating objects with numerous optional parameters.                                                |
| Prototype Pattern    | Creates new objects by copying an existing object, known as the prototype.                                                                                                                                                           | - Reduces the need for subclassing.<br>- Hides the complexity of instantiation.<br>- Facilitates the creation of objects at runtime.                  | - Creating objects when the classes to instantiate are specified at runtime.<br>- Avoiding the cost of creating complex objects through the new operator.                        |
| Adapter Pattern      | Allows incompatible interfaces to work together by converting the interface of a class into another interface expected by the client.                                                                                                 | - Promotes reuse of existing classes.<br>- Facilitates interoperability between systems.<br>- Enhances flexibility and extensibility.               | - Integrating new components into legacy systems.<br>- Creating reusable libraries.                                                                                               |
| Iterator Pattern     | Provides a way to access elements of a collection object sequentially without exposing its underlying representation.                                                                                                                 | - Simplifies traversal of collections.<br>- Promotes encapsulation of collection details.<br>- Enhances uniformity in traversing different types of collections. | - Traversing elements in data structures like lists, trees, or graphs.<br>- Implementing custom traversal logic for complex collections.                                          |

This comparison table outlines the key aspects of each design pattern, including their descriptions, benefits, and typical use cases, providing a comprehensive overview of their functionalities and applications.
