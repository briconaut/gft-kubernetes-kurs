---
revision: 1
path: ".claude/TOPICS-ORIGINAL.md"
title: "Workshop Topics (Analysis)"
abstract: "Full analysis output: every topic/subtopic found in Original/, split into Topics and Exercises, filtered against VISION.md's content guardrails"
state: in progress
lang: en
numbersections: false
finished_sections: [ ]
vision_revision: 1
history:
  - "v1: initial build from Original/, filtered against VISION.md rev 1"
---

# Topics

## Local Kubernetes Cluster Setup

### Installing Required Software

- Git Bash
- Docker Desktop

## Introduction to Kubernetes & Container Orchestration

### Overview

Kubernetes is an open-source **container orchestration platform** that automates the deployment, scaling, and management of containerized applications. Originally developed by Google and open-sourced in 2014.

It abstracts away the complexity of managing individual containers and allows developers to focus on building and deploying their applications.

Some key benefits of using Kubernetes:

- **Container orchestration**: Automates the distribution and scheduling of containers across a cluster.
- **Scalability and self-healing**: Simplifies horizontal scaling (replicating containers) and vertical scaling (adjusting resource allocation) all with self-healing capabilities.
- **High availability**: Ensures containers (and thus your services) remain operational even if some nodes fail.
- **Portability**: Abstracts the underlying infrastructure, making it straightforward to run both on-premises and on different cloud providers.
- **Efficient resource utilization**: Resizes containers based on resource usage, optimizing resource allocation and reducing costs.

### What Are Containers

## Kubernetes Architecture

Kubernetes clusters are groups of nodes, which are individual machines that run the Kubernetes software. A Kubernetes cluster consists logically of two components:

- **Control Plane** is responsible for coordinating all activities within the cluster
- **(Worker) Node(s)** handle running and managing containers

### Infrastructure

- Cluster
- Nodes
- Networking
- Data storage

### Control Plane

The control plane is the set of components that manage the overall state of the cluster. It includes the following components:

- **API Server**: The Kubernetes API server is the front-end for the control plane, exposing the Kubernetes API to users and other components. This component acts as the central management point for all Kubernetes resources. It receives requests from users and other components and then enforces policies to manage the cluster.
- **Controller Manager**: The controller manager manages the core control loops in Kubernetes, ensuring the desired state of the cluster is maintained by constantly monitoring and reconciling changes made to objects within the cluster.
- **Scheduler**: The scheduler is responsible for assigning pods to available nodes based on resource requirements and other constraints.
- **etcd** is a distributed key-value store that serves as the primary datastore for Kubernetes. It stores all cluster data and ensures data consistency and availability.

### Worker Nodes

Worker Nodes are the worker machines that run containerized applications. Each node runs the container runtime (e.g., Docker or containerd) and the Kubernetes agent called kubelet, which communicates with the control plane.

- **kubelet**: This agent runs on each node in the cluster and is responsible for managing containers, ensuring they are running according to their specified configurations.
- **Kube Proxy**: This component runs on each node and is responsible for routing network traffic to the correct container.

## Key Concepts

### Pods + Container (Runtime)

A pod encapsulates one or more containers, storage resources, and a unique network IP, allowing containers within the pod to share the same network namespace. It is the smallest unit of deployment in Kubernetes.

Each pod has its own unique IP address and can communicate with other pods in the same cluster through this address. This allows for efficient communication between different components of an application.

Pods can come in either single or multi-container pods and each comes with their own use case.

- **Single-container pods**: The most common type of pod, where a single container is running inside. This is useful for simple applications or microservices that only require one container.
- **Multi-container pods**: Multiple containers are co-located and run together. This can be beneficial for complex applications where different containers need to communicate with each other and share resources.

### Namespaces

Namespaces provide a way to logically partition resources within a single cluster. This allows for better organization and management of resources, as well as tighter security controls.

Namespaces can also be used to manage different environments, such as development, staging, and production. This ensures that resources are isolated and not affected by changes made in other environments.

### Ports & Gateways

### Ephemerality & Persistence

## `kubectl` – CLI for Kubernetes

### Overview

- cluster-info
- Namespaces
- Pods
- Logs
- Events

## Deployment

### Deployment Types

### Replicas

### Deployments Overview

Deployments provide declarative updates for pods and their associated replica sets. They enable rolling updates, canary deployments, and rollback functionality to manage the desired state of your applications.

## Services & kube-proxy

### kube-proxy

- Explain kube-proxy

### Labels and Selectors

- Labels and selectors

### Services Overview

Services provide a stable network address (stable DNS name, stable IP address) to access a set of pods, acting as a load balancer and enabling service discovery. This abstraction allows you to decouple the front-end from the back-end and simplify application scaling.

### NodePort / Ingress / Gateway

An Ingress is an API object that defines rules to route external traffic to services within the cluster. It provides load balancing, SSL termination, and name-based virtual hosting, making it easier to expose multiple services under a single IP address.

**Ingress vs. API Gateway**

### LoadBalancer

## Configuration

### Overview

ConfigMaps and Secrets allow you to separate both configuration data and sensitive information from container images, making it easy to manage and update configurations without rebuilding and redeploying containers.

### ConfigMaps

ConfigMaps allow to overwrite configuration information inside of a container to customize it without modifying the original base image.

### Secrets

## Advanced Concepts

### Namespaces

### Rights Management

### Service Accounts

### Persistence

### StatefulSet

### DaemonSet

### Init Containers

### Sidecar

### Operators

Operators are software extensions that help automate the management of Kubernetes resources. They use custom controllers and API extensions to manage complex tasks more efficiently and automatically.

Using operators can greatly simplify the management of applications and resources within your cluster. With their ability to automate tasks and provide advanced features, they are becoming increasingly popular among Kubernetes users.

## CI/CD

## Helm and Kustomize

### Kustomize

## Links

### Overview

- What is Kubernetes? An Introduction With Examples
- Kubernetes: An Introduction for Beginners
- GitHub: Kubernetes in Action, 2nd Edition
- kubectl cheatsheet

# Exercises

## Local Kubernetes Cluster Setup

### Docker Desktop Setup

Create Kubernetes Cluster: Kubeadm; show system container (for illustration). Above creates a single node cluster and puts config into `~/.kube/config`.

`kubectl` installed e.g. via `winget` or `chocolatey`.

```bash
cat ~/.kube/config
```

We work inside Git Bash. You might want to activate Tab-Completion via `source <(kubectl completion bash)`.

When working with multiple clusters, you can use

```bash
export KUBECONFIG=/path/to/custom/kubeconfig
```

to set the appropriate config. Default config is `~/.kube/config`.

### First Steps with `kubectl`

- `kubectl cluster-info`
- `kubectl get namespaces`
- `kubectl get nodes`
- `kubectl get pods -n kube-system`

---

- `kubectl cluster-info`
- `kubectl get namespaces`
- `kubectl config set-context --current --namespace <namespace_name>`
- `kubectl get nodes`
- `kubectl get pods -n kube-system`

---

```bash
kubectl cluster-info
kubectl get nodes
kubectl describe node docker-desktop
kubectl get namespaces
kubectl config set-context --current --namespace <namespace_name>
kubectl get pods -n kube-system
```

## Introduction to Kubernetes & Container Orchestration

### Exercise: First Docker Commands

- Start/stop a container

## `kubectl` – CLI for Kubernetes

### Basic Commands

1. **kubectl get** — Retrieves information about resources.

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

2. **kubectl describe** — Shows detailed information about a specific resource.

   ```sh
   # Describe a pod to get detailed info
   kubectl describe pod my-pod

   # Describe a deployment
   kubectl describe deployment my-deployment
   ```

3. **kubectl apply** — Applies configurations from files or stdin.

   ```sh
   # Apply a configuration from a file
   kubectl apply -f my-deployment.yaml

   # Apply multiple config files at once
   kubectl apply -f ./config-files/
   ```

4. **kubectl create** — Creates resources from files, stdin, or pre-defined templates.

   ```sh
   # Create a pod from a file
   kubectl create -f my-pod.yaml

   # Create a deployment with command line args (not commonly used)
   kubectl create deployment my-deployment --image=nginx
   ```

### Managing Pods and Deployments

5. **kubectl delete** — Deletes resources.

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

6. **kubectl logs** — Shows logs for a pod or container.

   ```sh
   # Get logs from a specific pod
   kubectl logs my-pod

   # Get logs with timestamps
   kubectl logs my-pod --timestamps

   # Stream logs (like tail -f)
   kubectl logs -f my-pod
   ```

7. **kubectl exec** — Executes commands in a container.

   ```sh
   # Run bash inside a pod's container
   kubectl exec -it my-pod -- /bin/bash

   # Execute a command without interactive terminal (-i and -t flags omitted)
   kubectl exec my-pod -- ls /app
   ```

8. **kubectl scale** — Scales the number of pods in a deployment.

   ```sh
   # Scale a deployment to 5 replicas
   kubectl scale deployment my-deployment --replicas=5

   # Scale using short form
   kubectl scale deploy my-deployment --replicas=10
   ```

### Configuring and Managing Namespaces

9. **kubectl config** — Modifies kubeconfig settings.

   ```sh
   # View the current context (cluster/namespace/user)
   kubectl config view

   # Switch to a different cluster context
   kubectl config use-context my-cluster

   # Set default namespace in your kubeconfig
   kubectl config set-context --current --namespace=my-namespace
   ```

10. **kubectl namespace** — Manages namespaces.

    ```sh
    # Create a new namespace
    kubectl create namespace my-namespace

    # Delete an existing namespace
    kubectl delete namespace my-namespace

    # List all namespaces
    kubectl get namespaces
    ```

### Advanced Commands

11. **kubectl rollout** — Manages rolling updates and rollbacks.

    ```sh
    # Check status of the last rollout
    kubectl rollout status deployment my-deployment

    # Rollback to previous revision
    kubectl rollout undo deployment my-deployment

    # Rollback to a specific revision
    kubectl rollout undo deployment my-deployment --to-revision=2
    ```

12. **kubectl cordon/uncordon** — Marks nodes as unschedulable/schedulable.

    ```sh
    # Mark node as unschedulable (maintenance mode)
    kubectl cordon my-node

    # Mark node as schedulable again after maintenance
    kubectl uncordon my-node
    ```

13. **kubectl drain** — Safely evicts pods from a node.

    ```sh
    # Evict all pods to prepare for maintenance
    kubectl drain my-node --ignore-daemonsets

    # Drain with more specific options (e.g., timeout)
    kubectl drain my-node --ignore-daemonsets --timeout=120s
    ```

## Deployment

### Exercise: Deploying Containers into the Cluster

- Access within the cluster
- `kubectl delete pod ...`

---

- Cluster access
- `kubectl delete pod ...`

---

```bash
kubectl create deployment kiada --image=luksa/kiada:0.1
kubectl get deployments
kubectl describe deployment kiada
kubectl get pods
kubectl describe pod kiada-5c98fddf88-8nq8c
```

```bash
kubectl delete pod kiada-5c98fddf88-8nq8c  # hangs about 30 seconds; how to return directly?
kubectl get pods # you should see an new pod created (deployment guarantees one running pod)
```

## Services & kube-proxy

### Exercise: Deployment with Service

- Replicas: 2
- NodePort (Gateway?)

## Configuration

### Exercise: Deployment with ConfigMap and Secret

## Helm and Kustomize

### Helm

```bash
helm install <releaseName> <chartDir> --namespace=<namespaceName>

helm get manifest <releaseName>

helm uninstall <releaseName>


helm list -n <namespace>
helm list --all-namespaces -o yaml|json
```

# Notes

- Contradiction: `Original/Vision.md` ("no cloud cluster, no Rancher-specific features") vs. `Original/README.md` (lists "Rancher or Docker Desktop installed" under installable software). Resolved in favor of `Original/Vision.md`: "Installing Required Software" lists only Git Bash and Docker Desktop; Rancher was dropped.
- Cross-topic duplicate: "Namespaces" appears under "Key Concepts" (the concept itself, with prose), under "`kubectl` – CLI for Kubernetes" → Overview (as a CLI operation area, e.g. `kubectl get namespaces`) and Exercises → "Configuring and Managing Namespaces" (explicit commands), and under "Advanced Concepts" (repeated in `Original/README.md`'s advanced-concepts bullet list).
- Filtered out (doesn't fit VISION.md guardrails): "Service-Mesh (e.g. Istio)" — found in `Original/Contents.qmd`. Service mesh (e.g. Istio) is a networking-infrastructure add-on layered on top of Kubernetes, not a concept within Kubernetes itself, and its coverage would drift into the "no infrastructure/cluster-ops deep dive (networking internals, …)" non-goal.

# Source Files

| Path | MD5 |
|---|---|
| Original/Contents.qmd | D057EEA503DFA29836D77EAC5A0DECB2 |
| Original/Practices.md | 91D82520F004190AAD2BB7FCAE9F168E |
| Original/README.md | 5B04DBEEC07A5E36F1D49B51E5BE1A96 |
| Original/Vision.md | 7157F268024FC29EF5F50A2BC79EF8F6 |
| Original/kubectl.md | 9D60FFD0B9953333DE2E8BF1F7F24D24 |
