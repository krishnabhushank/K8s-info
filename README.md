# K8s-info
Information related to k8s

In Kubernetes, distributing StatefulSet pods across specific zones is not natively supported. StatefulSets are designed for applications requiring stable, unique network identifiers and stable, persistent storage, but they do not inherently support zonal distribution.

However, you can achieve zone-based distribution using a combination of node affinity, node selectors, and pod anti-affinity rules. Here's a high-level approach:

1. **Label Nodes by Zone:**
   Label your nodes to indicate their zones. For example:
   ```bash
   kubectl label nodes <node-name-1> topology.kubernetes.io/zone=zone-a
   kubectl label nodes <node-name-2> topology.kubernetes.io/zone=zone-b
   kubectl label nodes <node-name-3> topology.kubernetes.io/zone=zone-b
   ```

2. **Use Pod Affinity and Anti-Affinity:**
   Define pod affinity and anti-affinity rules in your StatefulSet manifest to control the distribution of pods. Here's an example of how to define these rules:

   ```yaml
   apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: example-statefulset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example
  template:
    metadata:
      labels:
        app: example
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            preference:
              matchExpressions:
              - key: topology.kubernetes.io/zone
                operator: In
                values:
                - zone-a
          - weight: 50
            preference:
              matchExpressions:
              - key: topology.kubernetes.io/zone
                operator: In
                values:
                - zone-b
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - example
            topologyKey: "topology.kubernetes.io/zone"
      containers:
      - name: example
        image: your-image
   
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: example-statefulset
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: example
     template:
       metadata:
         labels:
           app: example
       spec:
         affinity:
           nodeAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
               nodeSelectorTerms:
               - matchExpressions:
                 - key: topology.kubernetes.io/zone
                   operator: In
                   values:
                   - zone-a
           podAntiAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
             - labelSelector:
                 matchExpressions:
                 - key: app
                   operator: In
                   values:
                   - example
               topologyKey: "topology.kubernetes.io/zone"
         containers:
         - name: example
           image: your-image
   ```

In this example:

- The `nodeAffinity` rule ensures that at least one pod is scheduled in `zone-a`.
- The `podAntiAffinity` rule tries to spread the pods across different zones by ensuring that no two pods with the same label are scheduled in the same zone.

While this configuration does not strictly guarantee 1 pod in `zone-a` and 2 pods in `zone-b`, it helps to guide the scheduler towards the desired distribution. Kubernetes may still override these preferences based on overall cluster resource availability and constraints.
