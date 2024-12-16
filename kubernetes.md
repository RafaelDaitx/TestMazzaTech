# Kubernetes

Kubernetes is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications. It is widely used in modern microservices-based architectures, offering several advantages for application and infrastructure management. Some of the advantages of using Kubernetes are:

* Automated Container Management: Kubernetes simplifies container management by automating tasks such as scaling, load balancing, and restarting containers in case of failure.
* Scalability: It automatically adjusts the number of container replicas based on demand, ensuring high availability and efficient resource usage.
* High Availability: Kubernetes guarantees resilience by distributing containers across different nodes in the cluster and automatically restarting any containers that fail.

We  can create a YAML file for kubernetes using the following command:
“kubectl apply -f <filename.yaml>”

This command will create the deployment in the kubernetes cluster according to the specifications in the file. Next is an example of a YAML file to configure deployment:

```yaml
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

```

Benefits of Deployments

* Rollouts and Rollbacks: Kubernetes allows you to perform rolling updates, which gradually deploy new versions of your application. If an issue arises, you can roll back to a previous stable version of the application.
* Pod Management: Kubernetes automatically detects failing Pods and will create new ones to replace them, ensuring that your application is always running smoothly.



<br><br>


Go to 
 [Testing](https://github.com/RafaelDaitx/TestMazzaTech/blob/main/tests.md).