# Architechture

This architecture aims to design a scalable, robust, and efficient microservice capable of handling high data volumes with low latency. Below, we describe the key components and their roles in ensuring performance and scalability

I'll describe some of the steps involved in creating our product and helping people with their problems. I'll describe some of the costs.

First of all, we have to see how our microservice will work. 

Looking to the image below, we have the client-side making a request to our API, and this API will request a data (or send) to our Gateway. The API Gateway acts as the entry point for client requests, handling authentication, rate-limiting, and routing traffic to the appropriate Kubernetes service.

<img src="/images/flow.png">
Made on Miro.com<br><br><br>



That is the way the data will work through API. Our Dataflow, must follow the following process:

<img src="/images/dataflow.png">

In our flow, the request will check our application’s cache (this improves performance, if it is loaded). On the other hand, it will go to interact with the Kubernetes (which routes requests to the correct pods, do server balancing and service discovery), and go to the API (do the necessary logic), going to the database and coming back to our client, updating the existing cache. 

* Kubernetes makes it easy to create replicas of services (pods), distributing the load automatically and efficiently between them. This ensures that the system can cope with sudden increases in traffic.

* Data in the cache is stored in memory, which drastically reduces access time compared to the database, especially for read operations. This is essential for achieving the response requirement of less than 500ms. Less access to the database means less CPU, memory and I/O consumption by the database server, reducing operating costs, a database optimized for fast queries (such as Redis for persistent caching) is a good option.

```yaml
@startuml
actor Client 
participant Gateway as "API Gateway"
participant Cache as "Cache System"
participant K8S as "Kubernetes"
participant API as "API Service"
database DB as "Database"

Client -> Gateway : HTTP Request
Gateway -> Cache : Check Cache
alt Cache Hit
    Cache --> Gateway : Cached Response
else Cache Miss
    Gateway -> K8S : Forward to Kubernetes Service
    K8S -> API : Route to API Pod
    API -> DB : Query/Save Data
    DB --> API : Return Data/Confirmation
    API -> Cache : Update Cache
    API --> Gateway : Response
end
Gateway --> Client : HTTP Response
@enduml
```
<br>


Client → Gateway

The client (browser, mobile application, etc.) sends an HTTP request (GET or POST) to the API Gateway.
The Gateway serves as a single gateway to the system, ensuring security (authentication and authorization) and allowing scalability by distributing requests among the available services.
Gateway → Kubernetes

The Gateway redirects the request to Kubernetes, which is responsible for locating the right microservice pod to handle the request.

Here, Kubernetes performs load balancing, ensuring that the request is distributed efficiently to the available microservice instances (pods).
Kubernetes → API

After determining the correct pod, the request is sent to the microservice (API).
 * The API Service performs validations and executes the necessary business logic.
 * Depending on the operation, the service may need to access the persistence layer (database) or consult the caching system.


API → Database (or Cache)
Cache Miss case (not found in the cache):
 * The service queries the database directly to retrieve or store information. After obtaining the data, the system updates the cache to handle future requests more quickly.

Cache Hit case (found in the cache):
 * The service directly retrieves the data from the cache, avoiding the need to query the database, which reduces response time and the load on the system.
Database (or Cache) → API → Gateway → Client

The processed data is returned from the API to the Gateway, which sends the final response to the client.
This flow ensures that the client receives the data or confirmation of the operation with the lowest possible latency.



Go to
 [Technologies](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/technologies.md).