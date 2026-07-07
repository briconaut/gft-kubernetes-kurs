---
revision: 1
title: "GFT Kubernetes-Workshop"
subtitle: "Practices"
abstract: "Overview of planned practices. Used images based on [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)"
lang: en
numbersections: true
state: preliminary
finished_sections: [ ]
history: [ ]
---

# Local K8s Cluster Setup

## Docker Desktop on Win11 (4.57.0)

### Activate K8s in Gui

- Create Kubernetes Cluster: Kubeadm (v1.34.1); show system container (for illustration)

Above creates single node cluster and puts config into `~/.kube/config`

### `kubectl`

Installed e.g. via `winget` or `chocolatey`

```bash
cat ~/.kube/config
```

### Environment

We work inside Git Bash.

You might want to activate Tab-Completion via `source <(kubectl completion bash)`.

When working with multiple clusters, you can use

```bash
export KUBECONFIG=/path/to/custom/kubeconfig
```

to set the appropriate config.
Default config is `~/.kube/config`


# First steps with `kubectl`

```bash
kubectl cluster-info
kubectl get nodes
kubectl describe node docker-desktop
kubectl get namespaces
kubectl config set-context --current --namespace <namespace_name>
kubectl get pods -n kube-system
```


# Deployment of 2 containers into cluster


## Deploy your first application:

```bash
kubectl create deployment kiada --image=luksa/kiada:0.1
kubectl get deployments
kubectl describe deployment kiada
kubectl get pods
kubectl describe pod kiada-5c98fddf88-8nq8c
```

## Cluster access

```bash
kubectl delete pod kiada-5c98fddf88-8nq8c  # hangs about 30 seconds; how to return directly?
kubectl get pods # you should see an new pod created (deployment guarantees one running pod)
```


# Deployment with Services

- Replica: 2
- NodePort (Gateway?)


# Deployment with ConfigMap and Secret


