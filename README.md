
# MERN Application Deployment on Azure AKS

## Prerequisites

- An Azure account
- Azure CLI installed
- Kubectl installed
- Docker installed
- Git installed

## Step 1: Clone the Repository

Clone the application repository from GitHub.

```bash
git clone https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices
cd SampleMERNwithMicroservices
```

## Step 2: Build Docker Images

Navigate to each service directory (hello-service, profile-service, frontend) and build the Docker images.

```bash
cd hello-service
docker build -t your-dockerhub-username/mernhelloservice:latest .
docker push your-dockerhub-username/mernhelloservice:latest

cd ../profile-service
docker build -t your-dockerhub-username/mernprofileservice:latest .
docker push your-dockerhub-username/mernprofileservice:latest

cd ../frontend
docker build -t your-dockerhub-username/mernfrontend:latest .
docker push your-dockerhub-username/mernfrontend:latest
```

## Step 3: Create an Azure Kubernetes Service (AKS) Cluster

Create an AKS cluster using the Azure CLI.

```bash
az login
az group create --name myResourceGroup --location eastus
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

## Step 4: Deploy the Application on AKS

Ensure you have your Kubernetes manifests ready (provided in the KubernetesManifest.yaml file).

Apply the Kubernetes manifests to deploy the application.

```bash
kubectl apply -f KubernetesManifest.yaml
```

## Step 5: Configure Ingress

Create an Ingress resource to manage access to your services.

```bash
kubectl apply -f KubernetesIngress.yaml
```

## Step 6: Verify the Deployment

Check the status of your pods and services to ensure everything is running smoothly.

```bash
kubectl get pods
kubectl get services
kubectl get ingress
```

## Step 7: Access the Application

Once the services are up and running, access the application IP through the browser



