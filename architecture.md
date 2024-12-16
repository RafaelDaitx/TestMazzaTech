# Architechture

In this API construction, the focus is to make it as easy as possible,  focusing on getting our API up and running faster.

I'll describe some of the steps involved in creating our product and helping people with their problems. I'll describe some of the costs.

First of all, we have to see how our microservice will work. 

Looking to the image below, we have the client-side making a request to our API, and this API will request a data (or send) to our Gateway (it will allows us, protect our API Address and the we can scale application in the best way)

<img src="/images/flow.png">
Made on Miro.com



That is the way the data will work through API. Our Dataflow, must follow the following process:

<img src="/images/dataflow.png">

In our flow, the request will check our application’s cache (this improves performance, if it is loaded). On the other hand, it will go to interact with the Kubernetes (which routes requests to the correct pods, do server balancing and service discovery), and go to the API (do the necessary logic), going to the database and coming back to our client, updating the existing cache. 

*<b>Personal note:</b> it was a little bit difficult to learn how the following code works and how to create it. I developed this code for the Dataflow. Made on https://www.plantuml.com/.

@startuml
actor Client </br>
participant Gateway as "API Gateway"</br>
participant Cache as "Cache System"</br>
participant K8S as "Kubernetes"</br>
participant API as "API Service"</br>
database DB as "Database"</br>

Client -> Gateway : HTTP Request</br>
Gateway -> Cache : Check Cache</br>
alt Cache Hit</br>
    Cache --> Gateway : Cached Response</br>
else Cache Miss</br>
    Gateway -> K8S : Forward to Kubernetes Service</br>
    K8S -> API : Route to API Pod</br>
    API -> DB : Query/Save Data</br>
    DB --> API : Return Data/Confirmation</br>
    API -> Cache : Update Cache</br>
    API --> Gateway : Response</br>
end</br>
Gateway --> Client : HTTP Response</br>
@enduml</br>



Go to
 [Techonologies](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/technologies.md).