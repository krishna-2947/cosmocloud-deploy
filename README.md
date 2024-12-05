# COSMOCLOUD-DEPLOY

This README explains the chart structure, deployment process, and verification steps.


# Project Summary: Full-Stack Application Deployment with Helm and Kubernetes.

This project involves the creation and deployment of a full-stack application using Kubernetes, Minikube, and Helm. The application consists of three main components:

Frontend---> A user-facing application.

Backend---> The business logic layer that communicates with the frontend and Redis.

Redis---> A caching database used by the backend to store data.

The application was developed and tested on a Ubuntu machine, where the following tools were utilized:

Docker---> To containerize the application components (frontend, backend, Redis) and run them as Kubernetes pods.

Minikube---> A local Kubernetes cluster was set up using Minikube to simulate a production-like environment for testing.

kubectl--- Used for managing and interacting with the Kubernetes cluster, including deploying resources and inspecting pods and services.

Helm---> Helm charts were used to define the Kubernetes resources for the frontend, backend, and Redis services. It simplifies the deployment process and ensures consistency across environments.

# The project’s primary goal was to:

Create a Helm chart that defines the necessary Kubernetes resources, such as deployments and services, for the frontend, backend, and Redis components.
Ensure proper communication between the frontend, backend, and Redis through environment variables (BACKEND_URL for the frontend and REDIS_URI for the backend).
Expose the frontend application externally using a NodePort service, while keeping the backend and Redis services internal using ClusterIP services.
Validate the deployment through Kubernetes tools like kubectl and ensure everything works as expected within the Minikube cluster.



This setup successfully deployed the full-stack application on a local Kubernetes cluster, with the frontend being accessible via the configured NodePort, and the backend and Redis services communicating seamlessly within the cluster.

The project demonstrates an understanding of containerization, Kubernetes deployment patterns, and Helm chart management, ensuring that the application can scale, be maintained, and be deployed consistently across different environments.









# Cosmocloud-deploy :


This repository contains a yaml files to deploy a full-stack application with:

Frontend ---> A user-facing application.

Backend ---> Handles business logic and interacts with Redis.

Redis ---> A caching database for backend operations.


# Helm Chart Structure

The directory structure of the Helm chart is as follows:

cosmocloud-deploy/

---> Chart.yaml         # Metadata about the Helm chart

---> values.yaml        # Default configuration values

# Kubernetes resource templates

---> backend-deployment.yaml

---> backend-service.yaml

---> frontend-deployment.yaml

---> frontend-service.yaml

---> redis-deployment.yaml

---> redis-service.yaml


# Chart Components :

Chart.yaml --->

Contains metadata like chart name, version, description, and dependencies.


values.yaml --->

Centralized configuration for customizing the deployment.
Includes values for replicas, image versions, environment variables, and port mappings.

templates --->

Contains the Kubernetes manifests (YAML templates) for deploying and exposing resources.

Here’s a brief explanation of each YAML files.

# backend-deployment.yaml ----->

Deploys the backend pod using the image shreybatra/sample-backend.

Configures the environment variable REDIS_URI to connect to Redis (redis-svc:6379).

Exposes the backend application on port 8000.

-----------------------

 # backend-service.yaml ------->

Creates a ClusterIP service to expose the backend internally within the cluster.

Maps the service's port 8000 to the backend pod's port 8000.

-----------------------

# frontend-deployment.yaml ------->

Deploys the frontend pod using the image shreybatra/sample-frontend.

Configures the environment variable BACKEND_URL to connect to the backend (backend-svc:8000).

Exposes the frontend application on port 5173.

------------------------

# frontend-service.yaml ------->

Creates a NodePort service to expose the frontend externally.

Maps the service's port 5173 to the frontend pod's port 5173, and makes it accessible via NodePort 31000.

----------------------

# redis-deployment.yaml ------->

Deploys a Redis pod using the redis image.

Exposes Redis for internal communication on port 6379.

-------------------

# redis-service.yaml ------>

Creates a ClusterIP service to expose Redis internally within the cluster.

Maps the service's port 6379 to the Redis pod's port 6379.








# Project Setup on Ubuntu Machine

For this project, I set up the entire infrastructure on my Ubuntu machine. The following tools were installed and used:

# Docker:

Docker was installed to run containerized applications and allow the creation of custom containers for the backend, frontend, and Redis services.

# Minikube:

Minikube was used to create a local Kubernetes cluster. It allowed me to deploy and test the full-stack application within a controlled environment.

# kubectl:

kubectl was installed to interact with the Kubernetes cluster, manage resources, and perform tasks like deploying the Helm chart, creating pods, services, and inspecting the application status.

This setup enabled me to simulate the deployment process and test the application's functionality locally before moving to a production environment.


# Run the following command to deploy the Helm chart:

helm install testapp . --atomic --timeout 30s


# Verify the Deployment

Once the deployment is complete, verify the resources:

kubectl get pods

kubectl get svc

kubectl get deploy

![Screenshot(41).png](https://github.com/krishna-2947/cosmocloud-deploy/blob/main/Screenshot%20(41).png)

And by using the Minikube IP we can access our frontend Appliation.


![Screenshot(40).png](https://github.com/krishna-2947/cosmocloud-deploy/blob/main/Screenshot%20(40).png)


Here is the Web Interface of our application :

![Screenshot(42).png](https://github.com/krishna-2947/cosmocloud-deploy/blob/main/Screenshot%20(42).png)




