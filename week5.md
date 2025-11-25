# Kubernetes 

## 1. Kubernetes Overview

- **Kubernetes (K8s)**  
  Open-source platform for automating container deployment, scaling, and management.

- **Primary Goals**
  - High availability
  - Scalability
  - Self-healing
  - Efficient resource utilization


## 2. Core Kubernetes Concepts

### Pod

- **Pod**  
  Smallest deployable unit in Kubernetes.

- **Pod Contains**
  - One or more containers
  - Shared network (IP, ports)
  - Shared storage (volumes)

- **Scheduling**
  - Control Plane decides *where*
  - Worker Node runs the pod

#### Useful Commands
```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl delete pod <pod-name>
```

## 3. Kubernetes Architecture

Kubernetes has two main planes:
- Control Plane
- Data Plane (Worker Nodes)

