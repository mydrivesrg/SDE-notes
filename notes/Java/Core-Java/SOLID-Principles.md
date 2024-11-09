# SOLID Design Principles:
-----------------------------------------------------------------------------

## 1. Single Responsibility Principle (SRP)

**Definition:**
A class should have only one reason to change. This means a class should only have one job or responsibility.

**Why it's important:**
- **Maintainability:** Easier to update and fix bugs.
- **Readability:** Code is easier to understand.
- **Testability:** Each class has a single focus, making it easier to write unit tests.

**Example in Depth:**

Consider a simple application that manages employee records and generates reports.

**Incorrect Approach:**
```java
class Employee {
    private String name;
    private String position;

    public Employee(String name, String position) {
        this.name = name;
        this.position = position;
    }

    public String getName() {
        return name;
    }

    public String getPosition() {
        return position;
    }

    public void generateReport() {
        // Logic to generate report for the employee
    }
}
```

**Problems with the Incorrect Approach:**
- The `Employee` class has multiple responsibilities: managing employee data and generating reports.
- Changes to the report generation logic might require changes to the `Employee` class, which can introduce bugs into unrelated parts of the code.

**Correct Approach:**
Split the responsibilities into separate classes.

**Step 1: Create an `Employee` class for managing employee data.**

```java
class Employee {
    private String name;
    private String position;

    public Employee(String name, String position) {
        this.name = name;
        this.position = position;
    }

    public String getName() {
        return name;
    }

    public String getPosition() {
        return position;
    }
}
```

**Step 2: Create an `EmployeeReport` class for generating reports.**

```java
class EmployeeReport {
    public void generateReport(Employee employee) {
        // Logic to generate report for the employee
        System.out.println("Generating report for " + employee.getName());
    }
}
```

**Step 3: Use the classes together in a client class.**

```java
public class Main {
    public static void main(String[] args) {
        Employee employee = new Employee("John Doe", "Developer");
        EmployeeReport report = new EmployeeReport();
        report.generateReport(employee);
    }
}
```

**Benefits of the Correct Approach:**
- **Single Responsibility:** Each class has a single responsibility.
- **Easier Maintenance:** If report generation logic changes, only the `EmployeeReport` class needs modification.
- **Improved Testability:** You can test `Employee` and `EmployeeReport` classes independently.

**Additional Example:**

Let's consider a more detailed example involving a `Book` class that originally handles both book properties and database operations.

**Incorrect Approach:**

```java
class Book {
    private String title;
    private String author;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public void save() {
        // Logic to save the book in the database
        System.out.println("Saving book to database");
    }

    public void printDetails() {
        // Logic to print book details
        System.out.println("Title: " + title + ", Author: " + author);
    }
}
```

**Correct Approach:**

**Step 1: Create a `Book` class for book properties.**

```java
class Book {
    private String title;
    private String author;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }
}
```

**Step 2: Create a `BookRepository` class for database operations.**

```java
class BookRepository {
    public void save(Book book) {
        // Logic to save the book in the database
        System.out.println("Saving book to database");
    }
}
```

**Step 3: Create a `BookPrinter` class for printing book details.**

```java
class BookPrinter {
    public void printDetails(Book book) {
        // Logic to print book details
        System.out.println("Title: " + book.getTitle() + ", Author: " + book.getAuthor());
    }
}
```

**Step 4: Use the classes together in a client class.**

```java
public class Main {
    public static void main(String[] args) {
        Book book = new Book("Effective Java", "Joshua Bloch");
        BookRepository repository = new BookRepository();
        BookPrinter printer = new BookPrinter();

        repository.save(book);
        printer.printDetails(book);
    }
}
```

**Benefits of the Correct Approach:**
- **Single Responsibility:** Each class has a single responsibility.
- **Modularity:** Easier to replace or update individual components.
- **Scalability:** New functionalities can be added without affecting existing code.

### Summary:
The Single Responsibility Principle helps keep your code organized and manageable by ensuring each class focuses on a single responsibility. This improves maintainability, readability, and testability.

---
## 2. Open/Closed Principle (OCP)

**Definition:**
Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means you should be able to add new functionality to a class without altering its existing code.

**Why it's important:**
- **Maintainability:** Existing code remains untouched, reducing the risk of introducing bugs.
- **Scalability:** New features can be added by extending existing code, promoting code reuse.
- **Modularity:** Each class/module has a clear purpose and is less likely to have unintended side effects when modified.

**Example in Depth:**

Consider a simple shape hierarchy with a `Shape` base class and concrete subclasses `Rectangle` and `Circle`. Let's explore how to apply the OCP to this scenario.

**Incorrect Approach:**
```java
class Shape {
    private String type;

    public Shape(String type) {
        this.type = type;
    }

    public void draw() {
        if (type.equals("Rectangle")) {
            drawRectangle();
        } else if (type.equals("Circle")) {
            drawCircle();
        }
    }

    private void drawRectangle() {
        System.out.println("Drawing a rectangle");
    }

    private void drawCircle() {
        System.out.println("Drawing a circle");
    }
}
```

**Problems with the Incorrect Approach:**
- Adding a new shape (e.g., `Triangle`) requires modifying the `draw` method in the `Shape` class, violating OCP.
- The `Shape` class is not closed for modification.

**Correct Approach:**
Apply the OCP by using abstraction and polymorphism.

**Step 1: Create an abstract `Shape` class.**

```java
abstract class Shape {
    public abstract void draw();
}
```

**Step 2: Create concrete subclasses for each shape.**

```java
class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

**Step 3: Use the classes together in a client class.**

```java
public class Main {
    public static void main(String[] args) {
        Shape rectangle = new Rectangle();
        Shape circle = new Circle();

        rectangle.draw();
        circle.draw();
    }
}
```

**Benefits of the Correct Approach:**
- **Open for Extension:** You can add new shapes (e.g., `Triangle`) by creating a new subclass of `Shape` without modifying existing code.
- **Closed for Modification:** Existing code (e.g., `Shape` and its subclasses) remains unchanged when adding new shapes.

**Additional Example:**

Let's consider an example with a `PaymentProcessor` class that initially handles payments using a specific payment method.

**Incorrect Approach:**

```java
class PaymentProcessor {
    public void processPayment(String paymentMethod, double amount) {
        if (paymentMethod.equals("CreditCard")) {
            processCreditCardPayment(amount);
        } else if (paymentMethod.equals("PayPal")) {
            processPayPalPayment(amount);
        }
    }

    private void processCreditCardPayment(double amount) {
        System.out.println("Processing credit card payment of $" + amount);
    }

    private void processPayPalPayment(double amount) {
        System.out.println("Processing PayPal payment of $" + amount);
    }
}
```

**Correct Approach:**

**Step 1: Create an interface for payment methods.**

```java
interface PaymentMethod {
    void processPayment(double amount);
}
```

**Step 2: Implement concrete classes for each payment method.**

```java
class CreditCardPayment implements PaymentMethod {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment of $" + amount);
    }
}

class PayPalPayment implements PaymentMethod {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing PayPal payment of $" + amount);
    }
}
```

**Step 3: Modify `PaymentProcessor` to use the interface.**

```java
class PaymentProcessor {
    public void processPayment(PaymentMethod paymentMethod, double amount) {
        paymentMethod.processPayment(amount);
    }
}
```

**Step 4: Use the classes together in a client class.**

```java
public class Main {
    public static void main(String[] args) {
        PaymentProcessor processor = new PaymentProcessor();
        PaymentMethod creditCard = new CreditCardPayment();
        PaymentMethod payPal = new PayPalPayment();

        processor.processPayment(creditCard, 100.0);
        processor.processPayment(payPal, 50.0);
    }
}
```

**Benefits of the Correct Approach:**
- **Open for Extension:** You can add new payment methods by implementing the `PaymentMethod` interface without modifying existing code.
- **Closed for Modification:** Existing code (e.g., `PaymentProcessor`) remains unchanged when adding new payment methods.

### Summary:
The Open/Closed Principle encourages designing software components that are open for extension (allowing new functionalities to be added) but closed for modification (existing code remains unchanged). This promotes code reuse, maintainability, and scalability.

-------------------------------------------------------------------------------------

## 3. Liskov Substitution Principle (LSP)

**Definition:**
Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In simpler terms, a subclass should be able to substitute its parent class without causing errors or unexpected behavior.

**Why it's important:**
- **Code Reusability:** Promotes reuse of code by allowing subclasses to be used interchangeably with their parent class.
- **Maintainability:** Makes it easier to modify or extend classes without breaking existing code.
- **Polymorphism:** Supports polymorphic behavior, where objects of different classes can be treated uniformly.

**Example in Depth:**

Consider a scenario where we have a `Bird` superclass with subclasses `Sparrow` and `Ostrich`.

**Incorrect Approach:**
```java
class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}

class Sparrow extends Bird {
    // Sparrow can fly, so no issues here
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostrich can't fly");
    }
}
```

**Problems with the Incorrect Approach:**
- The `Ostrich` subclass violates the LSP because it throws an exception for the `fly` method, which is unexpected behavior for a bird.
- If code expects all birds to fly and uses a `Bird` reference, substituting an `Ostrich` object would lead to runtime errors.

**Correct Approach:**
Ensure that subclasses can be substituted for their parent class without altering the program's correctness.

**Step 1: Refactor the hierarchy to adhere to LSP.**

```java
abstract class Bird {
    public abstract void fly();
}

class Sparrow extends Bird {
    @Override
    public void fly() {
        System.out.println("Sparrow flying");
    }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        // Ostrich can't fly, so no implementation needed
        System.out.println("Ostrich can't fly");
    }
}
```

**Step 2: Use the classes with polymorphism.**

```java
public class Main {
    public static void main(String[] args) {
        Bird sparrow = new Sparrow();
        Bird ostrich = new Ostrich();

        sparrow.fly();  // Output: Sparrow flying
        ostrich.fly();  // Output: Ostrich can't fly
    }
}
```

**Benefits of the Correct Approach:**
- **Polymorphism:** Objects of different subclasses (`Sparrow` and `Ostrich`) can be treated as `Bird` objects, allowing for polymorphic behavior.
- **Substitution:** Substituting a `Sparrow` or `Ostrich` object for a `Bird` object does not lead to unexpected behavior or errors.

**Additional Example:**

Let's consider a more practical example involving geometric shapes.

**Incorrect Approach:**

```java
class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

**Correct Approach:**

```java
interface Shape {
    void draw();
}

class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

**Benefits of the Correct Approach:**
- **Liskov Substitution:** Objects of `Rectangle` and `Circle` classes can be substituted for `Shape` objects without causing issues.
- **Code Extensibility:** Adding new shapes is straightforward without modifying existing code.
- **Polymorphism:** Shapes can be treated uniformly through the `Shape` interface.

### Summary:
The Liskov Substitution Principle ensures that subclasses can be substituted for their parent class without altering the program's correctness. This promotes code reusability, maintainability, and supports polymorphic behavior.

----------------------------------------------------------------------------------------------

## 4. Interface Segregation Principle (ISP):

**Definition:**
Clients should not be forced to depend on interfaces they do not use. This principle encourages designing interfaces that are specific to the needs of clients to avoid unnecessary dependencies.

**Why it's important:**
- **Reduced Coupling:** Interfaces tailored to client needs reduce dependencies and coupling between components.
- **Modularity:** Classes/interfaces have clear responsibilities, making it easier to maintain and extend the codebase.
- **Scalability:** New functionalities can be added without affecting existing clients.

**Example in Depth:**

Consider a scenario where we have a `Worker` interface representing workers who can work and eat.

**Incorrect Approach:**
```java
interface Worker {
    void work();
    void eat();
}

class Human implements Worker {
    @Override
    public void work() {
        System.out.println("Human working");
    }

    @Override
    public void eat() {
        System.out.println("Human eating");
    }
}

class Robot implements Worker {
    @Override
    public void work() {
        System.out.println("Robot working");
    }

    @Override
    public void eat() {
        // Robots don't eat, so no implementation needed
    }
}
```

**Problems with the Incorrect Approach:**
- The `Robot` class is forced to implement the `eat` method even though robots don't eat, violating ISP.
- Clients that only need the `work` functionality are unnecessarily dependent on the `eat` method.

**Correct Approach:**
Design interfaces that are specific to client needs.

**Step 1: Create separate interfaces for different responsibilities.**

```java
interface Worker {
    void work();
}

interface Eater {
    void eat();
}

class Human implements Worker, Eater {
    @Override
    public void work() {
        System.out.println("Human working");
    }

    @Override
    public void eat() {
        System.out.println("Human eating");
    }
}

class Robot implements Worker {
    @Override
    public void work() {
        System.out.println("Robot working");
    }
}
```

**Step 2: Use interfaces based on client requirements.**

```java
public class Main {
    public static void main(String[] args) {
        Worker humanWorker = new Human();
        Worker robotWorker = new Robot();

        humanWorker.work();
        ((Eater) humanWorker).eat();  // Human-specific behavior

        robotWorker.work();
    }
}
```

**Benefits of the Correct Approach:**
- **Reduced Dependency:** Clients only depend on interfaces they use, reducing unnecessary dependencies.
- **Clear Responsibilities:** Interfaces and classes have clear responsibilities, improving code clarity and maintainability.
- **Scalability:** New interfaces can be added for new functionalities without affecting existing clients.

**Additional Example:**

Let's consider a scenario involving a printer system with different functionalities.

**Incorrect Approach:**

```java
interface Printer {
    void print();
    void scan();
    void fax();
}

class MultiFunctionPrinter implements Printer {
    @Override
    public void print() {
        System.out.println("Printing");
    }

    @Override
    public void scan() {
        System.out.println("Scanning");
    }

    @Override
    public void fax() {
        System.out.println("Faxing");
    }
}
```

**Correct Approach:**

```java
interface Printer {
    void print();
}

interface Scanner {
    void scan();
}

interface Fax {
    void fax();
}

class MultiFunctionPrinter implements Printer, Scanner, Fax {
    @Override
    public void print() {
        System.out.println("Printing");
    }

    @Override
    public void scan() {
        System.out.println("Scanning");
    }

    @Override
    public void fax() {
        System.out.println("Faxing");
    }
}
```

**Benefits of the Correct Approach:**
- **Modularity:** Interfaces are specific to functionalities, promoting modularity and code reusability.
- **Reduced Dependency:** Clients only depend on interfaces they need, reducing unnecessary coupling.
- **Scalability:** New functionalities can be added by implementing new interfaces without affecting existing clients.

### Summary:
The Interface Segregation Principle advocates designing interfaces that are specific to client needs to avoid unnecessary dependencies and promote modularity. This leads to cleaner, more maintainable, and scalable codebases.

----------------------------------------------------------------------------------------------
### 5. Dependency Inversion Principle (DIP)

**Definition:**
- High-level modules should not depend on low-level modules. Both should depend on abstractions.
- Abstractions should not depend on details. Details should depend on abstractions.
- In simpler terms, classes should depend on abstractions (interfaces or abstract classes) rather than concrete implementations.

**Why it's important:**
- **Decoupling:** Reduces dependencies between classes/modules, making the codebase more flexible and easier to maintain.
- **Testability:** Enables easier unit testing by allowing mock objects and stubs to be used.
- **Reusability:** Encourages code reuse through abstractions and interfaces.

**Example in Depth:**

Consider a scenario where we have a high-level `User` class that depends on a low-level `Database` class for data storage.

**Incorrect Approach:**
```java
class Database {
    public void saveData(String data) {
        System.out.println("Saving data: " + data);
    }
}

class User {
    private Database database;

    public User() {
        this.database = new Database(); // Dependency on Database class
    }

    public void saveUserData(String userData) {
        database.saveData(userData);
    }
}
```

**Problems with the Incorrect Approach:**
- The `User` class directly depends on the `Database` class, violating DIP. This makes it hard to change database implementations or mock for testing.

**Correct Approach:**
Use abstractions and interfaces to invert the dependencies.

**Step 1: Create an interface for data storage.**

```java
interface DataStorage {
    void saveData(String data);
}
```

**Step 2: Implement the interface in the low-level module.**

```java
class Database implements DataStorage {
    @Override
    public void saveData(String data) {
        System.out.println("Saving data to database: " + data);
    }
}
```

**Step 3: Modify the high-level module to depend on the interface.**

```java
class User {
    private DataStorage dataStorage;

    public User(DataStorage dataStorage) {
        this.dataStorage = dataStorage; // Dependency injection
    }

    public void saveUserData(String userData) {
        dataStorage.saveData(userData);
    }
}
```

**Step 4: Use dependency injection to provide the implementation.**

```java
public class Main {
    public static void main(String[] args) {
        DataStorage database = new Database();
        User user = new User(database);

        user.saveUserData("User's data");
    }
}
```

**Benefits of the Correct Approach:**
- **Decoupling:** `User` class no longer depends directly on `Database` class, enabling easier changes and testing.
- **Flexibility:** Different implementations of `DataStorage` interface (e.g., `Database`, `FileStorage`, `CloudStorage`) can be used without modifying `User` class.
- **Testability:** Mock objects can be easily used for unit testing `User` class.

**Additional Example:**

Let's consider a scenario with a `NotificationService` that depends on different notification providers.

**Incorrect Approach:**

```java
class EmailNotificationService {
    public void sendEmail(String recipient, String message) {
        System.out.println("Sending email to " + recipient + ": " + message);
    }
}

class NotificationService {
    private EmailNotificationService emailService;

    public NotificationService() {
        this.emailService = new EmailNotificationService(); // Dependency on EmailNotificationService
    }

    public void sendNotification(String recipient, String message) {
        emailService.sendEmail(recipient, message);
    }
}
```

**Correct Approach:**

```java
interface NotificationProvider {
    void sendNotification(String recipient, String message);
}

class EmailNotificationService implements NotificationProvider {
    @Override
    public void sendNotification(String recipient, String message) {
        System.out.println("Sending email to " + recipient + ": " + message);
    }
}

class NotificationService {
    private NotificationProvider notificationProvider;

    public NotificationService(NotificationProvider notificationProvider) {
        this.notificationProvider = notificationProvider; // Dependency injection
    }

    public void sendNotification(String recipient, String message) {
        notificationProvider.sendNotification(recipient, message);
    }
}
```

**Usage:**

```java
public class Main {
    public static void main(String[] args) {
        NotificationProvider emailProvider = new EmailNotificationService();
        NotificationService notificationService = new NotificationService(emailProvider);

        notificationService.sendNotification("example@example.com", "Hello!");
    }
}
```

**Benefits of the Correct Approach:**
- **Decoupling:** `NotificationService` depends on the abstraction (`NotificationProvider`) rather than a specific implementation.
- **Flexibility:** Different notification providers can be easily swapped without modifying `NotificationService` class.
- **Testability:** Mock notification providers can be used for testing `NotificationService`.

### Summary:
The Dependency Inversion Principle encourages designing software with abstractions and interfaces, allowing high-level modules to depend on abstractions rather than concrete implementations. This leads to reduced dependencies, increased flexibility, and improved testability.


Here's the summary table for all the SOLID principles without the examples column:

| Principle                             | Definition                                                                                              | Key Benefits                                        |
|---------------------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| **Single Responsibility Principle**   | A class should have only one reason to change, meaning it should only have one job or responsibility.   | Easier maintenance, enhanced readability, reduced complexity |
| **Open/Closed Principle**             | Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. | Improved flexibility, easier to extend functionality, reduced risk of breaking existing code |
| **Liskov Substitution Principle**     | Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. | Promotes code reusability, maintainability, supports polymorphism |
| **Interface Segregation Principle**   | Clients should not be forced to depend on interfaces they do not use.                                    | Reduced coupling, increased modularity, enhanced scalability |
| **Dependency Inversion Principle**    | High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. | Reduced dependencies, improved testability, enhanced flexibility |

### Summary:

- **SRP (Single Responsibility Principle)**: Focuses on classes having a single responsibility or reason to change.
- **OCP (Open/Closed Principle)**: Emphasizes designing classes that are open for extension but closed for modification.
- **LSP (Liskov Substitution Principle)**: Ensures subclasses can replace their parent classes without affecting the program's correctness.
- **ISP (Interface Segregation Principle)**: Promotes using specific interfaces rather than a general-purpose one, reducing dependencies.
- **DIP (Dependency Inversion Principle)**: Suggests that high-level modules should depend on abstractions rather than concrete implementations.
