# TestMazzaTech

Thinking about testing and deploying the application into production, I decided to use Docker for this step. Docker allows us to test our server and ensure everything is running correctly. We will upload a container of our application. First, we will create a Dockerfile with the following instructions:
FROM openjdk:17-jdk-slim
This image provides a minimal Java environment for running our application. You can also use other base images for different technologies, like Node.js (node:20-slim).
ARG JAR_FILE=cambio-service/target/*.jar
This defines a build-time variable to specify the path to the JAR file that will be included in the container.
RUN bash -c 'touch /app.jar'
This ensures the /app.jar file exists. It is not strictly necessary and can usually be omitted unless you have a specific reason for it.
COPY ${JAR_FILE} app.jar
This copies the JAR file from the build context into the container and names it app.jar.
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
This specifies the command that runs when the container starts. In this case, it starts the Java application using the JAR file.


We will save this Dockerfile in the root directory of the project (not as a YAML file). With the Dockerfile in place, we can build the image by running the following command:

“docker build -t name-of-image .””

This command creates an image with the name defined in the -t flag. The . at the end indicates the build context, which is the current directory.
To verify that the image was created successfully, you can run the next command (this command lists all the images available on your system):
“docker images”

To run the container, use the following command:
“docker run -p 3000:3000 --name my-container name-of-image”

-p 3000:3000: Maps port 3000 on the host to port 3000 inside the container.
--name my-container: Assigns a name to the container for easier management.
name-of-image: Refers to the image we just built.
We can access (in our own machine) accessing http://localhost:3000 to validate our application. 