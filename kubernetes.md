# TestMazzaTech

Kubernetes is an open source container orchestration platform designed to automate the deployment, scaling and management of containerized applications. It is widely used in modern microservices-based architectures, bringing several advantages to application and infrastructure management. Some advantages of using Kubernetes is:
Automated Container Management: it reduces the complexity of container management by allowing you to automate tasks such as scaling, load balancing and restarting containers in the event of failures
Scalability made easy: it automatically adjusts the number of container replicas based on demand, ensuring high availability
High Availability: it guarantees resilience by distributing containers across different nodes in the cluster and automatically restarting those that fail.

We  can create a YAML file for kubernetes using the following command:
“kubectl apply -f <filename.yaml>”

This command will create the deployment in the kubernetes cluster according to the specifications in the file. Next is an example of a YAML file to configure deployment:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
      - name: example-container
        image: example-image
        ports:
        - containerPort: 8080

The benefits of deployments are the Reollouts and Roolbacks tha facilitate the gradual deployment (Rolling out) of new versions of applications, as well rolling back to previous versions in the event problem. Also, it can identify deployment fail ain automatically provision a new Pod.






Go to 
 [Testing](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/tests.md)