# Technologies

We could create this with many languages (like Csharp, Nodejs or Kotlin), but for this example, I decided to use Java + SpringBoot. Spring has a big community with great solutions (despite the verbosity of Java, which can make a little bit confusing for some programmers at first). Well, let's put our plan in practice.
We will create our project and organize it in the following way.

If we have Login, we can construct it using OAuth 2.0. It is an authorization protocol that allows applications to access user data, using tokens which provides security for the user and the application. The user requests authorization on our application, and the app transfers credentials (access token) with OAuth to our server and returns info to the user that the app is accessible.

Database: We will use Postgres to control the data and for more efficiency.<br>
We also use AWS as a cloud system, because of its easy maintenance and excellent service online.<br>
Routing and Messaging: we can use RabbitMQ to control our queue, ensuring and having a strategy for eventual errors. RabbitMQ is a powerful tool which ensures that all data will be delivered in an efficient way. Our messages are published on an exchange that controls them and routes the messages received on the server to one or more queues.<br>
We can use a Direct Exchange, sending the message with specific key (Routing Key).<br>
Resilence4j: a strategy to implement our circuit Breaker, in order to avoid overloading of API, and in status of “Open”, we can controls if an unexpected error occurs, allowing us to forward this message (request) to a waiting queue. 


<img src="/images/resilence.png"><br><br>

Cache: we will use <b>Redis</b>.<br> It is a Store In-memory, it stores data in RAM,which provides extremely fast read and write times (in the order of milliseconds). It results in reducing the latency of PIs that need to respond quickly.

Using Spring Boot Starter Dependencies, you can add specific resources to the project (such as web, security or database). Below is an example using Redis as a dependency or any other dependency (even for Postgres)


	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-cache</artifactId>
		<version>3.1.5</version>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-data-redis</artifactId>
		<version>3.1.5</version>
	</dependency>


<br><br>
Go to 
 [Project](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/project.md).