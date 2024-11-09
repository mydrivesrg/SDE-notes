\?# ThaughtWorks:

## Round 1: Code Pairing Round:
- Able to understand existing code
- Can able to add new backend logic in code with support
- Has knowledge of SOLID principles, Java, Springboot
- Able to pickup hints
#### Areas of improvement:
- Needs to be more proficient in Springboot
- Should practice writing Clean code
- Should try understanding Java docs


## Round 2: Technical Interview 2:
- Technical depth and breath will be accessed
- In depth knowledge on Java, Springboot, microservices and mentioned tech stack on resume
- Why should you use React over Angular?
- Explain project in detail -> challenges-> tech stack you are currently utilizing in your project -> why using these tech stacks only why not some other?
- Project Architecture
- Current Tredns in market in terms of technology
- Database design
- Problem solving skill
- LLD system Design problem
- Design Patterns
- FE + BE + Cloud + CICD + TDD
- Design Principles
- Adjacent Technologies
- Self awareness of skills and experience
- Self learning
- Node js, Python


# Review & Analysis:
- Overconfidence
- project explaination and architecture
- not being confident
- explained Java and spring well but not sufficient
- Why using dependency injection
- Microservices connection
- Messaging Queue -> Learn RabitMQ or Kafka
- Store procedures and triggers
- Remove python from resume
- learn Stream properly
- improper introduction due to nervousness
- field or constructor which one better
- others backend options in java
- considering "ho hi jayega"

---------------------------------------------
# Received Reviews from the Recruiter:
- Can explain functional side of the project
- Has basic knowledge of Java
- Don't have knowledge of various annotations provided in spring framework and when to use them
- He gives up to early
- Has basic knowledge of java however when probed there is lack of deeper understanding,
- **Was not able to explain use of Dependency injection in springboot**
- **How to compare identities of two java objects**
- Was not able to put an architectire diagram and explain what are the components and how the components interact with each other.
- 
------------------------------------------------------------------------------
# Lets start preparing for Technical Interview 2:

## 1. Why you are using React js Over Angular?
- I thing management choose React over Angular because its features which can make it better than Angular like:
- 1. React us easier to learn as compare to angular as its syntax is easy.
- 2. React uses Virtual DOM concept but angular directly works with real Dom. It updates only the parts of the DOM that have changed, which results in faster and more efifcient updates compared to Angular's full DOM manipulation.
- 3.  And also if any fresher is coming into the project who knows javascript then react would be easier to learn for him, but for angulat he has to learn the complete framework and typescript also.
- 4.  Also React is lightweight in nature as compare to Angular this makes it faster to load.
- 5. Also in React we can reuse the components. 
I think because of this benefits of React over Angular management has chooses React over Angular.

## 2. Why are you using SpringBoot over other microservices like Node js and Python?
- In past I was completing one course in which there was a portion of node js also and there I got to know that node js is easier to learn as compare to springboot if you kno basics javascript concepts but for developing enterprize level application mostly developers are using springboot like in our project also because Springboot has a benefits over node js or other frmaeworks like:
- 1. Like the easyness for doing database transaction using ORM tools like JPA, springboot auto configures the connection for us, this motivates us to focus more on writing business logic instead of doing configurations.
- 2. Also after creating the Sprongboot application we don't need to configure the server to run our application it automatically configures Tomcat server for us to run our application.
- 3. It also supports microservices architecture strongly, As per my information node js also supports microservices architecture but needs one more different liabrary which is Express js.
- 4. As most of the companies are using Java, Sprongboot for backend so definitely it has big community support also.
the reasons like this management might have cosidered while selecting Springboot for developing backend for ERM. 

## 3. Current Trends in Market?
Talking about current trends in market, we can say:
- 1. Artificial Intelegence and Machine Learning:
- 2. Also Cloud compouting is something everyone is looking at, like companies don't want to waste their resources on managing the infrastructure so they are using Cloud services like AWS for better performance and efficiency.
- 3. IOT devices : As I am working for Energy client which is mainly in business of energy generatio and distribution so client has their own meters which uses IOT for getting data from the consumer's meters.
- 4. 5G technology ->
- 5. Also DevOps is becoming standard in software development, promoting CICD.
This are the few Current trends in Market also ChatGPT also the trens we can.

## 4. Polymorphism and its types?
Basically polyphormism means having many forms like having many form for same function name,
So in java we have two types of polymorphisms:
1. Method Overloading: Compile Time Polymorphism -> this means in same class there are two methods with same name but the arguments they are accepting are different.
2. MEthod OverRiding: Run Time Polymorphism -> This means there are two classes like Parent and Child there is a method in Parent class with specific parameters, and the method is there in Child class also with same name and same parameters.
---------------------------------------------------------------------------------------------
## 5. Collections in Java?
The collection framework contains multiple interfaces where every interface is used to store a specific type of data.
For example: ArrayList, LinkedList, HashSet, HashMap, Queue, List

## 6. Explain working of HashMap?
- HashMap is a part os Java's Collections Framework and provides the basic implementations of the Map Interface.
- It stores key-value pairs and allows for fast retrieval, insertion, and deletion of elements.

### Key Concepts:
#### 1. Hash Function:
- HashMap uses s hash function to compute an index(also known as a hash code) from the key.
- This index determines where the key-value pair should be stored in the internal array(bucket array).

#### 2. Buckets:
- A bucket is essentially a slot in the internal array.
- Each bucket can store multiple key-value pairs in case of hash collisions.

#### 3. Collision Handling:
- When multiple keys has to the same index(bucket), it results in a collision.
- HashMap handles collisions using chaining, where each bucket contains a linked list of entries that share the same hashCode.

#### 4. Load Factor:
- The load factor is a measure of how full the HashMap can get before it needs to resize the internal array.
- The default load factor is 0.75, meaning when 75% full, it will resize and rehash the entries.

### Working Mechanism:
#### 1. Put Operation:
When you add a key-value pair to a HashMap using the `put` method, the following steps occur:
- 1. **Hash Calculation:** The hash code of the key is calculated using the hash function.
- 2. **Index Calculation:** The hashcode is then converted to an index in the internal array.
- 3. **Insertion:** if the bucket at the calculated index is empty, the key-value pair is added. If the bucket is not empty, the linked listis traversed to ckeck if the key already exists. If it does, the value is updated. If it doesn't, a new entry is added to the linked list.

#### 2. Get Operation:
When you retrieve a value using the `get` method, the following steps occur:
- **Hash Calculation:** The hash code of the key is calculated.
- **Index Calculation:** The hash code is converted into an index in the internal array.
- **Retrieval:** The bucket at the calculated index is checked. If the bucket is empty, `null` is returned. If the bucket is not empty, the linkedlist is traversed to find the entry with the matching key, and the associated value is returned.

#### 3. Remove Operation:
When you remove a key-value pair using the `remove` method, the following steps occur:
- **Hash Calculation:** The hashcode of the key is calculated.
- **Index Calculation:** The hash code is converted to an index in the internal array.
- **Deletion:** The bucket at the calculated index is checked. If the bucket is not empty, the linked list is traversed to find the entry with the matching key, and the entry is removed from the list.
------------------------------------------------------------------------
## 7. Java 8 features?
#### 1. Lambda Expression:
- Lambda expressions provide a clear and concise way to represent one method interface using an expression.
- They enable functional programming and can be used to simplify the syntax for creating anonymous classes.

```
// Before Java 8
Runnable runnable = new Runnable(){
  @Override
  public void run() {
    System.out.println("I am Runnable");
  }
};

// with lambda expression
Runnable runnable = () -> System.out.println("I am Runnable");
```
#### 2. Stream API:
- The Stream API is used for processing sequences of elements, such as collections, In functional style.
- It supports operations like filter, map, reduce, find, match, and more allowing for efficient data manipulation.

#### 3. Functional Interfaces:
- Java 8 introduced several functional interfaces in the `java.util.function` package, such as `Predicate`, `Function`, `Consumer`, and `Supplier`.
- A functional interface with a Single Abstract Method(SAM), which can be implemented using Lambda expressions.
```java
@FunctionInterface
interface MyFunctionalInterface {
  void myMethod();
}

MyFunctionalInterface myFunctionalInterface = () ->System.out.println("Hello World");
myFunctionalInterface.myMethod()

```
#### 4. Default and Static method in Interfaces:
- Interfaces can now have default and static methods.
- Default methods provide a way to add new methods to existing interfaces without breaking the implementing classes.
- Static methods can be called on the interface itself. No need to implement this methods in subclasses.

```java
interface MyInterface {
  default void defaultMethod() {
    System.out.println("defaultMethod");
  }

  static void staticMethod() {
    System.out.println("staticMethod");
  }
}

class MyClass implements MyInterface {
  @Override
  public void defaultMethod() {
    System.out.println("MyClass.defaultMethod");
  }
}

public class Main {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.defaultMethod();
    MyInterface.staticMethod();
  }
}
```
#### 5. Optional Classes:
- The `Optional` class is a container object which may or may not contain a non-null value.
- It helps in avoiding null checks and `NullPointerException`.
- It provides methods like `isPresent()`, `ifPresent()`, `orElse()`, and `orElseGet()`.
 **Go more deep**
#### 6. Date and Time API(Java.time.package):
- Java 8 introduced a new date and time API in the `java.time` package, which is more comphresive amd powerful than the previous `java.util.date` and `java.util.Calender` classes.
- It includes classes like `LocalDate`, `LocalTime`, `LocalDateTime`.
```java
LocalDate today = LocalDate.now();
System.out.println(today);
```
-------------------------------
## 8. JPA Query or NativeQuery?

### Which one to use in Your Project?
#### JPA Query(JPQL): 
- Use JPA Queries for standard CRUD operations and moderately complex queries where portability, maintainability, and Integration with the JPA entiry lifecycle are important.
#### NativeQuery:
- Use Native queries for performance-critical operations, complex queries that JPQL cannot handle, or when you need to laverage specific database features.

In my project also we are using as per the requirement and the complexity of the operation.

---------------------------------------------------
# 9. Class diagram?
----------------------------------------------

## 10. Types of Keys in Database
so in databases we have different types of keys like primary key, foreign key, unique key, candidate key:
#### Primary Key:
- A unique identifier for each record in a table.
- **Characteristics:**
- **Uniqueness:** No two rows can have same primary key value.
- **Not Null:** A primary key value cannot be null.
- Usually a single column but can be a composite key(multiple columns)
- ```employee_id INT PRIMARY KEY```

#### Foreign Key:
- A field (or collection of fields) in one table that uniquely identifies a row of another table.
- **Characteristics:**
- It creates a link between two tables.
- Ensures referential integrity of the data.
- The foreign key in the child table points to the primary key in the parent table.
```FOREIGN KEY (department_id) REFERENCES departments(departments_id);```

#### Unique Key:
- A constraint that ensures all values in a column or a group of columns are unique across the table.
- No two rows can have the same value for the unique key.
- Can contain a null but only once.

#### Candidate Key:
- A column, or set of columns, that can uniquely identify any database record without referring to any other data.

----------------------------------------------------
## 11. DNS lookup. load Balancing and how server works?

### DNS Lookup:
- DNS(Domain Name System) lookup is the process of translating a domain name like(www.satish.com) to IP address.
- DNS is like a phonebook for the internet, mapping human-readable domain names to numerical IP addresses that computers use to communicate.

### Load Balancing:
- Load balancing is the process of distributing incoming network traffic across multiple servers to ensure efficient utilization of resources, maximum throughput, and enhance reliability by avoiding overloading individual servers.

#### How it Works?
- **Traffic Distribution:**
- A load balancer sits between clients (such as web browsers) and a group of backend servers.
- It distributes incoming requests across these servers based on predefined algorithms.

- **Health Checks:**
- Load balancers monitor the health and performance of backend servers using health checks.
- Unhealthy servers are temporarily removed from the pool to avoid serving requests to faulty servers.

- **Scalability:**
- Load balancing enable horizontal scaling by adding more servers to handle increased traffic, ensuring that the system remains responsive and available even during high load conditions.

- **Fault Tolerance:**
- Load balancers improve fault tolerance by providing redundancy. If one server fails, the load balancer redirects traffic to healthy servers, minimizing downtime.


## How Servers Work:

**1. Request Handling:**
   - **Receive Request:** When a server receives a request (e.g., HTTP request for a web page), it processes the request based on the application or service running on the server.
   - **Processing:** The server executes the necessary code, retrieves data from databases or other services, and generates a response.
   - **Response:** The server sends the response back to the client (e.g., web browser) that made the request.

**2. Server Software:**
   - Servers run specialized software to handle requests, such as web servers (e.g., Apache HTTP Server, Nginx), application servers (e.g., Tomcat, JBoss), database servers (e.g., MySQL, PostgreSQL), etc.
   - Each type of server software is designed for specific purposes, such as serving web pages, running applications, or managing databases.

**3. Protocols:**
   - Servers communicate with clients using protocols like HTTP, HTTPS, FTP, SSH, etc., depending on the type of service they provide.
   - For example, web servers use HTTP/HTTPS protocols to serve web pages, while database servers use protocols like MySQL, PostgreSQL, or Oracle's proprietary protocols to handle database queries.

**4. Scalability and Redundancy:**
   - To handle increasing traffic or ensure high availability, servers can be scaled horizontally by adding more servers (load balancing) or vertically by upgrading hardware resources (CPU, RAM, storage) of existing servers.
   - Redundancy is achieved by deploying multiple servers in a cluster or using failover mechanisms to ensure continuity of service in case of server failures.

Overall, DNS lookup, load balancing, and server operations are fundamental components of modern network infrastructure, ensuring efficient and reliable communication and service delivery over the internet.
---------------------------------------------------------------
## 3. Difference between Segmentation ang Paging?
- This are the schemas used in operating systems to manage how programs are stored in menory.

#### Segmentation:
- **Logical Division:** Segmentation divides the program into logical units, such as functions, arrays, or stacks.
- Each segment can grow or shrink independently.
#### Paging:
- **Fixed Size Division:** Paging divides the program into fix-sized pages.
----------------------------------------------------
## 12. a. What is distributed system?
- A distributed system is a group of computers or devices that work together to solve a problem or perform a task.
- Instead of relying on a single central computers, tasks and data are distributed across multiple computers, often connected over the network.

- **Characteristics:**
- *Decentralized:* There's no single computer controlling everything. Tasks are distributed across multiple computers or devices, called nodes.
- *Communication*: Nodes communicates with each other over the network.

## 12. What is Kafka?
- Apache Kafka is an open-source distributed event streaming platform used for building real-time data pipelines and streaming applications.


## 13. What is Jenkins?
- Jenkins is an open source automation server used for continous integration(CI) and Continous Delivery(CD) of software projects.
- It is designed to automate varuous tasks like buiding, deploying the software.

- **Key Concepts in Jenkins:**
- *Jobs:* Tasks or Processes in Jenkins, such as building, deploying, or cleaning up.
- *Pipeline:* A series of jobs or stages that define the entire software delivery process, from code commit to deployment.
- *Build:* The process of compiling source code, running tests, and creating artifacts (e.g., executable files, packages)
- *Integration:* Integration with version control systems(e.g., Git, SVN) build tools(e.g., Maven, Gradle), and deployment tools for end-to-end automation.

- **Use Cases:**
- *Continous Integration->* Automatically build and test code changes as they are commited to version control, ensuring code quality and identifying issues warly.
- *Continous Delivery(CD)->* Automate deployment processes to deliver software releases quickly and reliably to production environments.
- *Scheduled Jobs->* Schedule tasks such as backups, cleanups, and maintenance activities to run at specific times.

## 14. What is Docker?
- Docker is a platform and toolset used to develop, deploy and run applications in containers.
- Containers are lightweight, portable, and isolated environments that package software and its dependencies, making it easy to build, ship, and run applications consistently across different computing environments.

- **Key Concepts in Docker:**
- *Docker Images->* Blueprints or templates that define what goes into a container, including the application, dependencies, and configuration.
- *Container->* Running instances of docker image. Eac container is isolated and contains everything needed to run the application.
- *Dockerfile->* A text file that defines the steps to create a Docker image, specifying the base image, dependencies, commands, and configurations.
- *Docker Engine->The core component of docker that manages containers, images, networks, and storage*
- *Docker hub->* a public repository/registry where Docker images are stored and shared, allowing developers to access pre-built images or publish theiur own.

- **Use Cases:**
- solves a major problem its working fine in my machine

## 15. Developers point of view?
- mindset of a software developer when approaching tasks, challenges, or decisions related to software development.
- It encompasses various aspects such as `coding practices`, `problem solving approaches`, `design considerations`, and `collaboration with team member`.

- **1. Problem Solving:** Developers approach problem analytically, breaking them down into manageable parts and designing solutions using algorithms, data struatures, and programming language.

- **2. Coding Practices->** Developers adhere to coding best practices writing clean, efficient, and maintainable code. This includes following coding standards, using meaningful variable names, writing comments for clarity, and applying design patterns where appropriate.

- **3. Testing and Quality Assurance:** Developers emphasizes testing their code thoroughly, including unit testing.

- **4. Continous LEarning:** Developers have a growth mindset, continously learning new technologies, tools, and techniqies to improve their skills and stay updated with industry tredns.

- **5. Collaboaration:** Developers value colaboaration and teamwork, working closely with other team members such as designers, product managers, and testers to deliver high-quality software.

- **Problem Ownership:** Developers take ownership of the problems they work on, taking initiative, being proactive, and finding creative solutions.
- They are resourceful in rsolving issues and overcoming challenges that arises during development.

## 16. Requirement gathering phase?
The requirement gathering phase, also known as requirements elicitation or requirements gathering, is an essential stage in the software development lifecycle where stakeholders and development teams gather, document, and analyze the requirements for a software project. Here's an explanation of the requirement gathering phase:

### Overview of Requirement Gathering Phase:

1. **Identifying Stakeholders:** The first step is to identify and involve stakeholders who have a vested interest in the software project. Stakeholders can include clients, end-users, business analysts, project managers, and technical teams.

2. **Understanding Needs:** Stakeholders and development teams collaborate to understand and clarify the needs, objectives, and goals of the software project. This includes gathering information about business processes, user requirements, functional specifications, and technical constraints.

3. **Eliciting Requirements:** Techniques such as interviews, surveys, workshops, brainstorming sessions, and use case analysis are used to elicit requirements from stakeholders. The goal is to gather comprehensive and accurate information about what the software should do and how it should behave.

4. **Documenting Requirements:** Requirements are documented in detail, usually in the form of requirement documents or specifications. These documents capture functional requirements (what the software should do), non-functional requirements (performance, security, usability), and system requirements (hardware, software, integrations).

5. **Analyzing and Prioritizing:** Once requirements are gathered, they are analyzed to ensure they are clear, complete, consistent, and feasible. Requirements are prioritized based on their importance, impact on the project, and dependencies.

6. **Review and Validation:** The documented requirements are reviewed by stakeholders and development teams to validate their accuracy and alignment with project goals. Feedback is incorporated, and any discrepancies or ambiguities are resolved.

### Importance of Requirement Gathering:

- **Alignment:** Ensures that the software solution aligns with the needs and expectations of stakeholders and end-users.
- **Scope Definition:** Defines the scope of the project, including what features and functionalities will be included in the software.
- **Risk Mitigation:** Identifies potential risks, challenges, and constraints early in the project, allowing for proactive risk mitigation strategies.
- **Cost and Time Estimation:** Helps in estimating project costs, timelines, and resource requirements based on the scope and complexity of requirements.
- **Foundation for Development:** Provides a solid foundation and roadmap for the development, testing, and implementation phases of the project.

In summary, the requirement gathering phase is a critical part of software development, laying the groundwork for a successful project by ensuring clear understanding, alignment, and documentation of project requirements.

## 17. Git -> 
### How i use git?
- In our project, we utilize git extensively for version control and collaboration.
- We follow a feature branch workflow, where each new feature or bug fix is developed pn seperate branch.
- This approach allows us to work concurrently without interfering with each other's code.
- We commit changes regularly with descriptive commit messages, which helps in tracking the progress of the codebase and understanding the purpose of each change.
- Before merginf branches, we conduct thorough code reviews via pull requests to ensure code quality and catch any issues early on.

- Our Git workflow is complemented by Github, where we manage issues, track project progress, and integrate continous integration and deployment processes seamlessly.
 

### Rebase strategy
- Git rebase is a strategy used to incorporate changes from one branch into another by reapplying commits on top of another branch's commit history.

1. **Starting Point:** When you initiate a rebase, Git identifies a common ancestor commit between the branch you're rebasing (let's call it the feature branch) and the branch you're rebasing onto(oftenn the main branch, like `master` or `main`).

2. **Commit Reapplication:**
- Git then "replays" the commits from the feature branch on top of the commit history of the target branch.
- This process involves identifying the changes introduced by each commit on the feature branch and reapplying those changes sequentially.

3. **Resolve Conflicts:**
- If there are any conflicts between the changes in the feature branch and the target branch, Git pauses the rebase process and prompts you to resolve these conflicts manually.
- Once conflicts are resolved, you continue the rebase.

4. **Completing the Rebase:**
- After all commits from the feature branch are successfully reapplied on top of the target branch's commit history, the rebase is completed.
- The feature branch now has a linear commit history, with its changes integrated into the target branch's history

### Taking pull
Taking a pull to add new features or resolve bugstypically involves several steps in Git:

### **1. Update Local Repository:**
- Before starting any new work, ensure your local repository is up to data with the remote repository.
- Use `git pull origin main` (assuming the main branch is named `main`) to fetch and merge changes from the remote main branch into your local main branch.

### 2. Create a Feature Branch: 
- After updating your main branch, create a new branch for the new feature or bug fix.
- Use `git checkout -b feature-branch-name` to create and switch to the new branch.

### 3. Work on the Feature/Bug Fix: 
- Make your changes on the feature branch, following your development process (coding, testing, etc).

### 4. Commit Changes ->
- Commit your changes with descriptive commit messages using `git add .` to stage all changes and `git commit -m "Your commit message"` to commit them.

### 5. Fetch Latest Changes:
- Periodically fetch the latest changes from the remote main branch to ensure your feature branch is bases on the most recent code.
- Use `git fetch origin main` to fetch changes without merging them.

### 6. Resolve Conflicts (if Any):
- If there are conflicts between your changes and the latest changes on the main branch, Git will indicate this during the pull or fetch process.
- Resolve conflicts by editing the affected files, staging the changes (`git add <file>`), and then continouing the rebase or merge process.

### 7. Rebase or MErge:
- Once your feature is ready and conflicts are resolved, you can either rebase your deature branch into the main branch (`git rebase main`) or merge the main branch into your frature branch(`git merge main`).
- Rebase is preferres for maintaining a cleaner commit history, but it requires care to avoid rewriting shared history.

### 8. Test-> After rebasing or merging, test your changes thoroughly to ensure they worj as expected.

### 9. Push Changes : Finally, push your feature branch to the remote repository using `git push origin feature-branch-name`.

### 10. Create Pull Request:
- On the remote repository platform (Github, Gitlab, etc) crete a pull request (PR) from your feature branch into the main branch.
- This PR serves as a review and integration point for your changes.

### Why we create hotfix branches
A hotfix branch is a type of branch creates in Git specificall to address critical issues or bugs in `production environment`.

- A hotfix branch is a short-lived branch created from the main branch (often master or main) to quickly fix critical issues or bugs found in the production environment.
- Unlike regular branches, which focus on developing new feature or enhancements, hotflix branches are created in response to urgent issues that require immediate attention and deployment.

### Purpose of Hotfix Branches:
- **Rapid Response:** Hotfix branches enable development teams to respond swiftly to critical issues or bugs that impact the production environment's stability or functionality.
- **Isolation of Changes:** By creating a separate hotfix branch, developers can isolate and focus solely on fixing the critical issue without affecting ongoing development work in other branches.
- **Minimize Disruption:** Hotfix branches help minimize disruption to the main development workflow. They allow the team to address urgent issues without interrupting ongoing feature development or waiting for the next regular release cycle.
- **Deployment Control:** Hotfix branches undergo testing and validation to ensure the fix is effective and does not introduce new issues. Once validated, the hotfix can be deployed to the production environment independently of other ongoing development activities.

### WorkFlow of Hotfix Branches:
- Identify the critical issue or bug in the production environment that requires immediate attention.
- Create a hotfix branch from the main branch using git checkout -b hotfix-branch-name.
- Make the necessary changes and fixes on the hotfix branch.
- Test the hotfix thoroughly to ensure it resolves the issue without introducing regressions.
- Merge the hotfix branch into the main branch (master or main) and any other relevant long-term branches (e.g., develop) after testing and validation.
- Deploy the hotfix to the production environment once it's approved and ready.




======================================================
#### Experience:
- Be prepared on past experiences -> prepare 3 stories well
- Exception Handling
- String
- MultiThreading
- 20 coding practice
- Be confident
- 
