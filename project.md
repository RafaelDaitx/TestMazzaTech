# Project

Our project is organized into specific folders, each designed to separate concerns and improve maintainability:

config: Contains general configuration files, such as enabling CORS, defining global settings, or setting up dependencies.
controller: Hosts the controller classes responsible for handling HTTP requests and defining our API endpoints. They delegate the business logic to service classes.
vos: This folder contains classes used for JSON mapping. These classes help customize how we process incoming or outgoing JSON in our API.
exceptions: Includes custom exception classes that provide meaningful and user-friendly error messages when exceptions occur. This improves the user experience and debugging process.
repository: Contains classes responsible for database interactions, such as CRUD operations or custom database queries. These classes are typically interfaces extending JPA repositories.
mapper: This folder contains mapper classes that translate entities from the database into application objects (DTOs) and vice-versa. This ensures a clear separation between the data layer and business logic.

<br>


<img src="/images/folders.png">
<br>
Its completely important to think about the future. Our database needs to be easier to upgrade at any moment. For this, we will use FlyWay for control our migrations and database versions in the easiest way (remembering that we are shaping our API with specific tools, we can find similar tools for other languages).

With Flyway, we have a specific folder which automatically controls the versioning of our database. Below, an example how to create a file name to use Flyway.

<img src="/images/flyway.png">
<br><br>



Go to 
 [Containers](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/containers.md).