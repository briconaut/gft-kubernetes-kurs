---
revision: 2
title: "GFT Kubernetes-Workshop"
subtitle: "Contents"
abstract: "Definitive, section-organized list of workshop topics (headings and bullet points only); supersedes the narrative v1 draft."
lang: en
numbersections: true
state: in progress
finished_sections: [ ]
history:
  - "v2: replaced narrative v1 draft with a definitive, section-organized topic list (headings + bullets only) per TASKS.md 1.1; fixed invalid `state: preliminary` value and added missing `abstract` field per CLAUDE.md styleguide."
---

# What is Kubernetes and Why Should I Care?

## Container Orchestration

- Automated scheduling & placement
- Desired-state reconciliation

## Kubernetes vs. Plain Docker/Containers

- Single host vs. multi-node cluster
- Manual `docker run`/`compose` vs. declarative manifests

## Key Benefits

- Scalability
- Self-healing
- High availability
- Portability
- Resource efficiency

# Kubernetes Architecture

## Cluster & Nodes Overview

- Cluster = set of nodes
- Control plane vs. worker roles

## Control Plane vs. Worker Nodes

- Control plane: cluster-wide decisions
- Worker nodes: run application containers

## Control Plane Components

- API Server
- Scheduler
- Controller Manager
- etcd

## Worker Node Components

- kubelet
- kube-proxy
- Container runtime

# Pods & Namespaces

## Pods

- Smallest deployable unit
- Single- vs. multi-container pods

## Labels & Selectors

- Key/value metadata on objects
- Used by Deployments & Services to match pods

## Namespaces

- Logical partitioning of a cluster
- Environment separation (dev/staging/prod)

# `kubectl` — CLI for Kubernetes

## Basic Cluster Interaction

- cluster-info, namespaces, pods, logs, events
- Context & namespace switching

## Practice: First Steps with `kubectl`

- Inspect cluster & nodes
- List namespaces and system pods

# Deployments

## Deployments & ReplicaSets

- Deployment manages a ReplicaSet
- Declarative desired-state for Pods

## Replicas & Self-Healing

- Scaling replica count
- Automatic pod replacement on failure

## Rolling Updates & Rollback

- Gradual version replacement
- Reverting to a previous revision

## Practice: Deploy Pod(s) into the Cluster

- Create & scale a Deployment
- Observe self-healing after deleting a pod

# Services & Networking

## Services

- Stable virtual IP/DNS name
- Load balancing across matching pods

## Service Types

- ClusterIP
- NodePort
- LoadBalancer

## Ingress / Gateway API

- Host/path-based external routing
- Gateway API vs. Ingress

## Practice: Deployment with Services

- Expose a 2-replica Deployment
- Access via NodePort/Gateway

# Configuration Management

## ConfigMaps

- Externalized non-sensitive configuration
- Env vars vs. mounted files

## Secrets

- Externalized sensitive data
- Access restrictions vs. ConfigMaps

## Practice: Deployment with ConfigMap and Secret

- Mount ConfigMap & Secret into a Deployment
- Verify values inside the container

# Access Control

## RBAC

- Roles / RoleBindings
- ClusterRoles / ClusterRoleBindings

## Service Accounts

- Pod identity toward the API server
- Default vs. custom service accounts

# Storage & State

## Persistence

- Volumes
- PersistentVolume / PersistentVolumeClaim

## StatefulSets

- Stable per-replica identity
- Ordered deployment & scaling

# Workload Patterns

## DaemonSet

- One pod per (selected) node
- Use case: log/monitoring agents

## Init Containers

- Run-to-completion before app containers
- Use case: setup/dependency waits

## Sidecar Containers

- Auxiliary container in the same pod
- Use case: proxies, log shippers

## Operators

- Custom controller + CRD
- Automates day-2 operational tasks

# CI/CD with Kubernetes

## GitOps Concept

- Git as source of truth
- Automated sync/reconciliation (conceptual)

## Deployment Pipelines (Conceptual)

- Build → test → package → deploy
- Environment promotion (dev → staging → prod)

# Package Management: Helm & Kustomize

## Helm

- Package manager ("charts") for Kubernetes
- Install/upgrade/rollback as a unit

## Kustomize

- Overlay-based YAML customization
- Built into `kubectl -k`

# Service Mesh

## Purpose & Basic Concept

- Service-to-service traffic layer (routing, retries, mTLS)
- Examples: Istio, Traefik Mesh

# Further Reading / Links

- [What is Kubernetes? An Introduction With Examples](https://www.datacamp.com/blog/what-is-kubernetes)
- [Kubernetes: An Introduction for Beginners](https://tecadmin.net/kubernetes-introduction/)
- [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)
- [kubectl cheatsheet](https://kubernetes.io/de/docs/reference/kubectl/cheatsheet/)
