# kubectl Overview (by Devstral-small)

## Basic Commands

1. **kubectl get**
   - Retrieves information about resources.

   ```sh
   # Get all pods in the current namespace
   kubectl get pods

   # Get a specific pod
   kubectl get pod my-pod

   # Get all deployments
   kubectl get deployments

   # Get all nodes
   kubectl get nodes

   # Get resources with more details (including resource usage)
   kubectl get pods -o wide
   ```

2. **kubectl describe**
   - Shows detailed information about a specific resource.

   ```sh
   # Describe a pod to get detailed info
   kubectl describe pod my-pod

   # Describe a deployment
   kubectl describe deployment my-deployment
   ```

3. **kubectl apply**
   - Applies configurations from files or stdin.

   ```sh
   # Apply a configuration from a file
   kubectl apply -f my-deployment.yaml

   # Apply multiple config files at once
   kubectl apply -f ./config-files/
   ```

4. **kubectl create**
   - Creates resources from files, stdin, or pre-defined templates.

   ```sh
   # Create a pod from a file
   kubectl create -f my-pod.yaml

   # Create a deployment with command line args (not commonly used)
   kubectl create deployment my-deployment --image=nginx
   ```

## Managing Pods and Deployments

5. **kubectl delete**
   - Deletes resources.

   ```sh
   # Delete a pod
   kubectl delete pod my-pod

   # Delete multiple pods at once
   kubectl delete pod pod1 pod2

   # Delete all pods matching a label selector
   kubectl delete pods -l app=my-app

   # Delete all resources in a namespace (dangerous!)
   kubectl delete all --all -n my-namespace
   ```

6. **kubectl logs**
   - Shows logs for a pod or container.

   ```sh
   # Get logs from a specific pod
   kubectl logs my-pod

   # Get logs with timestamps
   kubectl logs my-pod --timestamps

   # Stream logs (like tail -f)
   kubectl logs -f my-pod
   ```

7. **kubectl exec**
   - Executes commands in a container.

   ```sh
   # Run bash inside a pod's container
   kubectl exec -it my-pod -- /bin/bash

   # Execute a command without interactive terminal (-i and -t flags omitted)
   kubectl exec my-pod -- ls /app
   ```

8. **kubectl scale**
   - Scales the number of pods in a deployment.

   ```sh
   # Scale a deployment to 5 replicas
   kubectl scale deployment my-deployment --replicas=5

   # Scale using short form
   kubectl scale deploy my-deployment --replicas=10
   ```

## Configuring and Managing Namespace

9. **kubectl config**
   - Modifies kubeconfig settings.

   ```sh
   # View the current context (cluster/namespace/user)
   kubectl config view

   # Switch to a different cluster context
   kubectl config use-context my-cluster

   # Set default namespace in your kubeconfig
   kubectl config set-context --current --namespace=my-namespace
   ```

10. **kubectl namespace**
    - Manages namespaces.

    ```sh
    # Create a new namespace
    kubectl create namespace my-namespace

    # Delete an existing namespace
    kubectl delete namespace my-namespace

    # List all namespaces
    kubectl get namespaces
    ```

## Advanced Commands

11. **kubectl rollout**
    - Manages rolling updates and rollbacks.

    ```sh
    # Check status of the last rollout
    kubectl rollout status deployment my-deployment

    # Rollback to previous revision
    kubectl rollout undo deployment my-deployment

    # Rollback to a specific revision
    kubectl rollout undo deployment my-deployment --to-revision=2
    ```

12. **kubectl cordon/uncordon**
    - Marks nodes as unschedulable/schedulable.

    ```sh
    # Mark node as unschedulable (maintenance mode)
    kubectl cordon my-node

    # Mark node as schedulable again after maintenance
    kubectl uncordon my-node
    ```

13. **kubectl drain**
    - Safely evicts pods from a node.

    ```sh
    # Evict all pods to prepare for maintenance
    kubectl drain my-node --ignore-daemonsets

    # Drain with more specific options (e.g., timeout)
    kubectl drain my-node --ignore-daemonsets --timeout=120s
    ```

These commands should cover most of the common operations you'll need to perform when managing Kubernetes clusters.
