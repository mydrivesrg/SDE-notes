# Razorpay - Product Development Engineer - 07/06/2024

## 1. HAckerearth Test: 3 coding problems on DSA

## 2. Machine Coding Round:
- Problem on designign a car parking system for different types of vehicles.
- Note: Was able to design the solution successfully

19:06:2024 -> Received the feedbacl and qualified for next round -> 

## Review and Mistakes:
- Not implemented any design patterns in LLD problem  -> Practice needed
- Not created seperate packages for service   ->  Practice Needed 
- Confident -> Was confident during this interview

-----------------------------------------------
## 3. Hiring Manager Round:

- thorough evaluation in terms of skill set as well as cultural fit.
- Past work history
- Situational questions
- Behavioural traits
- interviewer will also try to understand your interest, ambitions, and alignment.

## Tips:
-  Be true self and reflect on your resume and past experiences.
-  Ask more questions about the organization
-  Learn more about the Job description and answer how your profile is matching this role.

# Sample Questions:
- describe project and architecture
- API design principle
- springboot questions
- willing to relocate
- how do you align yourself with the job description
- Why you want to join razorpay
- What are your goals here
- What do you prioritize most at work


Here are 30 possible questions that a Hiring Manager might ask for a backend development role with the given requirements:

1. **Technical Expertise:**
## 1. Can you explain your experience with Golang, Java, PHP, Python, Ruby, or J2EE?
 
## 2. Describe a project where you built a feature from scratch. What was your approach?
- In CRM module, while developing an complaint management tool I got one task for creating an Email service.
- The requirement was something like that, there will be different triggers and for all those triggers we could use the same service.
- First I understood the requirement properly, and I had few doubts like what will be triggers, how would be the body. for clearing out these queries I scheduled a call with my product owner and got the queries clarified.
- Before that also I learnt email service but not in depth, so I gone through the official docs of spring for latest updates for email implementation.
- Then I started working on it, created one feature-branch, created one service class for Email service and used EmailSender in that along with MimeSender because the body couldn't be just a text it can be web pages also.
- And for Email I created a seperate class so that it would be easy to accept any changes in future.
- After the development commited the code to main repo and raised PR.
- Like this I approached this feature adding from the scratch. 

## 3. How do you ensure the scalability and performance of your applications?
- To ensure the scalability and performance of my application I will take few steps in different phases:
- Like in development phase I'll always focus on optimising the code  like by using techniqies and tools. like using stream API instead of forloop.
- In testing phase, I'll set up one special team for just to find the performance bugs.
- Also I;ll use tools like sonarQube for code review, here I will get a code smells in my code.
- Also I'll ensure codecoverage is as max as possible.
- Also if my application is monolithic, I'll break it down into microservices so that independent deployment and development of the application can be possible.
- Coming to deployment phase, I'll use Auto-Scaling techniques, API gateway and I'll prefer using Cloud tools like AWS to deploy my application, so that if during a specific the traffic is more then I can scale hirizontally and vertically as required.
- So these are few techniqies I'll follow to ensure scalability and performance of my application.

## 4. Explain the architecture of a recent system you've designed.

![image](https://github.com/Gavh2909/NOTES-QUESTIONS/assets/87062915/32075ece-5442-43ef-b91e-ae84353e80fd)

 - This is one of my personal project, which is vehicleWallet.
 - The userbase for this application will be any type of vehicle owners.
 - One user can add 3 vehicles under his name and can track the fuel expenses, consumption using the application.
 - Curretly I am developing this as monolith only even if it has 4 major services now 1. UserService 1. VehicleService 3. EntriesService 4. Reporting Service.


## 5. How do you handle API versioning in your projects?
- 

## 3. **REST APIs:**

## 1. What are REST APIs and why are they important?
   
## 2. How do you ensure the security of REST APIs?
- So in our project we're using Spring Security to handle the securuty part of the application.
- While developing the APIs we're getting it clarified the authorization of that API like which type of user can access it, it should be secured or general users also can access it like that.
- Suppose I;m developing API which is adding a new feature which will be beneficial for NRG's Consumers so in this case no one other that the Consumers shouldn't access it so using requestmatchers we're securing this APIs.
- 

## 3. Can you describe a challenging REST API integration you worked on?
- So initially I was not that much familier with how microservices connects, so while developing the Ticketing tool while connecting ticketing service with Apollo support group I faced few challenges but later I learnt how we can connect it using REST APIs and feign client.
- What happens here We creates a FeignClientService in out Support service with giving few parameters in that annotation, so like this it automatically gives us the instance of that another microservice.

## 4. How do you handle error responses in your APIs?
- To handle the error response in APIs I'm designing I'm mostly using ResponseEntity class provided by Springboot.
- Using this we can pass the response with different parameters like header, body, and status code also.
- SO if there is any error then I'm passing the possible error as header or body and passing related status code also.
- Example - []
- Using this we can throw different type of message or status code for different errors.

4. **Product Design and User Requirements:**
## 1. How do you gather and understand end-user requirements?
- Mostly I'm getting requirement from the functional team which is at the onsite location.
- They are planning rolling out new features as per the Management planning decisions and the problems their userbase is facing.
- After getting the requirement, If I'm having any query or doubt for that particular requirement then I'm approach to my lead and if he also doesn't understood the requirement then we're scheduling a call with functional team and we're getting that qiery clarified before working on that.
- So like this I understdns the end-iser requirements.

## 2. Can you give an example of a time when you translated user requirements into technical solutions?

## 3. Describe your process for formulating use cases.

5. **Programming Languages:**
## 1. How do you decide which programming language to use for a particular project?
- for deciding which language will be better for particular project I'll definitely take few aspects into the considerations, Like.
- I'll understand the project requiremtnt first,

## 2. Describe your experience working with dynamic languages like PHP, Python, or Ruby.
- I have not got the opportunity of working in PHP and Ruby, but in Python like 2 years before I did completed a course on Python and I'm falilier with the python concepts.

## 3. What challenges have you faced when working with multiple programming languages in one project?
- so in my personal project, I am working on both FE and BE side and using React js for FE and Springboot for BE.
- so the problem I am facing while working on two technologies at a time is, we can say as I am using both on same project na, so their is hurryness we can say like if doing something in BE suppose, then directly going to FE and trying to implement it.So sometimes this is leading to failure.

6. **Problem-Solving and Innovation:**
   1. Describe a problem you faced in a project and how you solved it.
   2. How do you approach brainstorming for new product features?
## 3. What innovative solutions have you proposed or implemented in your previous roles?
- One solution I proposed that wasn't that much innovative but they felt it will be beneficial.
- So what happened there was few problems client was facing, so what they did they listed down all the problems there was almost 34 small and big size problems, so what they did they arranged one 4 hours *Ideation session* and it was mandatory for all to join.
- So there was one issue on a screen, they have recently acquired *Vivant Home Automation* company and they wanted to do something so thet even NRG consumers could be aware about the VIVANT's products.
- So what I suggested is offering a Home Automation products to existing NRG consumers with few discounts and to letting them know about the VIVANT's products we can add small windows on their screen so that they will be aware about it.
- That much I suggested and I consider that wasn't innovative but later few more people countered and added their's addons also like one added "if we're having the data for each consumer which appliance of his home is comsuming more units and let's show him Vivant's product as a substitute.
- The team considered this and said they also add more things from their side and in future they will be adding this.

7. **Open Source Contributions:**
## 1. Have you contributed to any open-source projects? Can you describe one?
- I've not got the opportunity of working on open source projects.
- But whenever I'm getting a free time I'm working on one of my personal project, and for that I'm developing both frontend and backend side.
  
## 2. How do you manage your time between professional work and contributing to open-source projects?
- I've not got the opportunity of working on open source projects.
- But whenever I'm getting a free time I'm working on one of my personal project, and for that I'm developing both frontend and backend side.
- Mostly on weekends I'm working on this project.
  
## 3. What do you see as the benefits of contributing to open-source projects?
- 

8. **Product Company Experience:**
## 1. What is your experience working in a product company?
- So as I am currently working at Cognizant which is not a product based company, but the client I'm working for is a product company which is in business of energy generation and distribution in US and Canada region.
- Like main benefit of working on product company is you will be doing innovative things, like if there is a particular product then there will be competetors for that product and to suatain in the market the company will try to thing in innovative way like adding new features which are not there in the competetors products.
- Like we can say the amount of services RazorpayX is providing, so there is no competor who is providing that much services in one product.

## 2. How do you balance feature development with maintaining existing products?
- 

## 3. Describe a time when you had to make a trade-off between product quality and delivery deadlines.
- for delivery deadlines I always do effiective time management, like that particular task has this much importance and urgency so it should be completed at any cost.
- But sometime it happens like, if I am feeling like for delivering this before time I might phase a difficulty, then am asking for help from team members or requesting lead for a help, So if he feels he can help and the task can be done earlier then he's heping or transfering this to a person who have experience of working on this kind of tasks.


9. **Payment Infrastructure:**
## 1. What is your experience with payment systems or financial technology?
- I have basic knowledge of like UPI and who maintains it and how it is being maintained.
- Also other financial terms like cash flow in organization, What is Escrow account and how it works in industry.
- Also how the UPI became powerful year-by-year so this are things I am aware of. 

## 2. How would you design a payment gateway to handle millions of transactions per day?
- To design a payment gateway I will design a backend in such a way that in less time it should be able to multiple requests.
- Also I'll be taking care of one request should not disturb other.
- After developing the gateway, next thing I'll do is, I will enable adding multiple servers if more requests are coming to the system, we call it as a horizintal scalling.

## 3. What are the key security considerations when building payment infrastructure?
- While developing a payment infrastructure we should take few aspects in the mind like no one should hack out system, the atomicity should be there, the consistenchy should be there.
- Like if the payment is started then it should ne wither successfull or fail.
- Like if money is deducted from senders bank then it should be credited in the receivers account.


10. **Learning and Adaptability:**
## 1. Can you describe a time when you had to quickly learn a new technology or programming language?
- So in my project, during one sprint I got one task to implement email functionality, so at that time I was completely unaware about the email-functionality in springboot.
- Then I learnt this concept through official documentation and YouTube videos.
- Ans was able to complete the assigned task before due date.

## 2. How do you stay up-to-date with the latest developments in software engineering?
- Before joining CTS na, I used to learn the technologies from uTube, like I learnt Java, Javascript and React js before joining CTS.
- But after joining CTS, I got to know that CTS supports much for Learning and has a dedicated learning platform and all employees have free Udemy access.
- So from that time I started completing Udemy courses, and since I joined I am continously learning one technology at a time.
- My target is learning one new technology or enhancing knowledge is existing skillset during each 2 months.
- Thats how I completed Udemy AWS course last year and later applied for free AWS official certification voucher and they provided also, and in September last year I was able to complete the Official AWS certification exam.
- Now also for next 2 months, like before leaving CTS I want to complete Generative AI course here.

## 3. What new technologies are you interested in learning and why?
- I am interesting in adding more knowledge of AWS like going more deep into AWS.
- And also I would like to learn the DevOps part like how our applications are getting deployed in PROD env using Jenkins, Docker, Kubernetes and for this na in AWS also there are supportive services like elastic Container Services, Elastic Kubernetes services, so overall I would love to learn CICD using AWS.
- Because ... add by your own

11. **Miscellaneous:**
## 1. Can you show some of your weekend side projects on GitHub and explain them?
- Show Fueltracking and CES email sender project

## 2. How do you prioritize tasks when working on multiple projects simultaneously?
- In cognizant, at one time I have worked on one project only, but if you ask me working on multiple tasks.
- I am always sorting out the tasks as per the priority, like the feature needs to be implemented at any cost and I'm working on them first.
- My second priority is completing the bug fixing tasks and small feature implementation, and taking help from peer team members if needed.
- And if any task I'm not able to complete and which might affect the final delivery then I am convenying my lead to assist me doing it or still I'm unable to do it them I'm requesting lead to transfer it to someone who can work efficiently on it.
Like this I am prioritize the tasks

## 3. What are the most important factors you consider when designing a scalable system?
- For designing a scalable system most important factors I consider are:
  - Using a microservices design pattern
  - Following design patterns and principles to design the logics.
  - For deploying also I'll take care of scalability like if during specific hours application is gettiing more load then at that time our application should not go down and it should handle the load without any downtime, like by adding multiple servers.
  - For this I'll choose AWS because it has few services like ELB, Auto-Scaling.
  - So this factors I'll consider while designing the scalable system.

Preparing answers for these questions should help you demonstrate your technical skills, problem-solving abilities, and experience effectively.


---------------------------------------------------------------------------------------------------------------------

## Possible questions on resume:
Here are 30 possible questions that the Hiring Manager might ask during your interview based on the job description and your resume:

### Technical Skills and Experience
## 1. Can you describe your experience with Java 1.8 and Spring Boot in your previous projects?
- On java I'm working since a long time but when I joined current project I started woking on both spring boot and Java in more deeper manner.
- In this project also we're using java 1.8 for the developing.

## 2. How have you implemented RESTful APIs in your projects? Can you walk me through a specific example?
- After getting requirement from the client before started working on that part, we're always ensuring that there are no doubts or queries before started working on it.
- So during the development of Ticketing tool in CRM i got one task for developing API for getting tasks from the ticketing service.
- The requirement was like that built for getting particulat team's tasks and the API should be flexible so that it can provide the tasks as per the asked status "like sending only queries which are in-progress".
- So I figured out the endpoints and got the confirmation from my team lead he suggested few suggestions and then we finalized the endpoints.
- **For getting particular groups tickets: /<-suggest the endpoint->**
- **For getting particular groups and mentioned status tickets: /<-suggest the endpoint->**
- **For getting pending tickets for particular group: /<-suggest the endpoint->**
- Like this I have developed the APIs for this particular task.

## 3. What challenges did you face when transitioning from monolithic architecture to Microservices, and how did you overcome them?
- So before our CRM was fully monilith as it was responsible for handling very less operations.
- But later client decided to add ticketing tool then it will not good for future like adding ticketing tool also in this monolith, so we decided to transition the application into microservice.
- As I was also part of this team, before this I was completely unaware about how to working on microservices applicarion, So before started working on this we arranged one one-weeks training session on microservices using springboot.
- After this session I was aware about the overall working of microservices, and explored few things by myself.
- Later started working on this, faced few problems while connecting the microservices but was able to manage them.
- and Now CRM is microservices application ans has 4 major services 1. User service, 2. Ticketing service, 3. Group service, 4. Plan Service.


## 4. Describe your experience with React.js. How did you use it in the Excellergy Revenue Manager project?
- When I joined CTS, I got tagged to Java Full stack domain, and in this domain path React js was also mandatory learning.
- So at that time I learnt React, I was already aware about Javascript so when I started learning React it benefitted me too much, and created my interest for diving deeper in React.
- Later also after this trainig phase I was tagged to one CTS's internal project, in which I worked as a React Developer, and in this project I used to get tasks like fixing minor bugs only.
- In ERM I am working on backend side only, but here also for CRM they have used React for developing the UI.

## 5. How have you utilized Spring Security in your applications?
- In my project one special team is working on user authentication side.
- In my case I worked on securing the APIs using Spring Security using requestMatchers, I worked on this part. 

## 6. Can you explain the concept of Microservices and its advantages over monolithic architecture?
- Micorservices means insated of developing the entire application as one entity, dividing it into multiple services and developing it independently.
- Talking about the benefits, we can develop and deploy independent services, like in monolith even is we made changes in one service we have to deploy the entire application again.
- Other thing is choosing the freedom to choose programming language and technologies for the development of independent services.
- other benefit is availability as compare to moniloth, in monolith is one part of the application goes down then the entire application can go down, but in microservices is specific service is went down then it will not affect the other services.

## 7. How did you handle data persistence in your projects using JPA and Hibernate?
8. Describe a scenario where you had to implement a feature from scratch. What was your approach?
9. How do you ensure code quality and maintainability in your projects?
10. Can you give an example of how you used AWS in your projects?

### Dynamic Languages and Web Development
11. Do you have any experience with PHP, Python, or Ruby? If so, can you provide examples?
12. How do you approach designing and developing REST APIs for scalability?
13. What are some best practices for developing RESTful APIs?
14. How do you handle user authentication and authorization in web applications?
15. What experience do you have with frontend technologies like HTML5, CSS3, and JavaScript?
16. Can you explain how you used Redux in your React.js applications?
17. Describe your experience with Node.js and Express.js in building backend services.

### Product and Design Discussions
18. How do you approach understanding end-user requirements and formulating use cases?
19. Can you provide an example of a product design discussion you led or contributed to?
20. How do you ensure that your design decisions align with user needs and business goals?

### Open Source and Side Projects
21. Can you talk about any open-source projects you have contributed to?
22. Do you have any side projects on GitHub that you are particularly proud of? Can you describe one in detail?
23. How do you stay updated with new technologies and trends in software development?

### Problem-Solving and Technical Challenges
24. Describe a technical challenge you faced in one of your projects and how you resolved it.
25. How do you approach debugging and troubleshooting issues in your applications?
26. Can you explain a complex problem you solved in one of your projects and the steps you took to solve it?

### Working in a Product Company
27. What was your role in the Medicaps project at Cognizant, and what were your key contributions?
28. How did you collaborate with other team members and stakeholders in your previous projects?
29. Can you provide an example of a time when you had to learn a new technology quickly to deliver a project?

### Miscellaneous
30. Why are you interested in working at Razorpay, and how do you see yourself contributing to our mission of making online payments easy and accessible?

These questions cover various aspects of your technical skills, experience, and problem-solving abilities, ensuring that you are well-prepared for the Hiring Manager round. Good luck with your interview!
