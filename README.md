# cosmocloud-deploy

This README explains the chart structure, deployment process, and verification steps.

Cosmocloud Helm Chart :


This repository contains a Helm chart (cosmocloud-deploy) to deploy a full-stack application with:

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

Chart.yaml:

Contains metadata like chart name, version, description, and dependencies.


values.yaml:

Centralized configuration for customizing the deployment.
Includes values for replicas, image versions, environment variables, and port mappings.

templates/:

Contains the Kubernetes manifests (YAML templates) for deploying and exposing resources.

Here’s a brief explanation of each YAML files.

backend-deployment.yaml ----->

Deploys the backend pod using the image shreybatra/sample-backend.
Configures the environment variable REDIS_URI to connect to Redis (redis-svc:6379).
Exposes the backend application on port 8000.

-----------------------

backend-service.yaml ------->

Creates a ClusterIP service to expose the backend internally within the cluster.
Maps the service's port 8000 to the backend pod's port 8000.

-----------------------

frontend-deployment.yaml ------->

Deploys the frontend pod using the image shreybatra/sample-frontend.
Configures the environment variable BACKEND_URL to connect to the backend (backend-svc:8000).
Exposes the frontend application on port 5173.

------------------------

frontend-service.yaml ------->

Creates a NodePort service to expose the frontend externally.
Maps the service's port 5173 to the frontend pod's port 5173, and makes it accessible via NodePort 31000.

----------------------

redis-deployment.yaml ------->

Deploys a Redis pod using the redis image.
Exposes Redis for internal communication on port 6379.

-------------------

redis-service.yaml ------>

Creates a ClusterIP service to expose Redis internally within the cluster.
Maps the service's port 6379 to the Redis pod's port 6379.

# Verify the Deployment

# Run the following command to deploy the Helm chart:

helm install testapp . --atomic --timeout 30s

# Verify the Deployment

Once the deployment is complete, verify the resources:

kubectl get pods
kubectl get svc
kubectl get deploy



