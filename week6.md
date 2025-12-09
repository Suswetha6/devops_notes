## 1. Control Plane Components
- **API Server** :
  - Entry point to the cluster
  - Handles REST requests from users and components
  ```bash 
  kubectl cluster-info
  ```
- **etcd** :
  - Distributed key-value store
  - Stores:
    - Cluster state
    - Configuration
    - Secrets (encrypted)

- **Controller Manager** : 

  - Ensures desired state matches actual state
  - Examples:
    - ReplicaSet controller
    - Node controller

- **Scheduler**
  - Decides which node runs a pod
  - Considers:
    - CPU / memory
    - Node taints & tolerations
    - Affinity rules

## 2.Data Plane (Worker Node) Components

- **Kubelet**
  - Agent running on each node
  - Ensures pods are running as defined

- **Container Runtime (CRI)**
  - Pulls images & runs containers
  - Examples:
    - containerd
    - CRI-O
    - Docker (legacy)

- **Kube-Proxy**
  - Manages networking rules
  - Enables Service → Pod communication

## 3. **Kubernetes Objects**
- **Deployment**
  - Manages ReplicaSets and Pods
  - Supports rolling updates
  ```bash 
  kubectl create deployment nginx --image=nginx
  kubectl scale deployment nginx --replicas=3
  ```
- **ReplicaSet**
Ensures specified number of pods are running

- **Service**
  - Stable network endpoint for pods
  - Types:
    - ClusterIP (default)
    - NodePort
    - LoadBalancer
  ```bash
  kubectl expose deployment nginx --type=NodePort --port=80
  ```
- **Namespace**
  - Logical isolation within cluster
  ```bash
  kubectl get namespaces
  kubectl create namespace dev
  ```

## 4. Key Kubernetes Features
- **Automatic Bin Packing** : 
   Schedules pods based on resource requests

- **Self-Healing** :
  - Restarts failed containers
  - Replaces failed pods
  - Reschedules pods from failed nodes

- **Horizontal Scaling** :

  - Scale pods based on metrics : 
    ``` bash
    kubectl scale deployment nginx --replicas=5
    ```

- **Service Discovery & Load Balancing** : 
  - DNS-based service discovery
  - Load balances traffic across pods

- **Automated Rollouts & Rollbacks** : 
  - Zero-downtime deployments
  ```bash
  kubectl rollout status deployment nginx
  kubectl rollout undo deployment nginx
  ```
- **Secrets & ConfigMaps** : 
Externalize configuration
```bash
kubectl create configmap app-config --from-literal=env=prod
kubectl create secret generic db-secret --from-literal=password=123
```

- **Batch & Cron Jobs** : 

Run one-time or scheduled tasks
```bash
kubectl get jobs
kubectl get cronjobs
```

