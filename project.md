# TestMazzaTech

We starting creating our project and organizing it into files, for example:
config: general settings of our API (like for CORS)
Controller: our controller classes that will guard our endpoints
vos: folder to have our Json Mapping classes, so we can customize them as we want our received Json.
exceptions: we customize our exceptions according to the code that the server return to us, so we leave friendly message for the user seeing
repository: we make the database connection class, where we can create customized queries for the database.
mapper: folder where we organize the classes to perform the necessary between the database layer (our repository) and our service


<img src="/images/folders.png">

Its completely important to think about the future. Our database needs to be easier to upgrade at any moment. For this, we will use FlyWay for control our migrations and database versions in the easiest way (remembering that we are shaping our API with specific tools, we can find similar tools for other languages). With Flyway, we have a specific folder which automatically controls the versioning of our database. Below, an example how to create a file name to use Flyway.

<img src="/images/flyway.png">