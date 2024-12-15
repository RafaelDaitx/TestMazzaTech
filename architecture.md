# TestMazzaTech

In this API construction, the focus is to make it as easy as possible,  focusing on getting our API up and running faster.

First of all, we have to see how our microservice will be. We have the client-side, who going to do a request to our API, and this API will request a data (or send) to our Gateway (it will allows us, protect our API Address and the we can scale application in the best way)

<img src="/images/flow.png">
Made on Miro.com

That is the way the data will work through API. Our Dataflow, must follow the following process:

<img src="/images/dataflow.png">

In our flow, the request will check our application’s cache (this improves performance, if it is loaded). On the other hand, it will go to interact with the Kubernetes (which routes requests to the correct pods, do server balancing and service discovery), and go to the API (do the necessary logic), going to the database and coming back to our client, updating the existing cache. 

*Personal note: it was a little bit difficult to learn how the following code works and how to create it. I developed this code for the Dataflow. Made on https://www.plantuml.com/.

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



Go to
 [Techonologies](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/technologies.md) ,