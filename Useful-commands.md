Here is a list of useful Kubernetes commands that can help you manage and troubleshoot your cluster:

### Basic Commands
- **List nodes:**
  ```bash
  kubectl get nodes
  ```
- **Get detailed information about a node:**
  ```bash
  kubectl describe node <node-name>
  ```

### Pod Management
- **List all pods in the default namespace:**
  ```bash
  kubectl get pods
  ```
- **List all pods in a specific namespace:**
  ```bash
  kubectl get pods -n <namespace>
  ```
- **Get detailed information about a pod:**
  ```bash
  kubectl describe pod <pod-name>
  ```
- **Get pod logs:**
  ```bash
  kubectl logs <pod-name>
  ```
- **Execute a command in a running pod:**
  ```bash
  kubectl exec -it <pod-name> -- <command>
  ```

### Deployment and StatefulSet Management
- **List all deployments:**
  ```bash
  kubectl get deployments
  ```
- **Get detailed information about a deployment:**
  ```bash
  kubectl describe deployment <deployment-name>
  ```
- **List all stateful sets:**
  ```bash
  kubectl get statefulsets
  ```
- **Get detailed information about a stateful set:**
  ```bash
  kubectl describe statefulset <statefulset-name>
  ```

### Service and Ingress Management
- **List all services:**
  ```bash
  kubectl get services
  ```
- **Get detailed information about a service:**
  ```bash
  kubectl describe service <service-name>
  ```
- **List all ingresses:**
  ```bash
  kubectl get ingresses
  ```
- **Get detailed information about an ingress:**
  ```bash
  kubectl describe ingress <ingress-name>
  ```

### Namespace Management
- **List all namespaces:**
  ```bash
  kubectl get namespaces
  ```
- **Create a new namespace:**
  ```bash
  kubectl create namespace <namespace-name>
  ```
- **Delete a namespace:**
  ```bash
  kubectl delete namespace <namespace-name>
  ```

### ConfigMap and Secret Management
- **List all config maps:**
  ```bash
  kubectl get configmaps
  ```
- **Get detailed information about a config map:**
  ```bash
  kubectl describe configmap <configmap-name>
  ```
- **List all secrets:**
  ```bash
  kubectl get secrets
  ```
- **Get detailed information about a secret:**
  ```bash
  kubectl describe secret <secret-name>
  ```

### Label and Annotation Management
- **Add a label to a node:**
  ```bash
  kubectl label node <node-name> <label-key>=<label-value>
  ```
- **Remove a label from a node:**
  ```bash
  kubectl label node <node-name> <label-key>-
  ```
- **Add an annotation to a pod:**
  ```bash
  kubectl annotate pod <pod-name> <annotation-key>=<annotation-value>
  ```
- **Remove an annotation from a pod:**
  ```bash
  kubectl annotate pod <pod-name> <annotation-key>-
  ```

### Resource Management
- **Scale a deployment:**
  ```bash
  kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>
  ```
- **Apply a configuration file:**
  ```bash
  kubectl apply -f <file.yaml>
  ```
- **Delete a resource:**
  ```bash
  kubectl delete -f <file.yaml>
  ```
- **View cluster resources in YAML/JSON:**
  ```bash
  kubectl get <resource-type> -o yaml
  kubectl get <resource-type> -o json
  ```

### Debugging and Troubleshooting
- **Get events in the cluster:**
  ```bash
  kubectl get events
  ```
- **Get events for a specific namespace:**
  ```bash
  kubectl get events -n <namespace>
  ```
- **View resource usage:**
  ```bash
  kubectl top nodes
  kubectl top pods
  ```

These commands cover a broad range of tasks and should help you manage and troubleshoot your Kubernetes cluster effectively.
