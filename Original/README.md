---
revision: 1
title: "README.md"
abstract: "Structure and contents of the kubernetes workshop"
lang: en
numbersections: true
state: preliminary
finished_sections: [ ]
history: [ ]
---


# 2025-Kubernetes-Workshop

## 🧭 Workshop Overview

- **Duration**: 4 hours  
- **Audience**: A technical audience with litte knowledge about kubernetes - primarily developers (also for business consultants?)
- **Prerequisites**:
  - Git Bash
  - Rancher or Docker Desktop installed
  - GitLab access (read-only)

---

## Installing the required software

- Git Bash
- Install Rancher or Docker Desktop

## 📘 Prior knowledge

- Container/Docker knowledge
- Shell knowledge (bash)

---

## 🚀 Contents

### 1. Container orchestration – introduction & motivation

- What are containers

#### 🧪 Exercise: First docker commands

- Sart/stop a container

### 2. Kubernetes architecture / infrastructure

#### Infrastructure

- Cluster
- Nodes
- Networking
- Data stroage

#### Basic concepts

- Pods + container (runtime)
- Services
- Namespaces
- Ports & Gateways
- Ephemerality + persistence

### 3. `kubectl` – CLI for Kubernetes

- cluster-info
- Namespaces
- Pods
- Logs
- Events

#### 🧪 Exercise: First kubectl commands

- Start Kubernetes
- `kubectl cluster-info`
- `kubectl get namespaces`
- `kubectl get nodes`
- `kubectl get pods -n kube-system`

### 4. Deployment

- Deployment types
- Replicas

#### 🧪 Exercise: Deploying 2 containers in the cluster

- Access within the cluster
- `kubectl delete pod ...`

### 5. Services & kube-proxy

- Explain kube-proxy

- Labels and selectors

- Service types:
  - NodePort
  - Ingress
  - Gateway
  - LoadBalancer

#### 🧪 Exercise: Deployment with service

- Replicas: 2
- NodePort (Gateway?)

### 6. Configuration

- ConfigMaps
- Secrets

#### 🧪 Exercise: Deployment with ConfigMap and secret

### 7. Advanced concepts

- Namespaces
- Rights management
- Service accounts
- Persistence
- StatefulSet
- DaemonSet
- Init containers

### 8. CI / CD with Kubernetes

### 9. Deployment templates: Helm and Kustomize