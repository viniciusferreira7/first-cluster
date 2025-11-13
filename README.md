# First Cluster - Kubernetes Study Project

> **Work in Progress** - This is a learning project from the Rocketseat DevOps curriculum

## Overview

This repository contains configuration for creating a local Kubernetes cluster using [kind](https://kind.sigs.k8s.io/) (Kubernetes in Docker). It's designed for learning Kubernetes concepts and practicing cluster operations in a local development environment.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) - Must be running before creating the cluster
- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation) - Kubernetes in Docker
- [kubectl](https://kubernetes.io/docs/tasks/tools/) - Kubernetes command-line tool

## Cluster Configuration

The cluster is defined in [kind.yaml](kind.yaml) with the following topology:

- **1 Control Plane Node** - Manages the Kubernetes cluster
- **1 Worker Node** - Runs application workloads

## Project Structure

```
first-cluster/
├── kind.yaml          # Kubernetes cluster configuration
├── pod.yaml           # Nginx pod declarative configuration
├── deployment.yaml    # Nginx deployment with 5 replicas
└── README.md          # This file
```

## Pods & Workloads

### Nginx Pod

A sample Nginx pod is defined in [pod.yaml](pod.yaml) with the following specifications:

- **Image**: `nginx:alpine3.22` - Lightweight Nginx image based on Alpine Linux
- **Port**: 80 (HTTP)
- **Resource Requests**:
  - CPU: 100m
  - Memory: 64Mi
- **Resource Limits**:
  - CPU: 200m
  - Memory: 128Mi

This pod demonstrates resource management best practices for Kubernetes workloads.

### Nginx Deployment

A Kubernetes Deployment for Nginx is defined in [deployment.yaml](deployment.yaml) with the following specifications:

- **Replicas**: 5 - Multiple pod replicas for high availability
- **Image**: `nginx:1.29.3-alpine3.22-slim` - Lightweight Nginx image
- **Port**: 80 (HTTP)
- **Resource Requests**:
  - CPU: 100m
  - Memory: 64Mi
- **Resource Limits**:
  - CPU: 200m
  - Memory: 128Mi

The Deployment manages multiple Nginx pod replicas, providing load balancing and automatic recovery if pods fail.

## Getting Started

### 1. Create the Cluster

```bash
kind create cluster --config kind.yaml --name first-cluster
```

### 2. Verify the Cluster

Check that the cluster is running:

```bash
kubectl cluster-info --context kind-first-cluster
kubectl get nodes
```

You should see two nodes: one control-plane and one worker.

### 3. Deploy the Nginx Pod

Deploy the sample Nginx pod to the cluster:

```bash
kubectl apply -f pod.yaml
```

Verify the pod is running:

```bash
kubectl get pods
kubectl describe pod nginx
```

### 4. Deploy the Nginx Deployment

Deploy the Nginx Deployment with 5 replicas:

```bash
kubectl apply -f deployment.yaml
```

Verify the deployment is running:

```bash
kubectl get deployments
kubectl get pods
kubectl describe deployment nginx
```

### 5. Access the Nginx Pods

Forward the deployment's port to your local machine:

```bash
kubectl port-forward deployment/nginx 8080:80
```

Then access Nginx at `http://localhost:8080` in your browser.

### 6. Start Experimenting!

Explore more Kubernetes concepts by creating additional pods, services, and deployments.

## Useful Commands

### Cluster Management

```bash
# List all kind clusters
kind get clusters

# Delete the cluster
kind delete cluster --name first-cluster

# Export cluster logs for troubleshooting
kind export logs --name first-cluster
```

### Kubernetes Operations

```bash
# View all resources
kubectl get all --all-namespaces

# View pods
kubectl get pods

# View services
kubectl get services

# Describe a resource
kubectl describe node <node-name>
```

### Pod Management

```bash
# Apply/Deploy the Nginx pod
kubectl apply -f pod.yaml

# View pod details
kubectl describe pod nginx

# View pod logs
kubectl logs nginx

# Delete the pod
kubectl delete pod nginx

# Forward pod port
kubectl port-forward pod/nginx 8080:80
```

### Deployment Management

```bash
# Apply/Deploy the Nginx deployment
kubectl apply -f deployment.yaml

# View deployment details
kubectl describe deployment nginx

# View deployment replicas
kubectl get deployment nginx

# Scale the deployment
kubectl scale deployment nginx --replicas=3

# Delete the deployment
kubectl delete deployment nginx

# Forward deployment port
kubectl port-forward deployment/nginx 8080:80

# View deployment logs
kubectl logs -l app=nginx --tail=100
```

## Learning Resources

- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [kind Documentation](https://kind.sigs.k8s.io/)

## Project Status

🚧 This is a study project and is currently under development as part of learning DevOps practices and Kubernetes fundamentals.
