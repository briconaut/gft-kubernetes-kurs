---
revision: 1
title: "GFT Kubernetes-Workshop"
subtitle: "Contents"
lang: en
numbersections: true
state: preliminary
finished_sections: [ ]
history: [ ]
---

# What is Kubernetes and Why should I Care? 

Kubernetes is an open-source **container orchestration platform** that automates the deployment, scaling, and management of containerized applications.
Originally developed by Google and open-sourced in 2014.

It abstracts away the complexity of managing individual containers and allows developers to focus on building and deploying their applications.

Some key benefits of using Kubernetes:

- **Container orchestration**: Automates the distribution and scheduling of containers across a cluster.
- **Scalability and self-healing**: Simplifies [horizontal scaling](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.concept.horizontal-scaling.en.html) (replicating containers) and vertical scaling (adjusting resource allocation) all with self-healing capabilities.
- **High availability**: Ensures containers (and thus your services) remain operational even if some nodes fail.
- **Portability**: Abstracts the underlying infrastructure, making it straightforward to run both on-premises and on different cloud providers.
- **Efficient resource utilization**: Resizes containers based on resource usage, optimizing resource allocation and reducing costs.


# Core Components of Kubernetes / Kubernetes-Architecture

Kubernetes clusters are groups of [nodes](https://kubernetes.io/docs/concepts/architecture/nodes/), which are individual machines that run the Kubernetes software.
A Kubernetes cluster consists logically of two components:

- **Controll Plane** is responsible for coordinating all activities within the cluster
- **(Worker) Node(s)** handle running and managing containers


Source: [Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

![Components of Kubernetes](.media/components-of-kubernetes.svg){width=12cm height=6cm}


## Control Plane

The control plane is the set of components that manage the overall state of the cluster.
It includes the following components:

- **API Server**: The Kubernetes API server is the front-end for the control plane, exposing the Kubernetes API to users and other components.
This component acts as the central management point for all Kubernetes resources. It receives requests from users and other components and then enforces policies to manage the cluster.
- **Controller Manager**: The controller manager manages the core control loops in Kubernetes, ensuring the desired state of the cluster is maintained by constantly monitoring and reconciling changes made to objects within the cluster.
- **Scheduler**: The scheduler is responsible for assigning pods to available nodes based on resource requirements and other constraints.
- **etcd** is a distributed key-value store that serves as the primary datastore for Kubernetes. It stores all cluster data and ensures data consistency and availability.


## Worker Nodes

Worker Nodes are the worker machines that run containerized applications.
Each node runs the container runtime (e.g., Docker or containerd) and the Kubernetes agent called kubelet, which communicates with the control plane.

- **kubelet**: This agent runs on each node in the cluster and is responsible for managing containers, ensuring they are running according to their specified configurations.
- **Kube Proxy**: This component runs on each node and is responsible for routing network traffic to the correct container.



# Key Concepts

![Kubernetes Concepts](.media/KubernetesConcepts.svg){width=14cm height=8cm}

## Pods + Container (-Runtime)

A pod encapsulates one or more containers, storage resources, and a unique network IP, allowing containers within the pod to share the same network namespace.
It is the smallest unit of deployment in Kubernetes.

Each pod has its own unique IP address and can communicate with other pods in the same cluster through this address.
This allows for efficient communication between different components of an application.

Pods can come in either single or multi-container pods and each comes with their own use case.

- **Single-container pods**: The most common type of pod, where a single container is running inside. This is useful for simple applications or microservices that only require one container.
- **Multi-container pods**: Multiple containers are co-located and run together. This can be beneficial for complex applications where different containers need to communicate with each other and share resources.


## Namespaces

[Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) provide a way to logically partition resources within a single cluster.
This allows for better organization and management of resources, as well as tighter security controls.

Namespaces can also be used to manage different environments, such as development, staging, and production.
This ensures that resources are isolated and not affected by changes made in other environments.


# `kubectl` – CLI für Kubernetes

- cluster-info
- Namespaces
- Pods
- Logs
- Events

## Practice: First steps with `kubectl`

- `kubectl cluster-info`
- `kubectl get namespaces`
- `kubectl config set-context --current --namespace <namespace_name>`
- `kubectl get nodes`
- `kubectl get pods -n kube-system`


# Deployment

## Practice: Deployment of a pod into the cluster

## Deployments

Deployments provide declarative updates for pods and their associated replica sets.
They enable rolling updates, canary deployments, and rollback functionality to manage the desired state of your applications.

- Deployment-Typen
- Replicas

## Practice: Deployment of 2 containers into cluster

- Cluster access
- `kubectl delete pod ...`


# Services & Kube-Proxy

## Services

Services provide a stable network address (stable DNS name, stable IP address) to access a set of pods, acting as a load balancer and enabling service discovery.
This abstraction allows you to decouple the front-end from the back-end and simplify application scaling.


## NodePort / Ingress / Gateway

An Ingress is an API object that defines rules to route external traffic to services within the cluster.
It provides load balancing, SSL termination, and name-based virtual hosting, making it easier to expose multiple services under a single IP address.

### Ingress vs. API Gateway

- [Anas T - 2024-01 - Kubernetes Gateway API vs Kubernetes Ingress](https://imesh.ai/blog/kubernetes-gateway-api-vs-ingress/)


## LoadBalancer

## Practice: Deployment with Services

- Replica: 2
- NodePort (Gateway?)


# Configuration

ConfigMaps and Secrets allow you to separate both configuration data and sensitive information from container images, making it easy to manage and update configurations without rebuilding and redeploying containers.

## ConfigMaps

ConfigMaps allow to overwrite configuration information inside of a container to customize it without modifying the original base image.


## Secrets

## Practice: Deployment with ConfigMap and Secret


# Additional/Advanced Conepts

## Rechte-Management

## Service-Accounts

## Persistence

## StatefulSet

## DaemonSet

## Init-Container

## Sidecar

## Operators

[Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) are software extensions that help automate the management of Kubernetes resources. They use custom controllers and API extensions to manage complex tasks more efficiently and automatically.

Using operators can greatly simplify the management of applications and resources within your cluster.
With their ability to automate tasks and provide advanced features, they are becoming increasingly popular among Kubernetes users.


# CI / CD

# Helm und Kustomize

## [Helm](https://helm.sh/docs/intro/install/)

```bash
helm install <releaseName> <chartDir> --namespace=<namespaceName>

helm get manifest <releaseName>

helm uninstall <releaseName>


helm list -n <namespace>
helm list --all-namespaces -o yaml|json
```


# Service-Mesh (e.g. Istio)

A service mesh is a dedicated infrastructure layer that controls service-to-service communication in a microservices architecture.
It manages the routing of service requests to other services, performs load balancing, encrypts data, and discovers other services.

- [Istio](https://istio.io)
- [Traefik Mesh](https://doc.traefik.io/traefik-mesh/)


# Links

- [What is Kubernetes? An Introduction With Examples](https://www.datacamp.com/blog/what-is-kubernetes)
- [Kubernetes: An Introduction for Beginners](https://tecadmin.net/kubernetes-introduction/)
- [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)
- [kubectl cheatsheet](https://kubernetes.io/de/docs/reference/kubectl/cheatsheet/)
