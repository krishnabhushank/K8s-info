To check if the existing nodes are labeled in your Kubernetes cluster, you can use the `kubectl get nodes` command along with the `-o json` or `-o yaml` option to inspect the labels on each node. Here are the steps:

1. **List All Nodes:**
   ```bash
   kubectl get nodes
   ```

   This will give you a list of all nodes in your cluster.

2. **Describe a Specific Node:**
   To see the labels of a specific node, you can describe it:
   ```bash
   kubectl describe node <node-name>
   ```

   This will show detailed information about the node, including its labels under the `Labels` section.

3. **Get Labels for All Nodes:**
   To see the labels for all nodes at once, you can use:
   ```bash
   kubectl get nodes --show-labels
   ```

   This command lists all nodes along with their labels.

4. **Inspect Node Labels in JSON or YAML:**
   To get more detailed information in JSON or YAML format, you can use:
   ```bash
   kubectl get nodes -o json | jq '.items[].metadata.labels'
   ```

   Or, for YAML format:
   ```bash
   kubectl get nodes -o yaml
   ```

   If you don't have `jq` installed, you can install it or use plain JSON output:
   ```bash
   kubectl get nodes -o json
   ```

By using these commands, you can inspect the labels on your nodes to see if they already have zone information or any other labels you might need. If the nodes are not labeled, you can add labels using the `kubectl label` command as described previously.
