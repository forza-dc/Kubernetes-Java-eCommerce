![ShopFront](<Java-Docker ShopFront.png>)

Java Application Deployment with Docker and Kubernetes
This guide provides step-by-step instructions for deploying a Java application with Docker and Kubernetes. The application consists of three separate components:

Shopfront: Frontend of the page.
ProductCatalogue: Database component.
StockManager: Inventory control component.
Each component is Dockerized and includes a pom.xml file for Maven to build it.

Prerequisites
Docker: Install Docker on your local machine. You can download it from Docker's official website.

Minikube: Install Minikube to set up a local Kubernetes cluster. Follow the instructions on the Minikube GitHub repository.

kubectl: Install kubectl to interact with the Kubernetes cluster. You can find installation instructions here.

Dockerizing Components
Each component (Shopfront, ProductCatalogue, StockManager) should have its Dockerfile. Below is a simplified example structure:


shopfront/
|-- Dockerfile
|-- src/
    |-- main/
        |-- java/
            |-- com/
                |-- shopfront/
                    |-- ShopfrontApp.java
                    |-- // other source files
        |-- resources/
            |-- // resources, HTML, etc.
        |-- pom.xml

productcatalogue/
|-- Dockerfile
|-- src/
    |-- main/
        |-- java/
            |-- com/
                |-- productcatalogue/
                    |-- ProductCatalogueApp.java
                    |-- // other source files
        |-- resources/
            |-- // resources, database scripts, etc.
        |-- pom.xml

stockmanager/
|-- Dockerfile
|-- src/
    |-- main/
        |-- java/
            |-- com/
                |-- stockmanager/
                    |-- StockManagerApp.java
                    |-- // other source files
        |-- resources/
            |-- // resources, configuration files, etc.
        |-- pom.xml
Building Docker Images
Build Shopfront Image:


cd shopfront
docker build -t shopfront:latest .
Build ProductCatalogue Image:


cd productcatalogue
docker build -t productcatalogue:latest .
Build StockManager Image:


cd stockmanager
docker build -t stockmanager:latest .
Running on Minikube
Start Minikube:


minikube start
Configure Docker Environment:


eval $(minikube docker-env)
Apply Kubernetes Configurations:


kubectl apply -f kubernetes/shopfront-deployment.yaml
kubectl apply -f kubernetes/productcatalogue-deployment.yaml
kubectl apply -f kubernetes/stockmanager-deployment.yaml
Expose Services:


kubectl expose deployment shopfront --type=NodePort
kubectl expose deployment productcatalogue --type=NodePort
kubectl expose deployment stockmanager --type=NodePort
Get URLs:


minikube service shopfront --url
The above command will provide a URL that you can use to access the main page of the application.

![Kubernetes Cluster](<Kubernetes Terminal.jpeg>)

Cleanup
To stop and delete the Minikube cluster, run:


minikube stop
minikube delete
This concludes the deployment process. You can now access the Java application through the provided URL from the local Minikube Kubernetes cluster.