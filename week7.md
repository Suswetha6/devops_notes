## 1. Scaling Mechanisms
- **Horizontal Pod Autoscaler (HPA)** : 
  Scales pods based on CPU / memory
  ```bash
  kubectl autoscale deployment nginx --min=2 --max=10 --cpu-percent=50
  ```
- **Vertical Pod Autoscaler (VPA)** : 
Adjusts CPU & memory requests automatically

- **Cluster Autoscaler** :
Scales worker nodes based on pending pods

## 2. Pod Lifecycle 

- Pending → Running → Succeeded / Failed
- Deleting pod:
  - Containers terminated
  - Resources released
  - Controller recreates pod if required
  ```bash
  kubectl delete pod <pod-name>
  ```

## 3. Certificates & Security

Kubernetes uses certificates for:

- API authentication
- Node communication
- Supports automatic certificate rotation

## 4. Useful Debugging Commands
```bash
kubectl get all

kubectl describe node <node-name>

kubectl logs <pod-name>

kubectl exec -it <pod-name> -- /bin/sh
