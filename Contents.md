---
revision: 8
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
  - "v6: revision bump only — build-contents run aborted before content changes."
  - "v7: enumerate — updated all 34 lesson file references to .lesson.md extension; no files moved (none exist yet)."
  - "v8: fill-subtopic 02.01 — added 6 subjects to What Are Containers."
---

------------------------------------------------------------------------------

# 01 Local Kubernetes Cluster Setup

## [01.01 Installing Docker Desktop](<Contents/01-Local Kubernetes Cluster Setup/01.01-Installing Docker Desktop.lesson.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.01-Installing Docker Desktop.lesson.md -->

- Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
- Enable Kubernetes in Docker Desktop's settings/preferences
- Docker Desktop provisions a single-node, kubeadm-based Kubernetes cluster
- Verify Kubernetes is running via Docker Desktop's status indicator
- Resulting cluster configuration is written to `~/.kube/config`
- No cloud account or external cluster required — everything runs locally

## [01.02 Installing Rancher Desktop](<Contents/01-Local Kubernetes Cluster Setup/01.02-Installing Rancher Desktop.lesson.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.02-Installing Rancher Desktop.lesson.md -->

- Download and install Rancher Desktop for your operating system (Windows/macOS/Linux)
- Choose a container runtime (dockerd/moby or containerd) during setup
- Enable Kubernetes in Rancher Desktop's preferences
- Rancher Desktop provisions a local, single-node k3s-based Kubernetes cluster
- Resulting cluster configuration is written to `~/.kube/config`
- Rancher Desktop and Docker Desktop cannot run their Kubernetes clusters at the same time — only one can be active

## [01.03 Enable Kubernetes](<Contents/01-Local Kubernetes Cluster Setup/01.03-Enable Kubernetes.lesson.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.03-Enable Kubernetes.lesson.md -->

- Enable Kubernetes in Docker Desktop
- Enable Kubernetes in Rancher Desktop

## [01.04 Installing git-bash](<Contents/01-Local Kubernetes Cluster Setup/01.04-Installing git-bash.lesson.md>)
<!-- lesson: Contents/01-Local Kubernetes Cluster Setup/01.04-Installing git-bash.lesson.md -->

- Download and install Git for Windows, which bundles Git Bash
- Git Bash provides a bash-compatible shell used for all `kubectl` and command-line exercises
- Optionally enable `kubectl` tab-completion via `source <(kubectl completion bash)`
- Verify Git Bash opens correctly and runs basic shell commands
- Git Bash is the assumed terminal environment throughout the workshop

------------------------------------------------------------------------------

# 02 Introduction to Kubernetes & Container Orchestration

## [02.01 What Are Containers](<Contents/02-Introduction to Kubernetes & Container Orchestration/02.01-What Are Containers.lesson.md>)
<!-- lesson: Contents/02-Introduction to Kubernetes & Container Orchestration/02.01-What Are Containers.lesson.md -->

- A container is an isolated, portable process bundling the application with its dependencies and configuration
- Container image as an immutable, layered build artifact; a running container as an instance spawned from that image
- Containers vs. virtual machines: shared host OS kernel, lighter resource footprint, faster startup time
- Container runtime (e.g. containerd, Docker Engine) as the component that starts, stops, and manages containers on a host
- Image registries (Docker Hub, private registries) as the distribution layer for container images
- Why many containers across many hosts introduce scheduling, networking, and lifecycle challenges — the gap Kubernetes fills

## [02.02 What is Kubernetes](<Contents/02-Introduction to Kubernetes & Container Orchestration/02.02-What is Kubernetes.lesson.md>)
<!-- lesson: Contents/02-Introduction to Kubernetes & Container Orchestration/02.02-What is Kubernetes.lesson.md -->

------------------------------------------------------------------------------

# 03 Kubernetes Architecture

## [03.01 Overview](<Contents/03-Kubernetes Architecture/03.01-Overview.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.01-Overview.lesson.md -->

## [03.02 Control Plane](<Contents/03-Kubernetes Architecture/03.02-Control Plane.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.02-Control Plane.lesson.md -->

## [03.03 Worker Nodes](<Contents/03-Kubernetes Architecture/03.03-Worker Nodes.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.03-Worker Nodes.lesson.md -->

## [03.04 Networking](<Contents/03-Kubernetes Architecture/03.04-Networking.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.04-Networking.lesson.md -->

## [03.05 Data Storage](<Contents/03-Kubernetes Architecture/03.05-Data Storage.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.05-Data Storage.lesson.md -->

------------------------------------------------------------------------------

# 04 Key Concepts

## [04.01 Pods + Container (Runtime)](<Contents/04-Key Concepts/04.01-Pods + Container (Runtime).lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.01-Pods + Container (Runtime).lesson.md -->

## [04.02 Services](<Contents/04-Key Concepts/04.02-Services.lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.02-Services.lesson.md -->

## [04.03 Namespaces](<Contents/04-Key Concepts/04.03-Namespaces.lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.03-Namespaces.lesson.md -->

------------------------------------------------------------------------------

# 05 Deployment

## [05.01 Why not just pods?](<Contents/05-Deployment/05.01-Why not just pods?.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.01-Why not just pods?.lesson.md -->

## [05.02 Deployment Types](<Contents/05-Deployment/05.02-Deployment Types.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.02-Deployment Types.lesson.md -->

## [05.03 Replicas](<Contents/05-Deployment/05.03-Replicas.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.03-Replicas.lesson.md -->

## [05.04 Deployments Overview](<Contents/05-Deployment/05.04-Deployments Overview.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.04-Deployments Overview.lesson.md -->

------------------------------------------------------------------------------

# 06 Services & kube-proxy

## [06.01 kube-proxy](<Contents/06-Services & kube-proxy/06.01-kube-proxy.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.01-kube-proxy.lesson.md -->

## [06.02 Labels and Selectors](<Contents/06-Services & kube-proxy/06.02-Labels and Selectors.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.02-Labels and Selectors.lesson.md -->

## [06.03 NodePort / Ingress / Gateway](<Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.lesson.md -->

## [06.04 LoadBalancer](<Contents/06-Services & kube-proxy/06.04-LoadBalancer.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.04-LoadBalancer.lesson.md -->

------------------------------------------------------------------------------

# 07 Configuration

## [07.01 ConfigMaps](<Contents/07-Configuration/07.01-ConfigMaps.lesson.md>)
<!-- lesson: Contents/07-Configuration/07.01-ConfigMaps.lesson.md -->

## [07.02 Secrets](<Contents/07-Configuration/07.02-Secrets.lesson.md>)
<!-- lesson: Contents/07-Configuration/07.02-Secrets.lesson.md -->

------------------------------------------------------------------------------

# 08 Advanced Concepts

## [08.01 Rights Management](<Contents/08-Advanced Concepts/08.01-Rights Management.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.01-Rights Management.lesson.md -->

## [08.02 Service Accounts](<Contents/08-Advanced Concepts/08.02-Service Accounts.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.02-Service Accounts.lesson.md -->

## [08.03 Persistence](<Contents/08-Advanced Concepts/08.03-Persistence.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.03-Persistence.lesson.md -->

## [08.04 StatefulSet](<Contents/08-Advanced Concepts/08.04-StatefulSet.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.04-StatefulSet.lesson.md -->

## [08.05 DaemonSet](<Contents/08-Advanced Concepts/08.05-DaemonSet.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.05-DaemonSet.lesson.md -->

## [08.06 Init Containers](<Contents/08-Advanced Concepts/08.06-Init Containers.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.06-Init Containers.lesson.md -->

## [08.07 Sidecar](<Contents/08-Advanced Concepts/08.07-Sidecar.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.07-Sidecar.lesson.md -->

## [08.08 Operators](<Contents/08-Advanced Concepts/08.08-Operators.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.08-Operators.lesson.md -->

------------------------------------------------------------------------------

# 09 Helm and Kustomize

## [09.01 Helm](<Contents/09-Helm and Kustomize/09.01-Helm.lesson.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.01-Helm.lesson.md -->

## [09.02 Kustomize](<Contents/09-Helm and Kustomize/09.02-Kustomize.lesson.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.02-Kustomize.lesson.md -->
