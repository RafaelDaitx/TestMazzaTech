# Containers

To test and deploy our application, we will use Docker. Docker simplifies the process of packaging and running our application in a consistent environment. Below, we outline the steps to create and use a Docker container for our project.
 
First, we will create a Dockerfile with the following instructions:

```java
FROM openjdk:17-jdk-slim
ARG JAR_FILE=cambio-service/target.jar
RUN bash -c 'touch /app.jar'
COPY ${JAR_FILE} app.jar 
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```
Explanation:
* FROM openjdk:17-jdk-slim: Specifies a minimal base image with Java 17.
* ARG JAR_FILE: Allows the JAR file's path to be passed during the build process.
* COPY: Copies the application JAR file into the container as app.jar.
* ENTRYPOINT: Defines the command to run the application when the container starts.

This specifies the command that runs when the container starts. In this case, it starts the Java application using the JAR file. This image provides a minimal Java environment for running our application. You can also use other base images for different technologies, like Node.js (node:20-slim).

We will save this Dockerfile in the root directory of the project (not as a YAML file). With the Dockerfile in place, we can build the image by running the following command:

“docker build -t name-of-image .””

This command creates an image with the name defined in the -t flag. The . at the end indicates the build context, which is the current directory.
To verify that the image was created successfully, you can run the next command (this command lists all the images available on your system):
“docker images”

To run the container, use the following command:
“docker run -p 3000:3000 --name my-container name-of-image”

</br>
-p 3000:3000: Maps port 8080 on the host to port 3000 inside the container. Adjust the port as per your application's configuration.
--name my-app-container: Assigns a custom name to the container for easier management.
my-app-image: Refers to the image we built earlier.
</br></br>

Notes and Alternatives

* Other Base Images: You can use alternative base images for different technologies, such as node:20-slim for Node.js applications.
* Cloud Deployment: For production deployment, consider using container orchestration tools like Kubernetes for scalability and fault tolerance.

We can access (in our own machine) accessing http://localhost:3000 to validate our application. </br>
Go to 
 [Cloud](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/cloud.md).