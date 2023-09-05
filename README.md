# Deploying a Flask Application on Kubernetes 

This guide explains how to deploy a Flask application on aKubernetes cluster .

## Build the Docker Image

Build a Docker image for your Flask application. Replace `flask_img` with the desired image name.

```bash
docker build -t flask_img .
```

Push Image to Docker Hub (Optional) or Load Image to Minikube

Option 1: Push Image to Docker Hub (Replace with your Docker Hub repository and tag)

```bash
docker tag flask_img:latest your-docker-hub-username/flask_img:latest
docker push your-docker-hub-username/flask_img:latest
```

Option 2: Load Image to Minikube
Load your Docker image into the Minikube cluster.

```bash
minikube image load flask_img:latest
```

## Deploy to Kubernetes

Apply the Kubernetes deployment and service configurations.

```bash
kubectl apply -f deployment.yaml
kubectl apply -f k8s_cluster.yaml
```

## Access the Application Locally

To access your Flask application locally, use the following command to open it in your default web browser.

```bash
minikube service flask-app-service
```

## Useful Kubernetes Commands

Here are some useful Kubernetes commands for monitoring your cluster and applications:

- List all Pods:
``` bash
  kubectl get pods
```

- List all Deployments:
``` bash
  kubectl get deployments
```

- View Pod Logs:
``` bash
  kubectl logs <podname>
```

- Describe a Pod (useful for troubleshooting):
``` bash
  kubectl describe pod <podname>
```

- List all Services:
``` bash
  kubectl get services
```

- List all ConfigMaps:
``` bash
  kubectl get configmaps
```

- List all Secrets:
``` bash
  kubectl get secrets
```

- View Cluster Info:
``` bash
  kubectl cluster-info
```

- Get Nodes:
``` bash
 kubectl get nodes
```

## Useful Port forwarding commands

### Port forwarding for pods
``` bash
kubectl port-forward <pod-name> <local-port>:<pod-port>
kubectl port-forward my-pod 8080:80
```
Now, any traffic sent to http://localhost:8080 on your local machine will be forwarded to port 80 of the my-pod pod in the cluster.

### Port forwarding for deployments
``` bash
kubectl port-forward deployment/<deployment-name> <local-port>:<pod-port>
kubectl port-forward deployment/my-deployment 8080:80
```