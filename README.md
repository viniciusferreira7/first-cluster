# First Cluster - Kubernetes Study Project

> **Work in Progress** - This is a learning project from the Rocketseat DevOps curriculum

## Overview

This repository contains configuration for creating a local Kubernetes cluster using [kind](https://kind.sigs.k8s.io/) (Kubernetes in Docker). It's designed for learning Kubernetes concepts and practicing cluster operations in a local development environment.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) - Must be running before creating the cluster
- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation) - Kubernetes in Docker
- [kubectl](https://kubernetes.io/docs/tasks/tools/) - Kubernetes command-line tool

## Cluster Configuration

The cluster is defined in `kind.yaml` with the following topology:

- **1 Control Plane Node** - Manages the Kubernetes cluster
- **1 Worker Node** - Runs application workloads

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

### 3. Start Experimenting!

Deploy a sample application, create pods, services, and explore Kubernetes concepts.

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

## Learning Resources

- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [kind Documentation](https://kind.sigs.k8s.io/)

## Notes

⚠️ **Known Issue**: There's a typo in the current `kind.yaml` file - `control-plan` should be `control-plane`. This may need to be corrected for the cluster to work properly.

## Project Status

🚧 This is a study project and is currently under development as part of learning DevOps practices and Kubernetes fundamentals.
