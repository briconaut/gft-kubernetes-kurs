---
revision: 5
path: "Contents.md"
title: "GFT Kubernetes-Workshop"
subtitle: "Contents"
abstract: "Definitive, section-organized list of workshop topics (headings and bullet points only); supersedes the narrative v1 draft."
lang: en
numbersections: true
state: in progress
finished_sections: [ ]
history:
  - "v1: intial, empty version."
  - "v2: Filling 01.01 with content."
  - "v3: Filling 01.02 with content."
  - "v4: Filling 01.03 with content."
  - "v5: build-contents sync with TOPICS.md rev 1."
---

------------------------------------------------------------------------------

# 01 Local Kubernetes Cluster Setup

## [01.01 Installing Docker Desktop](<Contents/01-Local Kubernetes Cluster Setup/01.01-Installing Docker Desktop.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.01-Installing Docker Desktop.md -->

- Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
- Enable Kubernetes in Docker Desktop's settings/preferences
- Docker Desktop provisions a single-node, kubeadm-based Kubernetes cluster
- Verify Kubernetes is running via Docker Desktop's status indicator
- Resulting cluster configuration is written to `~/.kube/config`
- No cloud account or external cluster required — everything runs locally

## [01.02 Installing Rancher Desktop](<Contents/01-Local Kubernetes Cluster Setup/01.02-Installing Rancher Desktop.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.02-Installing Rancher Desktop.md -->

- Download and install Rancher Desktop for your operating system (Windows/macOS/Linux)
- Choose a container runtime (dockerd/moby or containerd) during setup
- Enable Kubernetes in Rancher Desktop's preferences
- Rancher Desktop provisions a local, single-node k3s-based Kubernetes cluster
- Resulting cluster configuration is written to `~/.kube/config`
- Rancher Desktop and Docker Desktop cannot run their Kubernetes clusters at the same time — only one can be active

## [01.03 Enable Kubernetes](<Contents/01-Local Kubernetes Cluster Setup/01.03-Enable Kubernetes.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.03-Enable Kubernetes.md -->

## [01.04 Installing git-bash](<Contents/01-Local Kubernetes Cluster Setup/01.04-Installing git-bash.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.04-Installing git-bash.md -->

- Download and install Git for Windows, which bundles Git Bash
- Git Bash provides a bash-compatible shell used for all `kubectl` and command-line exercises
- Optionally enable `kubectl` tab-completion via `source <(kubectl completion bash)`
- Verify Git Bash opens correctly and runs basic shell commands
- Git Bash is the assumed terminal environment throughout the workshop

------------------------------------------------------------------------------

# 02 Introduction to Kubernetes & Container Orchestration

## [02.01 What Are Containers](<Contents/02-Introduction to Kubernetes & Container Orchestration/02.01-What Are Containers.md>)
<!-- lesson: Contents/02-Introduction to Kubernetes & Container Orchestration/02.01-What Are Containers.md -->

## [02.02 What is Kubernetes](<Contents/02-Introduction to Kubernetes & Container Orchestration/02.02-What is Kubernetes.md>)
<!-- lesson: Contents/02-Introduction to Kubernetes & Container Orchestration/02.02-What is Kubernetes.md -->

------------------------------------------------------------------------------

# 03 Kubernetes Architecture

## [03.01 Overview](<Contents/03-Kubernetes Architecture/03.01-Overview.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.01-Overview.md -->

## [03.02 Control Plane](<Contents/03-Kubernetes Architecture/03.02-Control Plane.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.02-Control Plane.md -->

## [03.03 Worker Nodes](<Contents/03-Kubernetes Architecture/03.03-Worker Nodes.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.03-Worker Nodes.md -->

## [03.04 Networking](<Contents/03-Kubernetes Architecture/03.04-Networking.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.04-Networking.md -->

## [03.05 Data Storage](<Contents/03-Kubernetes Architecture/03.05-Data Storage.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.05-Data Storage.md -->

------------------------------------------------------------------------------

# 04 Key Concepts

## [04.01 Pods + Container (Runtime)](<Contents/04-Key Concepts/04.01-Pods + Container (Runtime).md>)
<!-- lesson: Contents/04-Key Concepts/04.01-Pods + Container (Runtime).md -->

## [04.02 Services](<Contents/04-Key Concepts/04.02-Services.md>)
<!-- lesson: Contents/04-Key Concepts/04.02-Services.md -->

## [04.03 Namespaces](<Contents/04-Key Concepts/04.03-Namespaces.md>)
<!-- lesson: Contents/04-Key Concepts/04.03-Namespaces.md -->

------------------------------------------------------------------------------

# 05 Deployment

## [05.01 Why not just pods?](<Contents/05-Deployment/05.01-Why not just pods?.md>)
<!-- lesson: Contents/05-Deployment/05.01-Why not just pods?.md -->

## [05.02 Deployment Types](<Contents/05-Deployment/05.02-Deployment Types.md>)
<!-- lesson: Contents/05-Deployment/05.02-Deployment Types.md -->

## [05.03 Replicas](<Contents/05-Deployment/05.03-Replicas.md>)
<!-- lesson: Contents/05-Deployment/05.03-Replicas.md -->

## [05.04 Deployments Overview](<Contents/05-Deployment/05.04-Deployments Overview.md>)
<!-- lesson: Contents/05-Deployment/05.04-Deployments Overview.md -->

------------------------------------------------------------------------------

# 06 Services & kube-proxy

## [06.01 kube-proxy](<Contents/06-Services & kube-proxy/06.01-kube-proxy.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.01-kube-proxy.md -->

## [06.02 Labels and Selectors](<Contents/06-Services & kube-proxy/06.02-Labels and Selectors.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.02-Labels and Selectors.md -->

## [06.03 NodePort / Ingress / Gateway](<Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.md -->

## [06.04 LoadBalancer](<Contents/06-Services & kube-proxy/06.04-LoadBalancer.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.04-LoadBalancer.md -->

------------------------------------------------------------------------------

# 07 Configuration

## [07.01 ConfigMaps](<Contents/07-Configuration/07.01-ConfigMaps.md>)
<!-- lesson: Contents/07-Configuration/07.01-ConfigMaps.md -->

## [07.02 Secrets](<Contents/07-Configuration/07.02-Secrets.md>)
<!-- lesson: Contents/07-Configuration/07.02-Secrets.md -->

------------------------------------------------------------------------------

# 08 Advanced Concepts

## [08.01 Rights Management](<Contents/08-Advanced Concepts/08.01-Rights Management.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.01-Rights Management.md -->

## [08.02 Service Accounts](<Contents/08-Advanced Concepts/08.02-Service Accounts.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.02-Service Accounts.md -->

## [08.03 Persistence](<Contents/08-Advanced Concepts/08.03-Persistence.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.03-Persistence.md -->

## [08.04 StatefulSet](<Contents/08-Advanced Concepts/08.04-StatefulSet.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.04-StatefulSet.md -->

## [08.05 DaemonSet](<Contents/08-Advanced Concepts/08.05-DaemonSet.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.05-DaemonSet.md -->

## [08.06 Init Containers](<Contents/08-Advanced Concepts/08.06-Init Containers.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.06-Init Containers.md -->

## [08.07 Sidecar](<Contents/08-Advanced Concepts/08.07-Sidecar.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.07-Sidecar.md -->

## [08.08 Operators](<Contents/08-Advanced Concepts/08.08-Operators.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.08-Operators.md -->

------------------------------------------------------------------------------

# 09 Helm and Kustomize

## [09.01 Helm](<Contents/09-Helm and Kustomize/09.01-Helm.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.01-Helm.md -->

## [09.02 Kustomize](<Contents/09-Helm and Kustomize/09.02-Kustomize.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.02-Kustomize.md -->
