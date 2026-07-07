---
revision: 3
title: "GFT Kubernetes-Workshop"
subtitle: "Contents"
abstract: "Definitive, section-organized list of workshop topics (headings and bullet points only); supersedes the narrative v1 draft."
lang: en
numbersections: true
state: in progress
finished_sections: [ ]
history:
  - "v2: replaced narrative v1 draft with a definitive, section-organized topic list (headings + bullets only) per TASKS.md 1.1; fixed invalid `state: preliminary` value and added missing `abstract` field per CLAUDE.md styleguide."
  - "v3: expanded every `##` subheading to at least 6 bullet points"
---

# What is Kubernetes and Why Should I Care?

## Container Orchestration

- Automated scheduling & placement
- Desired-state reconciliation
- Self-healing / auto-restart of failed containers
- Horizontal & vertical scaling
- Rolling updates without downtime
- Declarative configuration via manifests

## Kubernetes vs. Plain Docker/Containers

- Single host vs. multi-node cluster
- Manual `docker run`/`compose` vs. declarative manifests
- No built-in scheduling in plain Docker
- No built-in self-healing in plain Docker
- Docker Compose scope vs. cluster-wide orchestration
- When plain Docker is still sufficient

## Key Benefits

- Scalability
- Self-healing
- High availability
- Portability
- Resource efficiency
- Extensibility via API & ecosystem

# Kubernetes Architecture

## Cluster & Nodes Overview

- Cluster = set of nodes
- Control plane vs. worker roles
- Single-node vs. multi-node clusters
- Node = physical or virtual machine
- Cluster-wide vs. per-node resources
- How Docker Desktop's single-node cluster maps to this model

## Control Plane vs. Worker Nodes

- Control plane: cluster-wide decisions
- Worker nodes: run application containers
- Control plane can be single or multi-instance (HA)
- Node roles are labeled, not physically distinct
- Communication direction: API Server as central hub
- Failure impact: control plane vs. worker node outage

## Control Plane Components

- API Server
- Scheduler
- Controller Manager
- etcd
- Cloud Controller Manager (brief mention)
- All components communicate through the API Server

## Worker Node Components

- kubelet
- kube-proxy
- Container runtime
- Node-level resource reporting
- Pod lifecycle management on the node
- Container Runtime Interface (CRI) concept

# Pods & Namespaces

## Pods

- Smallest deployable unit
- Single- vs. multi-container pods
- Shared network namespace (localhost between containers)
- Shared storage volumes within a pod
- Pod lifecycle & phases
- Ephemeral nature (pods are not durable identities)

## Labels & Selectors

- Key/value metadata on objects
- Used by Deployments & Services to match pods
- Arbitrary vs. well-known labels
- Selector expressions (equality vs. set-based)
- Labels vs. annotations
- Common labeling conventions (app, version, environment)

## Namespaces

- Logical partitioning of a cluster
- Environment separation (dev/staging/prod)
- Namespace-scoped vs. cluster-scoped resources
- Default namespace
- Resource quotas per namespace (brief mention)
- Naming & switching context with `kubectl`

# `kubectl` — CLI for Kubernetes

## Basic Cluster Interaction

- cluster-info, namespaces, pods, logs, events
- Context & namespace switching
- `kubectl get` / `describe` / `logs` verbs
- Output formats (-o wide/yaml/json)
- `kubectl explain` for discovering fields
- Interacting with kube-system components

## Practice: First Steps with `kubectl`

- Inspect cluster & nodes
- List namespaces and system pods
- Switch active namespace
- View logs of a system pod
- List recent cluster events
- Explore a resource's fields via `kubectl explain`

# Deployments

## Deployments & ReplicaSets

- Deployment manages a ReplicaSet
- Declarative desired-state for Pods
- ReplicaSet ensures pod count matches spec
- Deployment adds versioned rollout history
- Relationship: Deployment → ReplicaSet → Pods
- When to use a bare ReplicaSet vs. a Deployment

## Replicas & Self-Healing

- Scaling replica count
- Automatic pod replacement on failure
- Horizontal scaling via `kubectl scale`
- Readiness affects traffic routing
- Liveness probes trigger restarts (brief mention)
- Manual vs. automatic (HPA) scaling (brief mention)

## Rolling Updates & Rollback

- Gradual version replacement
- Reverting to a previous revision
- Rollout strategies (RollingUpdate vs. Recreate)
- maxSurge / maxUnavailable concept
- Pausing & resuming a rollout
- Viewing rollout history & status

## Practice: Deploy Pod(s) into the Cluster

- Create & scale a Deployment
- Observe self-healing after deleting a pod
- Trigger a rolling update
- Roll back to a previous revision
- Inspect rollout status
- Clean up the Deployment

# Services & Networking

## Services

- Stable virtual IP/DNS name
- Load balancing across matching pods
- Decoupling consumers from pod IP churn
- Service discovery via DNS
- Selector-based endpoint matching
- Headless services (brief mention)

## Service Types

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName (brief mention)
- Default type behavior
- When to choose which type

## Ingress / Gateway API

- Host/path-based external routing
- Gateway API vs. Ingress
- TLS termination
- Single entrypoint for multiple services
- Ingress controller requirement
- Name-based virtual hosting

## Practice: Deployment with Services

- Expose a 2-replica Deployment
- Access via NodePort/Gateway
- Verify load balancing across replicas
- Inspect Service endpoints
- Test DNS-based service discovery
- Clean up Service & Deployment

# Configuration Management

## ConfigMaps

- Externalized non-sensitive configuration
- Env vars vs. mounted files
- Updating a ConfigMap without rebuilding images
- ConfigMap as command-line args source
- Immutable ConfigMaps (brief mention)
- Referencing a ConfigMap in a Pod spec

## Secrets

- Externalized sensitive data
- Access restrictions vs. ConfigMaps
- Base64 encoding vs. encryption (clarify: not encryption)
- Secret types (generic, docker-registry, tls)
- Mounting Secrets as files vs. env vars
- Least-privilege access considerations

## Practice: Deployment with ConfigMap and Secret

- Mount ConfigMap & Secret into a Deployment
- Verify values inside the container
- Update a ConfigMap and observe (non-)propagation
- Inject a Secret as an environment variable
- Compare file-mount vs. env-var access
- Clean up ConfigMap, Secret & Deployment

# Access Control

## RBAC

- Roles / RoleBindings
- ClusterRoles / ClusterRoleBindings
- Subjects (users, groups, service accounts)
- Verbs & resources in a Role rule
- Namespace-scoped vs. cluster-scoped permissions
- Principle of least privilege

## Service Accounts

- Pod identity toward the API server
- Default vs. custom service accounts
- Automatic token mounting
- Binding a Role to a Service Account
- Use cases: CI/CD, Operators, in-cluster tooling
- Disabling auto-mount for security

# Storage & State

## Persistence

- Volumes
- PersistentVolume / PersistentVolumeClaim
- StorageClass & dynamic provisioning (brief mention)
- Access modes (ReadWriteOnce, ReadWriteMany, etc.)
- Volume lifecycle vs. pod lifecycle
- emptyDir vs. persistent volumes

## StatefulSets

- Stable per-replica identity
- Ordered deployment & scaling
- Stable network identity per replica
- Stable storage per replica (via volumeClaimTemplates)
- Ordered, graceful termination
- Use cases: databases, distributed systems

# Workload Patterns

## DaemonSet

- One pod per (selected) node
- Use case: log/monitoring agents
- Node selectors/affinity for targeting
- Automatic scheduling on new nodes
- Comparison to Deployment (no fixed replica count)
- Update strategies for DaemonSets

## Init Containers

- Run-to-completion before app containers
- Use case: setup/dependency waits
- Sequential execution order
- Separate image/resource profile from app container
- Failure handling (pod restart on init failure)
- Common patterns: schema migration, config generation

## Sidecar Containers

- Auxiliary container in the same pod
- Use case: proxies, log shippers
- Shared network & volume with the main container
- Lifecycle coupling with the main container
- Native sidecar support (restartPolicy on init containers, brief mention)
- Examples: service mesh proxies, log forwarders

## Operators

- Custom controller + CRD
- Automates day-2 operational tasks
- Reconciliation loop pattern
- Encoding operational knowledge as code
- Examples: database operators, certificate operators
- Operator Framework / OperatorHub (brief mention)

# CI/CD with Kubernetes

## GitOps Concept

- Git as source of truth
- Automated sync/reconciliation (conceptual)
- Pull-based vs. push-based deployment
- Declarative desired state stored in Git
- Drift detection & auto-correction
- Auditability via commit history

## Deployment Pipelines (Conceptual)

- Build → test → package → deploy
- Environment promotion (dev → staging → prod)
- Image tagging & versioning strategy
- Automated rollout triggers
- Rollback as part of the pipeline
- Separation of CI (build/test) and CD (deploy) concerns

# Package Management: Helm & Kustomize

## Helm

- Package manager ("charts") for Kubernetes
- Install/upgrade/rollback as a unit
- Templating with values files
- Chart repositories
- Release versioning & history
- Managing multi-resource applications as one unit

## Kustomize

- Overlay-based YAML customization
- Built into `kubectl -k`
- Base + overlay pattern
- Patches vs. templating (Kustomize vs. Helm)
- Environment-specific overlays (dev/staging/prod)
- No templating language required

# Service Mesh

## Purpose & Basic Concept

- Service-to-service traffic layer (routing, retries, mTLS)
- Examples: Istio, Traefik Mesh
- Sidecar proxy pattern
- Observability (traffic metrics, tracing)
- Traffic splitting / canary routing
- When a service mesh is (not) needed

# Further Reading / Links

- [What is Kubernetes? An Introduction With Examples](https://www.datacamp.com/blog/what-is-kubernetes)
- [Kubernetes: An Introduction for Beginners](https://tecadmin.net/kubernetes-introduction/)
- [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)
- [kubectl cheatsheet](https://kubernetes.io/de/docs/reference/kubectl/cheatsheet/)
