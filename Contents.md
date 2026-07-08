---
revision: 8
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
  - "v4: rephrased every `##` topic heading as a concrete, answerable question in audience terms per TASKS.md 1.2; left `#` section headings and `## Practice: ...` headings unchanged"
  - "v5: tightened bullets under \"What components run on a worker node?\" to name components rather than responsibilities, per bullet/question fit review"
  - "v6: completeness pass — added Pod IP address bullet, `kubectl apply/create/delete` bullet, Docker Desktop hostpath StorageClass bullet, GitOps tool examples (Argo CD/Flux); replaced a redundant bullet in the Docker-comparison topic"
  - "v7: added 'Resource requests & limits (brief mention)' bullet under \"What is container orchestration?\", per /improve request — kept as an addition rather than replacing the existing declarative-config bullet, to avoid colliding with the dedicated Configuration Management section"
  - "v8: assigned a stable <nr>-<section> folder slug to each top-level section as an HTML comment under its `#` heading, per TASKS.md 1.3, for use as the Phase 2 folder name; marked 'Further Reading / Links' as excluded (not a lesson module)"
---

# What is Kubernetes and Why Should I Care?
<!-- folder: 01-introduction -->

## What is container orchestration?

- Automated scheduling & placement
- Desired-state reconciliation
- Self-healing / auto-restart of failed containers
- Horizontal & vertical scaling
- Rolling updates without downtime
- Declarative configuration via manifests
- Resource requests & limits (brief mention)

## How is Kubernetes different from plain Docker?

- Single host vs. multi-node cluster
- Manual `docker run`/`compose` vs. declarative manifests
- No built-in scheduling in plain Docker
- No built-in self-healing in plain Docker
- No cross-host service discovery/networking in Docker Compose
- When plain Docker is still sufficient

## What are the key benefits of using Kubernetes?

- Scalability
- Self-healing
- High availability
- Portability
- Resource efficiency
- Extensibility via API & ecosystem

# Kubernetes Architecture
<!-- folder: 02-architecture -->

## What is a cluster, and what is a node?

- Cluster = set of nodes
- Control plane vs. worker roles
- Single-node vs. multi-node clusters
- Node = physical or virtual machine
- Cluster-wide vs. per-node resources
- How Docker Desktop's single-node cluster maps to this model

## What is the difference between the control plane and worker nodes?

- Control plane: cluster-wide decisions
- Worker nodes: run application containers
- Control plane can be single or multi-instance (HA)
- Node roles are labeled, not physically distinct
- Communication direction: API Server as central hub
- Failure impact: control plane vs. worker node outage

## What components make up the control plane?

- API Server
- Scheduler
- Controller Manager
- etcd
- Cloud Controller Manager (brief mention)
- All components communicate through the API Server

## What components run on a worker node?

- kubelet
- kube-proxy
- Container runtime (containerd, CRI-O, etc.)
- Container Runtime Interface (CRI) concept
- kubelet reports node-level resource status to the API Server
- kubelet manages Pod lifecycle on the node

# Pods & Namespaces
<!-- folder: 03-pods-and-namespaces -->

## What is a Pod?

- Smallest deployable unit
- Single- vs. multi-container pods
- Shared network namespace (localhost between containers)
- Shared storage volumes within a pod
- Pod lifecycle & phases
- Ephemeral nature (pods are not durable identities)
- Each Pod gets its own (ephemeral) cluster-internal IP address

## What are labels and selectors?

- Key/value metadata on objects
- Used by Deployments & Services to match pods
- Arbitrary vs. well-known labels
- Selector expressions (equality vs. set-based)
- Labels vs. annotations
- Common labeling conventions (app, version, environment)

## What is a Namespace?

- Logical partitioning of a cluster
- Environment separation (dev/staging/prod)
- Namespace-scoped vs. cluster-scoped resources
- Default namespace
- Resource quotas per namespace (brief mention)
- Naming & switching context with `kubectl`

# `kubectl` — CLI for Kubernetes
<!-- folder: 04-kubectl -->

## How do I interact with a cluster using `kubectl`?

- cluster-info, namespaces, pods, logs, events
- Context & namespace switching
- `kubectl get` / `describe` / `logs` verbs
- `kubectl apply -f` / `create` / `delete` — creating and updating resources from manifests
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
<!-- folder: 05-deployments -->

## What is a Deployment, and how does it relate to a ReplicaSet?

- Deployment manages a ReplicaSet
- Declarative desired-state for Pods
- ReplicaSet ensures pod count matches spec
- Deployment adds versioned rollout history
- Relationship: Deployment → ReplicaSet → Pods
- When to use a bare ReplicaSet vs. a Deployment

## How does Kubernetes scale and self-heal Pods?

- Scaling replica count
- Automatic pod replacement on failure
- Horizontal scaling via `kubectl scale`
- Readiness affects traffic routing
- Liveness probes trigger restarts (brief mention)
- Manual vs. automatic (HPA) scaling (brief mention)

## How do rolling updates and rollbacks work?

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
<!-- folder: 06-services-and-networking -->

## What is a Service?

- Stable virtual IP/DNS name
- Load balancing across matching pods
- Decoupling consumers from pod IP churn
- Service discovery via DNS
- Selector-based endpoint matching
- Headless services (brief mention)

## What types of Services are there?

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName (brief mention)
- Default type behavior
- When to choose which type

## How do I expose a Service outside the cluster?

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
<!-- folder: 07-configuration-management -->

## What is a ConfigMap?

- Externalized non-sensitive configuration
- Env vars vs. mounted files
- Updating a ConfigMap without rebuilding images
- ConfigMap as command-line args source
- Immutable ConfigMaps (brief mention)
- Referencing a ConfigMap in a Pod spec

## What is a Secret, and how does it differ from a ConfigMap?

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
<!-- folder: 08-access-control -->

## What is RBAC (Role-Based Access Control)?

- Roles / RoleBindings
- ClusterRoles / ClusterRoleBindings
- Subjects (users, groups, service accounts)
- Verbs & resources in a Role rule
- Namespace-scoped vs. cluster-scoped permissions
- Principle of least privilege

## What is a Service Account?

- Pod identity toward the API server
- Default vs. custom service accounts
- Automatic token mounting
- Binding a Role to a Service Account
- Use cases: CI/CD, Operators, in-cluster tooling
- Disabling auto-mount for security

# Storage & State
<!-- folder: 09-storage-and-state -->

## How does Kubernetes handle persistent storage?

- Volumes
- PersistentVolume / PersistentVolumeClaim
- StorageClass & dynamic provisioning (brief mention)
- Access modes (ReadWriteOnce, ReadWriteMany, etc.)
- Volume lifecycle vs. pod lifecycle
- emptyDir vs. persistent volumes
- Docker Desktop's default `hostpath` StorageClass (exercise environment)

## What is a StatefulSet?

- Stable per-replica identity
- Ordered deployment & scaling
- Stable network identity per replica
- Stable storage per replica (via volumeClaimTemplates)
- Ordered, graceful termination
- Use cases: databases, distributed systems

# Workload Patterns
<!-- folder: 10-workload-patterns -->

## What is a DaemonSet?

- One pod per (selected) node
- Use case: log/monitoring agents
- Node selectors/affinity for targeting
- Automatic scheduling on new nodes
- Comparison to Deployment (no fixed replica count)
- Update strategies for DaemonSets

## What is an Init Container?

- Run-to-completion before app containers
- Use case: setup/dependency waits
- Sequential execution order
- Separate image/resource profile from app container
- Failure handling (pod restart on init failure)
- Common patterns: schema migration, config generation

## What is a Sidecar Container?

- Auxiliary container in the same pod
- Use case: proxies, log shippers
- Shared network & volume with the main container
- Lifecycle coupling with the main container
- Native sidecar support (restartPolicy on init containers, brief mention)
- Examples: service mesh proxies, log forwarders

## What is an Operator?

- Custom controller + CRD
- Automates day-2 operational tasks
- Reconciliation loop pattern
- Encoding operational knowledge as code
- Examples: database operators, certificate operators
- Operator Framework / OperatorHub (brief mention)

# CI/CD with Kubernetes
<!-- folder: 11-ci-cd -->

## What is GitOps?

- Git as source of truth
- Automated sync/reconciliation (conceptual)
- Pull-based vs. push-based deployment
- Declarative desired state stored in Git
- Drift detection & auto-correction
- Auditability via commit history
- Examples: Argo CD, Flux (brief mention)

## How does a deployment pipeline work with Kubernetes?

- Build → test → package → deploy
- Environment promotion (dev → staging → prod)
- Image tagging & versioning strategy
- Automated rollout triggers
- Rollback as part of the pipeline
- Separation of CI (build/test) and CD (deploy) concerns

# Package Management: Helm & Kustomize
<!-- folder: 12-package-management -->

## What is Helm?

- Package manager ("charts") for Kubernetes
- Install/upgrade/rollback as a unit
- Templating with values files
- Chart repositories
- Release versioning & history
- Managing multi-resource applications as one unit

## What is Kustomize?

- Overlay-based YAML customization
- Built into `kubectl -k`
- Base + overlay pattern
- Patches vs. templating (Kustomize vs. Helm)
- Environment-specific overlays (dev/staging/prod)
- No templating language required

# Service Mesh
<!-- folder: 13-service-mesh -->

## What is a service mesh, and why would I need one?

- Service-to-service traffic layer (routing, retries, mTLS)
- Examples: Istio, Traefik Mesh
- Sidecar proxy pattern
- Observability (traffic metrics, tracing)
- Traffic splitting / canary routing
- When a service mesh is (not) needed

# Further Reading / Links
<!-- no folder: reference links only, not a lesson module -->

- [What is Kubernetes? An Introduction With Examples](https://www.datacamp.com/blog/what-is-kubernetes)
- [Kubernetes: An Introduction for Beginners](https://tecadmin.net/kubernetes-introduction/)
- [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)
- [kubectl cheatsheet](https://kubernetes.io/de/docs/reference/kubectl/cheatsheet/)
