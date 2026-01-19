# 2025-Kubernetes-Workshop

## 🧭 Workshop Overview

- **Dauer**: 4 Stunden  
- **Publikum**: Keine Erfahrung, aber technisches Publikum - primär Entwickler (auch für Business-Consultants?)
- **Voraussetzungen**:
  - Git-Bash
  - Rancher oder Docker Desktop installiert
  - GitLab Zugang (lesend)

---

## Installation der nötigen Software

- Git-Bash
- Rancher oder Docker Desktop installieren

## 📘 Vorwissen

- Container-Kenntnisse
- Shell-Kenntnisse

---

## 🚀 Inhalte

### 1. Container Orchestrierung – Einführung & Motivation

### 2. Kubernetes-Architektur

- Cluster
- Nodes
- Pods + Container (-Runtime)
- Networking
- Namespaces
- Flüchtigkeit + Persistenz
- 12 Factor Apps

### 3. `kubectl` – CLI für Kubernetes

- cluster-info
- Namespaces
- Pods
- Logs
- Events

#### 🧪 Übung: Erste kubectl Befehle

- Kubernetes starten
- `kubectl cluster-info`
- `kubectl get namespaces`
- `kubectl get nodes`
- `kubectl get pods -n kube-system`

### 4. Deployment

- Deployment-Typen
- Replicas

#### 🧪 Übung: Deployment von 2 Containern im Cluster

- Zugriff im Cluster
- `kubectl delete pod ...`

### 5. Services & Kube-Proxy

- Kube-Proxy erklären

- Labels und Selectors

- Service-Typen:
  - NodePort
  - Ingress
  - Gateway
  - LoadBalancer

#### 🧪 Übung: Deployment mit Service

- Replica: 2
- NodePort (Gateway?)

### 6. Konfiguration

- ConfigMaps
- Secrets

#### 🧪 Übung: Deployment mit ConfigMap und Secret

### 7. Erweiterte Konzepte

- Namespaces
- Rechte-Management
- Service-Accounts
- Persistenz
- StatefulSet
- DaemonSet
- Init-Container

### 8. CI / CD mit Kubernetes

### 9. Deployment Templates: Helm und Kustomize
