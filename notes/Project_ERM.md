# Exellergy Revenue Manager:
---------------------------------------------------------------------
Client : NRG Energy - North America
- NRG Energy is a North American Energy company which works in the business of energy generation and retail distribution in US and Canada.

*Project Overview: Excellergy Revenue Manager (ERM)*

*Company Name:* NRG - Energy Distribution Company Canada

*Project Title:* ERM - Excellergy Revenue Manager

*Description:*
Excellergy Revenue Manager (ERM) is a web-based application developed using React.js for NRG, an energy distribution company in Canada. ERM is designed to streamline revenue management processes, particularly for billing NRG's customers, generating invoices, and managing customer data. It provides various functionalities such as previewing invoices, forecasting revenue, updating existing data, and handling consumer complaints.

*Working:*
1. *Data Loading:* Usage data is collected from consumers, and ERM loads this data into the system to be used for billing and rating customers.
2. *Billing Process:* ERM utilizes the loaded usage data to generate invoices for NRG's customers. It calculates billing amounts based on the usage data and any applicable rates.
3. *Preview and Forecast:* Before finalizing invoices, ERM allows users to preview them to ensure accuracy. Additionally, it provides forecasting capabilities to estimate future revenue based on projected usage data.
4. *Data Management:* ERM enables users to update existing data and perform various operations in response to consumer complaints or changes in billing information.

*Features:*
1. *Usage Data Management:* Efficiently manage and load usage data from consumers into the system.
2. *Billing and Invoicing:* Automatically generate invoices for NRG's customers based on their usage data and applicable rates.
3. *Preview and Forecast:* Preview invoices before finalizing them and utilize forecasting features to estimate future revenue.
4. *Data Updating:* Allow users to update existing data and perform necessary operations in response to consumer complaints or changes in billing information.


------------------------------------------

Based on the description of services in your project, here are potential microservices and their corresponding entity classes for microservices development using Spring Boot:

1. **Billing Microservice:**
   - Entity Class: Billing, Invoice

2. **Usage Data Management Microservice:**
   - Entity Class: UsageData, Consumer

3. **Forecasting Microservice:**
   - Entity Class: RevenueForecast

4. **Customer Management Microservice:**
   - Entity Class: Customer, Complaint

5. **Integration Microservice (e.g., CRM Integration):**
- Entity Class: CRMData

6. **Reporting Microservice:**
   - Entity Class: Report, RevenueTrends
----------------------------------------------------------------------------

## Challenges faced:
 So till now I have worked on two microservices 
 1. Customer Management Micrservice:
-  sO the thing is they have a consumer specific portal Consumer Relationship Manager(CRM) which have features like:
1. Onboarding new consumer[it tracks from registration to complete installation of the services]
2. Handling queries received from consumer and from local NRG authority.[new, inprogress, closed]
 - Initially what used to happed once the consumer raised the complaint it used to directly goes to local authority, and local authority used to go there can solves the query.
 - but in this process consumer was completely unaware about his ticket's current status, and due to this sometimes consumers were unhappy.
 - So in this I worked on once consumer raised the query it comes here in ERM's portal(GET) and I implemented the Email service here so that Consumer receives the Email with link to tract his queries status.
[so initially I was totally unaware about how Email service works, so for this I had to go through the concept properly and also I tool help from my peers for this] 
   4.  
-----------------------------------------------------------------------------------------------------

Here's an improved and expanded version of how you can develop the services using Spring Boot for Customer Management Microservice:

**User: Customer Management Microservice**

1. **Onboarding New Consumer:**
   - Create a dedicated endpoint to handle new consumer registration and onboarding.
   - Collect necessary information such as name, email, address, and service preferences.
   - Trigger the onboarding process that tracks from registration to service installation.

```java
@RestController
@RequestMapping("/onboarding")
public class OnboardingController {

    @Autowired
    private ConsumerService consumerService;

    @PostMapping("/register")
    public ResponseEntity<String> registerConsumer(@RequestBody Consumer consumer) {
        consumerService.onboardNewConsumer(consumer);
        return ResponseEntity.ok("Consumer registered successfully.");
    }
}
```

2. **Handling Queries:**
   - Implement a query management system with statuses (new, in progress, closed).
   - Allow consumers to raise queries and track their status throughout the resolution process.

```java
@RestController
@RequestMapping("/queries")
public class QueryController {

    @Autowired
    private QueryService queryService;

    @PostMapping("/raise")
    public ResponseEntity<String> raiseQuery(@RequestBody Query query) {
        queryService.raiseQuery(query);
        return ResponseEntity.ok("Query raised successfully.");
    }

    @GetMapping("/status/{id}")
    public ResponseEntity<QueryStatus> getQueryStatus(@PathVariable Long id) {
        QueryStatus status = queryService.getQueryStatus(id);
        return ResponseEntity.ok(status);
    }
}
```

3. **Email Notification Service:**
   - Develop an Email service to send notifications for onboarding and query status updates.
   - Include a link in the email for consumers to track their query status directly.

```java
@Service
public class EmailService {

    @Autowired
    private JavaMailSender javaMailSender;

    public void sendEmail(String to, String subject, String text) {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setTo(to);
        message.setSubject(subject);
        message.setText(text);
        javaMailSender.send(message);
    }
}
```

4. **Consumer Service:**
   - Define the business logic for onboarding new consumers and handling queries.

```java
@Service
public class ConsumerService {

    @Autowired
    private EmailService emailService;

    public void onboardNewConsumer(Consumer consumer) {
        // Perform onboarding tasks (e.g., registration, installation)
        // Send onboarding email
        String subject = "Welcome to NRG Services";
        String text = "Dear " + consumer.getName() + ",\n\nWelcome to NRG! Your registration is complete. " +
                      "We will contact you shortly for service installation.\n\nThank you.";
        emailService.sendEmail(consumer.getEmail(), subject, text);
    }
}
```

5. **Query Service:**
   - Manage queries, update their statuses, and send status tracking emails.

```java
@Service
public class QueryService {

    @Autowired
    private EmailService emailService;

    public void raiseQuery(Query query) {
        // Process the query and update its status (new, inprogress, closed, etc.)
        // Send status tracking email
        String subject = "Query Status Update";
        String text = "Dear " + query.getConsumerName() + ",\n\nYour query with ID " + query.getId() +
                      " is now " + query.getStatus() + ". Click here to track its status: [URL]\n\nThank you.";
        emailService.sendEmail(query.getConsumerEmail(), subject, text);
    }

    public QueryStatus getQueryStatus(Long id) {
        // Fetch query status from database or repository
        QueryStatus status = new QueryStatus();
        status.setId(id);
        status.setStatus("In Progress");
        return status;
    }
}
```

In this setup, the `OnboardingController` handles new consumer registration, the `QueryController` manages queries and status tracking, the `EmailService` sends email notifications, and the `ConsumerService` and `QueryService` contain the business logic for onboarding and query handling, respectively.

You can further enhance this setup by adding authentication, validation, error handling, and database integration as per your project requirements.
