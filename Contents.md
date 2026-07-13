---
revision: 37
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
  - "v9: fill-subtopic 02.02 — added 7 subjects to What is Kubernetes."
  - "v10: fill-subtopic 03.01 — added 7 subjects to Overview."
  - "v11: fill-subtopic 03.02 — added 6 subjects to Control Plane."
  - "v12: fill-subtopic 03.03 — added 6 subjects to Worker Nodes."
  - "v13: fill-subtopic 03.04 — added 6 subjects to Networking."
  - "v14: fill-subtopic 03.05 — added 6 subjects to Data Storage."
  - "v15: fill-subtopic 04.01 — added 7 subjects to Pods + Container (Runtime)."
  - "v16: fill-subtopic 04.02 — added 6 subjects to Services."
  - "v17: fill-subtopic 04.03 — added 6 subjects to Namespaces."
  - "v18: fill-subtopic 05.01 — added 6 subjects to Why not just pods?"
  - "v19: fill-subtopic 05.02 — added 6 subjects to Deployment Types."
  - "v20: fill-subtopic 05.03 — added 6 subjects to Replicas."
  - "v21: fill-subtopic 05.04 — added 7 subjects to Deployments Overview."
  - "v22: fill-subtopic 06.01 — added 6 subjects to kube-proxy."
  - "v23: fill-subtopic 06.02 — added 7 subjects to Labels and Selectors."
  - "v24: fill-subtopic 06.03 — added 6 subjects to NodePort / Ingress / Gateway."
  - "v25: fill-subtopic 06.04 — added 6 subjects to LoadBalancer."
  - "v26: fill-subtopic 07.01 — added 7 subjects to ConfigMaps."
  - "v27: fill-subtopic 07.02 — added 7 subjects to Secrets."
  - "v28: fill-subtopic 08.01 — added 7 subjects to Rights Management."
  - "v29: fill-subtopic 08.02 — added 7 subjects to Service Accounts."
  - "v30: fill-subtopic 08.03 — added 7 subjects to Persistence."
  - "v31: fill-subtopic 08.04 — added 7 subjects to StatefulSet."
  - "v32: fill-subtopic 08.05 — added 6 subjects to DaemonSet."
  - "v33: fill-subtopic 08.06 — added 6 subjects to Init Containers."
  - "v34: fill-subtopic 08.07 — added 6 subjects to Sidecar."
  - "v35: fill-subtopic 08.08 — added 6 subjects to Operators."
  - "v36: fill-subtopic 09.01 — added 7 subjects to Helm."
  - "v37: fill-subtopic 09.02 — added 7 subjects to Kustomize."
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

- Kubernetes as a production-grade, open-source container orchestration system — automating deployment, scaling, and lifecycle management of containerized applications across a cluster
- Kubernetes origin: designed at Google based on lessons from internal systems (Borg/Omega), open-sourced in 2014, now a CNCF project with broad adoption across cloud providers and on-premises environments
- Declarative configuration: workloads are described as desired state in YAML manifests; Kubernetes continuously reconciles the actual cluster state toward what is declared
- Self-healing: Kubernetes automatically restarts crashed containers, reschedules pods from failed nodes, and replaces unresponsive instances without manual intervention
- Built-in scaling and rolling updates: Kubernetes manages replica counts and applies configuration changes progressively without downtime, rolling back automatically on failure
- Kubernetes cluster model at a glance: a Control Plane manages scheduling and cluster state; Worker Nodes run the actual containerized workloads (architecture covered in depth in Topic 03)
- Portability across environments: the same workload manifests run on a local Docker Desktop cluster, on-premises, or any major cloud provider — no vendor lock-in

------------------------------------------------------------------------------

# 03 Kubernetes Architecture

## [03.01 Overview](<Contents/03-Kubernetes Architecture/03.01-Overview.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.01-Overview.lesson.md -->

- Kubernetes cluster as the top-level operational unit: a set of machines (nodes) forming a single coordinated system under a shared control layer
- Two-tier architecture: a Control Plane layer responsible for cluster-wide decisions and a Worker Node layer responsible for running containerized workloads — each covered in detail in the following subtopics
- API Server as the cluster's unified communication hub: all interactions — from kubectl, controllers, and kubelets — flow exclusively through the API Server, making it the central gateway for every read and write
- Controllers and the reconciliation loop: dedicated control loops watch for state changes via the API Server and continuously drive actual cluster state toward the declared desired state — this is how self-healing is implemented
- Kubernetes API objects (Pods, Deployments, Services, ConfigMaps, …) as the typed, versioned resources through which users and controllers express and observe workload intent
- Kubernetes as an extensible platform: the core API provides building blocks that higher-level tooling (Helm, Kustomize, Operators) extends — covered in later Topics
- Single-node cluster for local development (Docker Desktop / Rancher Desktop): Control Plane and Worker Node roles coexist on one machine, providing the same architectural model at a simplified scale

## [03.02 Control Plane](<Contents/03-Kubernetes Architecture/03.02-Control Plane.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.02-Control Plane.lesson.md -->

- API Server (kube-apiserver): the RESTful HTTP gateway exposing the Kubernetes API — validates and authenticates requests, enforces authorization, applies admission plugins, and persists accepted objects to etcd
- etcd: the distributed, consistent key-value store holding authoritative cluster state; only the API Server reads from and writes to etcd — all other components interact with state exclusively through the API Server
- Scheduler (kube-scheduler): watches for newly created Pods without an assigned node and selects the most suitable Worker Node based on resource requests, available capacity, and placement constraints
- Controller Manager (kube-controller-manager): runs the built-in control loops — ReplicaSet, Deployment, Node, Namespace, and others — each reacting to API object changes and reconciling actual state toward desired state
- Watch-based communication: Control Plane components register watches on the API Server rather than polling; object changes trigger immediate event notifications, enabling responsive, low-latency reconciliation
- Control Plane does not schedule user workloads: in production, Control Plane components run on dedicated nodes; system components appear in the `kube-system` namespace, separate from user workloads

## [03.03 Worker Nodes](<Contents/03-Kubernetes Architecture/03.03-Worker Nodes.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.03-Worker Nodes.lesson.md -->

- kubelet: the primary node agent on every Worker Node — watches the API Server for Pod specs assigned to its node and ensures the declared containers are running and healthy
- Container Runtime Interface (CRI): the standard abstraction through which the kubelet delegates container lifecycle operations (image pull, create, start, stop, status) to the underlying runtime (e.g., containerd)
- kube-proxy: runs on each Worker Node and maintains node-level network routing rules that implement the Service abstraction, directing traffic to the correct Pod endpoints (details in Topic 06)
- Node registration and health reporting: on startup the kubelet registers the node with the API Server, advertises its available CPU and memory capacity, and continuously reports node conditions (Ready, DiskPressure, MemoryPressure)
- Pod execution flow on a Worker Node: the Scheduler assigns a Pod → the kubelet picks up the spec from the API Server → instructs the container runtime via CRI → monitors container health and reports status back
- Node resource enforcement: the kubelet enforces container resource limits using Linux cgroups, ensuring workloads on the same node respect their declared resource requests and do not starve each other

## [03.04 Networking](<Contents/03-Kubernetes Architecture/03.04-Networking.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.04-Networking.lesson.md -->

- Flat Pod network model: every Pod receives a unique cluster-wide IP address and can communicate directly with any other Pod across nodes without Network Address Translation (NAT)
- Container Network Interface (CNI): a plugin specification through which Kubernetes delegates the setup of Pod networking on each node; CNI plugins (Calico, Flannel, Cilium) implement the flat network model — automatically configured in Docker Desktop / Rancher Desktop
- CoreDNS: the cluster's internal DNS server running in `kube-system`, allowing Pods and Services to be discovered by name rather than by IP address
- Pod IP ephemerality: Pod IPs are assigned at creation and released on deletion; because Pod IPs change constantly, Services provide stable virtual IPs and DNS names as the durable addressing layer (details in Topics 04 and 06)
- Cluster network vs. external network: the Pod network is internal to the cluster and isolated from the outside world by default; NodePort, LoadBalancer, and Ingress Service types bridge that boundary (details in Topic 06)
- NetworkPolicy: Kubernetes objects that define allow/deny rules for Pod-to-Pod and Pod-to-namespace traffic — the architectural hook for in-cluster access control (production use is beyond the mandatory workshop scope)

## [03.05 Data Storage](<Contents/03-Kubernetes Architecture/03.05-Data Storage.lesson.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.05-Data Storage.lesson.md -->

- Container filesystem ephemerality: a container's writable layer is discarded when it exits — data written inside a container does not survive Pod termination by default
- Volumes: the Kubernetes mechanism for attaching storage to a Pod; all containers in the Pod share the mounted volume and writes to it are visible across them
- Ephemeral volumes (e.g., emptyDir): storage that exists only for the Pod's lifetime — useful for scratch space and data exchange between containers in the same Pod, not for durable persistence
- PersistentVolumes (PV) and PersistentVolumeClaims (PVC): the two-resource model decoupling storage provisioning from consumption — cluster admins (or dynamic provisioners) create PVs; workloads request storage via PVCs (deeper treatment in Topic 08)
- Storage Classes: a Kubernetes object that describes a storage type and its provisioner, enabling on-demand PVC fulfillment without manually pre-creating PVs — infrastructure-specific provisioner details are out of scope for this workshop
- Stateful workloads and durable storage: unlike Deployments, StatefulSets assign each replica a dedicated PVC that persists across Pod restarts — the architectural link between persistent storage and stateful application patterns (details in Topic 08)

------------------------------------------------------------------------------

# 04 Key Concepts

## [04.01 Pods + Container (Runtime)](<Contents/04-Key Concepts/04.01-Pods + Container (Runtime).lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.01-Pods + Container (Runtime).lesson.md -->

- Pod as the smallest schedulable and deployable unit in Kubernetes — the platform schedules Pods, not individual containers; a Pod always runs as a whole on a single node
- Shared context within a Pod: all containers in the same Pod share one network namespace (same cluster IP, same localhost, same port space), the same hostname, and any volumes mounted to the Pod
- Single-container Pod as the common case: most Pods run exactly one application container; the Pod provides that container with its cluster identity, IP address, and resource scope
- Multi-container Pods for tightly coupled helpers: containers in the same Pod are always co-located and co-scheduled — used for sidecar, ambassador, and adapter patterns that extend or support the main container (details in Topic 08)
- Pod specification in YAML: declares containers with their images, resource requests and limits, environment variables, volume mounts, and restart policy — the declarative description Kubernetes acts on
- Pod lifecycle phases: Pending (awaiting scheduling or image pull), Running (at least one container active), Succeeded / Failed (all containers exited), Unknown — phases reported by the kubelet to the API Server
- Pods are not self-healing on their own: a terminated or evicted Pod is not automatically replaced unless managed by a higher-level controller such as a Deployment or ReplicaSet — the reason bare Pods are rarely used in practice (details in Topic 05)

## [04.02 Services](<Contents/04-Key Concepts/04.02-Services.lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.02-Services.lesson.md -->

- Service as a stable, long-lived API object that decouples clients from ephemeral Pod IPs — clients address the Service; Kubernetes routes traffic to whichever Pods are currently healthy and backing it
- Load-balancing across Pod backends: a Service distributes incoming connections across all healthy Pods matching its label selector, transparently absorbing Pod replacements and restarts
- Label-based Pod selection: a Service's selector defines which Pods it targets — any Pod with matching labels is automatically included in the backend pool (label syntax and mechanics covered in Topic 06)
- ClusterIP as the default Service type: assigns a stable internal virtual IP reachable only within the cluster; other types (NodePort, LoadBalancer, Ingress) extend this to expose workloads externally (details in Topic 06)
- Automatic DNS name: every Service receives a fully qualified cluster-internal hostname (`<service-name>.<namespace>.svc.cluster.local`), enabling name-based discovery without hardcoding IP addresses
- Services as the recommended pattern for inter-Pod communication: workloads address each other through Service names rather than direct Pod IPs, ensuring resilience to Pod churn and seamless scaling

## [04.03 Namespaces](<Contents/04-Key Concepts/04.03-Namespaces.lesson.md>)
<!-- lesson: Contents/04-Key Concepts/04.03-Namespaces.lesson.md -->

- Namespace as a virtual partition within a cluster: groups related Kubernetes objects (Pods, Services, Deployments, ConfigMaps, …) under a shared name scope, enabling multi-team or multi-environment use of a single cluster
- Default namespaces: `default` (user workloads when no namespace is specified), `kube-system` (Kubernetes system components), `kube-public` (cluster-wide publicly readable data), `kube-node-lease` (node heartbeat leases)
- Name uniqueness is scoped per namespace: two objects of the same type can share a name if they reside in different namespaces — enabling separate dev, staging, and production environments on a single cluster without naming conflicts
- Namespace-scoped vs. cluster-scoped resources: most objects (Pods, Services, Deployments, ConfigMaps) are namespace-scoped; some (Nodes, PersistentVolumes, Namespaces themselves) are cluster-scoped and not tied to any namespace
- Cross-namespace Service access: within the same namespace a Service is reachable by its short name; from a different namespace the `<service>.<namespace>` segment is required — but namespaces do not block inter-namespace network traffic by default (NetworkPolicy handles that)
- Namespaces as the administrative scope for RBAC permissions and resource quotas: operators can grant role-based access rights and constrain CPU/memory/object-count limits per namespace, making namespaces the primary multi-tenancy building block (details in Topic 08)

------------------------------------------------------------------------------

# 05 Deployment

## [05.01 Why not just pods?](<Contents/05-Deployment/05.01-Why not just pods?.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.01-Why not just pods?.lesson.md -->

- Bare Pods have no self-healing: when a Pod terminates due to a crash, node failure, or eviction it is permanently lost — Kubernetes does not restart or reschedule it without an owning controller
- No built-in redundancy: a standalone Pod is a single point of failure; there is no native way to maintain multiple identical Pods running in parallel without a managing controller
- Manual scaling is impractical: adding or removing capacity means creating or deleting individual Pod objects one at a time — bare Pods have no concept of a desired replica count
- No managed update strategy: updating a bare Pod's container image requires deleting the old Pod and creating a new one manually, with no staged rollout, traffic continuity, or automatic rollback
- Pods are named individuals, not fleet members: each Pod has a unique fixed name; you cannot ask Kubernetes to "run N copies of this Pod" — only a controller wrapping a Pod template provides that fleet abstraction
- Higher-level controllers (ReplicaSet, Deployment, and others) solve these limitations by wrapping a Pod template with reconciliation logic for replica count, automatic replacement, and rolling updates — covered in the following subtopics

## [05.02 Deployment Types](<Contents/05-Deployment/05.02-Deployment Types.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.02-Deployment Types.lesson.md -->

- Deployment: the standard controller for stateless applications — manages a ReplicaSet under the hood, supports a declarative replica count, rolling updates, and rollbacks; the go-to type for most application workloads
- ReplicaSet: ensures a specified number of identical Pod replicas are always running and automatically replaces failed Pods — typically created and owned by a Deployment rather than used directly
- Job: runs one or more Pods to successful completion rather than keeping them running continuously — for batch processing, data migrations, and one-off tasks
- CronJob: schedules Jobs on a recurring cron-like schedule — for periodic tasks such as report generation, database backups, or cleanup routines
- StatefulSet: manages stateful applications requiring stable network identities and per-replica persistent storage (e.g., databases) — each replica gets a predictable hostname and a dedicated PVC (details in Topic 08)
- DaemonSet: ensures exactly one Pod runs on every node in the cluster — used for node-level infrastructure agents such as log collectors or monitoring daemons (details in Topic 08)

## [05.03 Replicas](<Contents/05-Deployment/05.03-Replicas.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.03-Replicas.lesson.md -->

- Replica count as desired state: declaring `replicas: N` in a Deployment or ReplicaSet spec instructs the controller to maintain exactly N running Pod instances at all times
- ReplicaSet controller as the replica enforcer: continuously watches the actual Pod count against the declared desired count and creates or terminates Pods to close any gap
- Pod template as the replica blueprint: all replicas in a ReplicaSet are created from the same Pod template (same container image, environment variables, resource requests) — making all replicas identical and interchangeable
- Horizontal scaling in practice: the replica count can be changed by editing the spec or via `kubectl scale deployment <name> --replicas=N`; the controller immediately reconciles toward the new target
- Scheduler distribution across nodes: replica Pods are scheduled independently; the Scheduler may place them on different nodes, providing natural availability redundancy if a node fails
- Replicas suit stateless workloads: horizontal scaling by replica count works well when all instances are equivalent and share no local state; stateful workloads requiring per-instance identity or storage are handled by StatefulSet instead (details in Topic 08)

## [05.04 Deployments Overview](<Contents/05-Deployment/05.04-Deployments Overview.lesson.md>)
<!-- lesson: Contents/05-Deployment/05.04-Deployments Overview.lesson.md -->

- Deployment as the production-standard workload object: adds declarative image updates, rollout control, and automatic rollback on top of ReplicaSet's replica management
- Deployment update flow: changing the container image (or any Pod template field) triggers creation of a new ReplicaSet for the updated Pods while the old ReplicaSet is gradually scaled down — keeping the rollout auditable and reversible
- RollingUpdate strategy (default): new Pod versions are introduced incrementally; `maxUnavailable` and `maxSurge` parameters control how many Pods may be down or extra at any point during the rollout
- Recreate strategy: terminates all old Pods before starting any new ones — causes a brief downtime but avoids running two versions simultaneously, suitable for breaking schema changes
- Readiness probes as rollout gates: a new Pod counts as available only once its readiness probe passes; a persistently failing probe stalls the rollout, preventing a broken update from fully replacing healthy Pods
- Rollback: `kubectl rollout undo deployment/<name>` reverts to the previous revision; Kubernetes retains a configurable number of prior ReplicaSets as rollback history (`revisionHistoryLimit`)
- Monitoring rollouts: `kubectl rollout status deployment/<name>` reports progress in real time, showing whether a rollout is progressing, stalled, or complete — useful for CI/CD pipelines and manual verification

------------------------------------------------------------------------------

# 06 Services & kube-proxy

## [06.01 kube-proxy](<Contents/06-Services & kube-proxy/06.01-kube-proxy.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.01-kube-proxy.lesson.md -->

- kube-proxy as the Service-to-Pod traffic translator: runs as a DaemonSet on every node, watches the API Server for Service and Endpoint changes, and translates them into node-local network rules that redirect traffic addressed to Service IPs toward healthy Pod IPs
- iptables mode (default in kubeadm-based clusters including Docker Desktop): kube-proxy programs Linux iptables NAT rules that intercept packets addressed to a Service ClusterIP and DNAT them to a randomly selected healthy Pod IP
- IPVS mode (alternative): uses Linux Virtual Server for packet routing instead of iptables chains, offering better scalability and additional load-balancing algorithms — preferred for clusters with large numbers of Services
- EndpointSlice objects: Kubernetes tracks the current set of healthy Pod IPs for each Service in EndpointSlice objects; kube-proxy watches these and updates its routing rules immediately as Pods are added, removed, or fail health checks
- ClusterIP exists only in routing rules: the virtual IP of a Service is never assigned to a real network interface — it lives solely as a destination target in kube-proxy's iptables/IPVS rules, which is what makes the virtual IP route to actual Pods
- kube-proxy is not universal: some CNI plugins (e.g. Cilium in eBPF mode) replace kube-proxy entirely by implementing Service routing at the kernel level — in those environments kube-proxy does not run

## [06.02 Labels and Selectors](<Contents/06-Services & kube-proxy/06.02-Labels and Selectors.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.02-Labels and Selectors.lesson.md -->

- Labels as key-value metadata: arbitrary string key-value pairs attached to any Kubernetes object (Pods, Services, Deployments, Nodes, …); user-defined, with no built-in meaning to Kubernetes, but consumed by selectors, tooling, and operators for identification and grouping
- Common labeling conventions: keys like `app`, `environment`, `version`, and `tier` for human organization; the `app.kubernetes.io/*` prefix family for standard, interoperable attribute names (name, version, component, part-of, managed-by)
- Selectors: expressions that match objects whose labels satisfy specified conditions — equality-based (`app=frontend`) and set-based (`env in (staging,prod)`); used by Services and ReplicaSets to determine which Pods belong to them
- How a Service finds its Pods: the Service's `.spec.selector` field declares required label key-value pairs; any Pod in the same namespace whose labels contain all of them is automatically included in the Service's EndpointSlice and starts receiving traffic
- Labels in the Deployment Pod template: the labels defined in `spec.template.metadata.labels` are applied to every Pod the Deployment creates — these must match both the Service's selector and the ReplicaSet's pod selector for end-to-end traffic routing to work
- Annotations: also key-value metadata, but not selectable — designed for machine-readable data (build info, checksums, tool configs, descriptions) that should not be used as a query target; unlike labels, annotations cannot appear in selectors
- Filtering with kubectl: `kubectl get pods -l app=frontend` lists all matching objects; the `-l` flag works across all object types (`kubectl get all -l env=staging`) — an essential command for inspecting and debugging labeled resources

## [06.03 NodePort / Ingress / Gateway](<Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.03-NodePort - Ingress - Gateway.lesson.md -->

- NodePort: exposes a Service on a static port (30000–32767) on every node's IP address — external traffic reaching `<NodeIP>:<NodePort>` is forwarded by kube-proxy to the Service ClusterIP and then to a matching Pod
- NodePort limitations: exposes a single port across all nodes, requires clients to know a specific node's IP, provides no hostname routing or TLS termination — practical for local development but insufficient for most production use cases
- Ingress: a Kubernetes API object that defines HTTP/HTTPS routing rules (host-based and path-based) from a single external entry point to one or more backend Services, including optional TLS termination — decouples routing configuration from the underlying proxy implementation
- Ingress Controller: a separately deployed component (not part of Kubernetes core) that watches Ingress objects and configures an underlying reverse proxy (nginx, Traefik, HAProxy, …) to enforce the routing rules — must be installed before Ingress objects take effect
- Gateway API: a newer, more expressive Kubernetes API for traffic routing — separates concerns with a role-oriented model (Gateway for infrastructure teams, HTTPRoute/GRPCRoute for application teams) and supports richer traffic policies than Ingress
- Ingress vs. Gateway API: Ingress is widely supported and stable with broad controller ecosystem; Gateway API is more powerful and role-aware but requires a Gateway API-capable controller — the two coexist today, with Gateway API designed as the long-term successor

## [06.04 LoadBalancer](<Contents/06-Services & kube-proxy/06.04-LoadBalancer.lesson.md>)
<!-- lesson: Contents/06-Services & kube-proxy/06.04-LoadBalancer.lesson.md -->

- LoadBalancer Service type: requests an externally accessible IP from the underlying infrastructure; external traffic to that IP is forwarded to the Service's ClusterIP and then routed to healthy matching Pods
- Built on top of NodePort: a LoadBalancer Service also creates a NodePort internally — the provisioned load balancer routes to those NodePorts on cluster nodes; LoadBalancer adds the automatically managed external entry point on top
- Automatic provisioning in managed environments: in cloud-hosted or on-premises clusters with a load balancer controller installed, creating a LoadBalancer Service triggers automatic provisioning of an external load balancer and assignment of an external IP — infrastructure-specific details vary by environment
- Behavior in local clusters (Docker Desktop / Rancher Desktop): Docker Desktop natively supports LoadBalancer Services and assigns `localhost` as the external address, making Services accessible from the host machine without additional tooling during local development
- One external IP per Service: each LoadBalancer Service receives its own dedicated external IP — simple and direct, but in cloud environments each provisioned load balancer typically incurs cost; Ingress can serve multiple HTTP/HTTPS Services through a single shared entry point
- When to choose LoadBalancer vs. Ingress: LoadBalancer suits non-HTTP protocols (TCP, UDP) or cases requiring a dedicated external IP per Service; Ingress is preferred for HTTP/HTTPS workloads where multiple Services share one external entry point and hostname-based routing is needed

------------------------------------------------------------------------------

# 07 Configuration

## [07.01 ConfigMaps](<Contents/07-Configuration/07.01-ConfigMaps.lesson.md>)
<!-- lesson: Contents/07-Configuration/07.01-ConfigMaps.lesson.md -->

- ConfigMap as a namespace-scoped API object storing non-confidential key-value pairs or text files — the standard mechanism for externalizing application configuration from container images
- Why separate config from images: keeping environment-specific settings (database URLs, feature flags, log levels) outside the image means the same image can be deployed to dev, staging, and production without rebuilding
- ConfigMap data model: a flat map of string keys to string values or multi-line text blobs — supports arbitrary text, JSON fragments, YAML, properties files, or entire config file content
- Injecting ConfigMap entries as environment variables: individual keys can be projected as named environment variables in a Pod's container spec, making configuration available to the application without filesystem access
- Mounting a ConfigMap as a volume: a ConfigMap (or selected keys) can be mounted into a container as a directory of files — each key becomes a filename and its value becomes the file content; useful for applications that read config from disk
- Dynamic updates for volume-mounted ConfigMaps: when a ConfigMap is updated, mounted files are refreshed automatically (with a short propagation delay) without a Pod restart — environment-variable injections are static and require a Pod restart to pick up changes
- Creating ConfigMaps: via `kubectl create configmap` from literal values or from files, or by applying a YAML manifest with `kubectl apply` — declarative YAML is preferred for version-controlled, reproducible configuration

## [07.02 Secrets](<Contents/07-Configuration/07.02-Secrets.lesson.md>)
<!-- lesson: Contents/07-Configuration/07.02-Secrets.lesson.md -->

- Secret as a namespace-scoped API object for sensitive data (passwords, API tokens, TLS certificates, SSH keys) — the counterpart to ConfigMap for confidential configuration that must not appear in container images or plain environment files
- Base64 encoding is NOT encryption: Secret values are stored base64-encoded in etcd, which is a reversible transformation; without additional encryption-at-rest configuration a user with etcd access can recover the plain values — Secrets provide separation of concern, not cryptographic protection by default
- Injecting Secrets as environment variables: individual Secret keys can be projected as named environment variables in the Pod spec — the same mechanism as ConfigMap env injection, but values are decoded from base64 before being placed in the container environment
- Mounting Secrets as volumes: a Secret can be mounted as a directory of files in a container, with each key decoded to a file — the preferred injection method for TLS certificates, SSH keys, and other file-based credentials that applications expect to read from disk
- Built-in Secret types: `Opaque` (generic key-value), `kubernetes.io/tls` (TLS certificate + key), `kubernetes.io/dockerconfigjson` (registry pull credentials), `kubernetes.io/service-account-token` (automatically created for ServiceAccounts)
- Access control for Secrets: RBAC policies should restrict which workloads and users can read Secrets in a namespace; by default any Pod in the namespace can reference any Secret — securing access is covered in Topic 08
- Creating Secrets safely: via `kubectl create secret generic` or `kubectl create secret tls` from literals or files; embedding base64 Secret values in version-controlled YAML manifests exposes them — tools like Sealed Secrets or external secret managers address this in production

------------------------------------------------------------------------------

# 08 Advanced Concepts

## [08.01 Rights Management](<Contents/08-Advanced Concepts/08.01-Rights Management.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.01-Rights Management.lesson.md -->

- RBAC (Role-Based Access Control): the Kubernetes authorization model controlling which subjects can perform which actions on which resources — the API Server denies all requests not explicitly permitted by an active RBAC binding
- Role and ClusterRole: a Role defines a set of permissions scoped to a single namespace; a ClusterRole defines equivalent permissions at cluster scope and can also grant access to cluster-scoped resources (Nodes, PersistentVolumes, Namespaces)
- RoleBinding and ClusterRoleBinding: a RoleBinding grants the permissions of a Role (or ClusterRole) to one or more subjects within a namespace; a ClusterRoleBinding grants a ClusterRole's permissions cluster-wide regardless of namespace
- Subjects: the three entity types that receive permissions — User (external identity from an identity provider), Group (a set of users), and ServiceAccount (an in-cluster identity used by Pods and controllers)
- Verbs and resources: RBAC rules combine resource types (pods, secrets, configmaps, deployments, …) with verbs (get, list, watch, create, update, patch, delete) — granular combinations allow expressing least-privilege access policies
- Deny-by-default: RBAC is strictly deny-unless-explicitly-allowed; a request is permitted only when a matching RoleBinding or ClusterRoleBinding grants the required verb on the target resource for the requesting subject
- Inspecting and debugging RBAC: `kubectl auth can-i <verb> <resource>` checks whether the current identity has a given permission; `kubectl get roles,rolebindings -n <namespace>` and `kubectl describe clusterrolebinding` enumerate active policies

## [08.02 Service Accounts](<Contents/08-Advanced Concepts/08.02-Service Accounts.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.02-Service Accounts.lesson.md -->

- ServiceAccount as the in-cluster identity for Pods: a namespace-scoped API object that gives a Pod an identity it can present when authenticating to the Kubernetes API — distinct from user identities, which are managed externally
- Default ServiceAccount: every namespace contains a ServiceAccount named `default`; Pods that do not specify a `serviceAccountName` are automatically assigned this account and inherit its permissions
- Automatic token mounting: Kubernetes projects a signed, time-limited JWT token into every Pod at `/var/run/secrets/kubernetes.io/serviceaccount/token`; the kubelet rotates the token before expiry — Pods use this token to authenticate API requests without managing credentials manually
- Least-privilege ServiceAccounts: the default ServiceAccount has minimal API permissions; workloads that need API access (controllers, CI/CD agents, monitoring tools) should use a dedicated ServiceAccount with only the required RBAC roles bound to it
- Binding RBAC roles to a ServiceAccount: a RoleBinding (or ClusterRoleBinding) that names a ServiceAccount as subject grants all Pods running as that account the corresponding API permissions — the mechanism that enables in-cluster operators and automation to manage cluster resources
- Disabling automatic token mounting: setting `automountServiceAccountToken: false` in the Pod spec (or on the ServiceAccount itself) prevents the token from being projected into the container — recommended for Pods with no reason to call the Kubernetes API, reducing the attack surface
- ImagePullSecrets via ServiceAccount: a ServiceAccount can carry `imagePullSecrets` references so that all Pods using that account automatically inherit container registry pull credentials, avoiding repeated per-Pod Secret references

## [08.03 Persistence](<Contents/08-Advanced Concepts/08.03-Persistence.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.03-Persistence.lesson.md -->

- PersistentVolume (PV) provisioning modes: static provisioning (an admin pre-creates PVs pointing to specific storage) vs. dynamic provisioning (a StorageClass provisioner creates a PV automatically when a matching PVC is submitted)
- PersistentVolumeClaim (PVC) binding: a PVC declares required capacity, access mode, and an optional StorageClass name; the cluster binds it to a compatible available PV or dynamically provisions one if a StorageClass is specified
- Access modes: ReadWriteOnce (RWO — one node mounts read/write), ReadOnlyMany (ROX — multiple nodes read-only), ReadWriteMany (RWX — multiple nodes read/write); not all backends support all modes — the right choice depends on the workload topology
- Volume reclaim policy: controls what happens to a PV when its PVC is deleted — `Retain` preserves the PV and data for manual recovery; `Delete` removes both the PV object and the underlying storage resource; `Recycle` is deprecated
- Mounting a PVC in a Pod: the PVC is declared under `spec.volumes` with a reference to the claim name; individual containers reference it in `spec.containers[].volumeMounts` — the container sees a directory backed by the persistent storage
- StatefulSet volumeClaimTemplates: a StatefulSet's `volumeClaimTemplates` field causes Kubernetes to create a dedicated PVC for each replica automatically; those PVCs persist across Pod restarts and rescheduling, giving each replica stable, independent durable storage
- Default StorageClass and dynamic provisioning in the workshop environment: Rancher Desktop bundles a local-path provisioner set as the default StorageClass — unqualified PVCs (no StorageClass specified) are automatically fulfilled by it, making dynamic provisioning available out of the box for local development

## [08.04 StatefulSet](<Contents/08-Advanced Concepts/08.04-StatefulSet.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.04-StatefulSet.lesson.md -->

- StatefulSet as the controller for stateful applications whose replicas are NOT interchangeable: each instance holds unique state and requires a stable identity (name, network, storage) that persists across restarts — unlike Deployment replicas, which are fungible and carry no individual identity
- Stable ordinal naming: StatefulSet Pods are named `<statefulset-name>-0`, `<statefulset-name>-1`, … — the ordinal suffix is deterministic and preserved across Pod restarts, rescheduling, and node failures, so a crashed Pod 0 always restarts as Pod 0 with the same name
- Headless Service and per-Pod DNS: a StatefulSet requires a companion headless Service (`clusterIP: None`, referenced in `spec.serviceName`); Kubernetes registers a stable DNS A-record for each Pod — `<pod-name>.<headless-service>.<namespace>.svc.cluster.local` — enabling direct inter-replica communication essential for consensus protocols and peer discovery
- Ordered startup and shutdown: Pods are created sequentially — Pod 0 must be Running and Ready before Pod 1 starts, and so on — and are terminated in reverse ordinal order on scale-down; this ordering guarantee is fundamental for clustered applications that bootstrap quorum by contacting lower-ordinal peers
- PVC lifecycle independence from Pods: when a StatefulSet is scaled down or a Pod is deleted, its associated PVC is intentionally NOT garbage collected — data is preserved and the same PVC is reattached when the replica returns; orphaned PVCs must be manually deleted if the data is no longer needed
- Rolling update strategy and the partition parameter: StatefulSet rolling updates proceed from the highest ordinal Pod downward; `updateStrategy.rollingUpdate.partition` specifies a cutoff ordinal — only Pods with ordinal ≥ partition are updated — enabling staged, canary-style promotion where a subset of replicas can be updated and verified before committing the full rollout
- StatefulSet use cases: databases (MySQL, PostgreSQL, MongoDB), distributed message brokers (Kafka, RabbitMQ), consensus coordination systems (ZooKeeper), and search/indexing clusters (Elasticsearch) — workloads where individual instances own distinct data partitions or cluster roles and must be addressable independently

## [08.05 DaemonSet](<Contents/08-Advanced Concepts/08.05-DaemonSet.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.05-DaemonSet.lesson.md -->

- DaemonSet as the controller that ensures exactly one Pod instance runs on every node in the cluster (or a targeted subset): the DaemonSet controller automatically schedules a Pod when a new node joins and terminates it when the node is removed — no manual intervention required
- No declared replica count — node membership drives Pod count: unlike Deployment's `replicas` field, a DaemonSet has no replica target; the number of running Pods equals the number of nodes currently matching the DaemonSet's node selector, scaling automatically as the cluster grows or shrinks
- Targeting a node subset with nodeSelector and node affinity: a DaemonSet can restrict its Pods to nodes matching specific label criteria using `spec.template.spec.nodeSelector` or `nodeAffinity` rules — enabling role-targeted DaemonSets such as "GPU nodes only" or "Linux nodes only"
- Tolerations for tainted nodes: Control Plane nodes and specialized nodes typically carry taints (e.g., `NoSchedule`) to repel user workloads; DaemonSets that must run cluster-wide (kube-proxy, CNI plugin agents) add matching tolerations so their Pods are admitted regardless of those taints — the standard pattern for truly node-universal agents
- Update strategies: `RollingUpdate` (default) replaces DaemonSet Pods one node at a time as the Pod template changes; `OnDelete` delays the update until a Pod is manually deleted, giving operators explicit control over when each node's agent is restarted — important for node-level infrastructure where simultaneous restarts across all nodes would disrupt services
- DaemonSet use cases: node-level log collection agents (Fluentd, Fluent Bit), per-node metrics exporters (Prometheus node-exporter), CNI network plugin daemons (Calico, Cilium), distributed storage drivers, and security/audit agents — any workload whose fleet membership must track cluster node membership exactly

## [08.06 Init Containers](<Contents/08-Advanced Concepts/08.06-Init Containers.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.06-Init Containers.lesson.md -->

- Init containers: containers declared in `spec.initContainers` that run sequentially before any container in `spec.containers` starts — each must exit with code 0 before the next init container begins, and all must succeed before the main application containers are launched
- Sequential execution and ordering guarantee: init containers run in the exact order they are declared, strictly one at a time — unlike app containers, which all start concurrently; this makes init containers the correct mechanism for chaining setup steps that depend on each other
- Separate images for specialized tooling: each init container can use a different image from the app containers — enabling use of tools (database clients, CLI utilities, curl, git) that perform setup work without including those tools in the production image, keeping it lean
- Shared volume as the handoff mechanism: init containers and app containers share the Pod's volumes; the typical pattern is an init container writing rendered configuration, downloaded artifacts, or processed data into an emptyDir volume that the application container then reads on startup
- Init container use cases: waiting for a dependency to become reachable before the app starts (polling a database or external service endpoint), running database schema migrations, cloning a repository, fetching credentials from an external vault, or rendering configuration templates from raw files
- Failure and restart behavior: if an init container exits with a non-zero code, Kubernetes restarts the entire Pod (subject to `restartPolicy`); a persistent failure keeps the Pod in the `Init:CrashLoopBackOff` phase — visible in `kubectl describe pod` — and prevents any app container from ever starting

## [08.07 Sidecar](<Contents/08-Advanced Concepts/08.07-Sidecar.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.07-Sidecar.lesson.md -->

- Sidecar container as a concurrent helper: a sidecar is a container declared in `spec.containers` alongside the main application container — it runs concurrently with the main container throughout the entire Pod lifetime, augmenting or extending the main container's functionality without modifying its image
- Common sidecar patterns: logging/monitoring agent (reads from a shared volume or intercepts log streams to forward them), proxy (handles inbound or outbound network traffic on behalf of the main container, e.g., an Envoy proxy injected by a service mesh), adapter (translates the main container's output format for external consumers), and ambassador (pools or retries outbound connections)
- Leveraging shared Pod context: sidecars communicate with the main container over localhost (shared network namespace) and exchange data via mounted volumes — a log-shipping sidecar, for example, reads log files from a shared emptyDir that the main container writes to
- Separation of concerns as the core rationale: the sidecar pattern keeps the main container image focused on business logic while delegating cross-cutting concerns (log collection, distributed tracing, mTLS, connection pooling) to independently versioned, reusable sidecar containers that can be standardized and rolled out across many services
- Sidecar lifecycle vs. init container lifecycle: unlike init containers (which run before app containers and must exit with code 0), sidecars start alongside the main container and run indefinitely — they are terminated by the kubelet when the Pod is shut down, not by completing a bounded task
- Native sidecar containers (Kubernetes 1.29+): declaring an init container with `restartPolicy: Always` grants it formal sidecar semantics — guaranteed to start before app containers, to restart independently if it crashes, and to outlive app containers during graceful shutdown — a more robust alternative to informal multi-container sidecars when startup ordering or independent restarts matter

## [08.08 Operators](<Contents/08-Advanced Concepts/08.08-Operators.lesson.md>)
<!-- lesson: Contents/08-Advanced Concepts/08.08-Operators.lesson.md -->

- The Operator pattern: a software extension to Kubernetes that implements a custom controller managing a complex application through its entire operational lifecycle — encoding operational knowledge (install, upgrade, backup, failover) as automated reconciliation logic rather than manual runbook steps
- Custom Resource Definitions (CRDs): CRDs extend the Kubernetes API with new, application-specific resource types (e.g., `PostgreSQLCluster`, `KafkaTopic`, `RedisCluster`); once a CRD is installed, users create and manage instances of the custom resource using `kubectl` and YAML manifests, exactly like native objects
- Custom controller reconciliation: an Operator runs a custom controller that watches instances of its CRDs via the API Server and continuously reconciles actual application state toward the declared desired state — the same watch-based reconciliation pattern as built-in controllers (Deployment, ReplicaSet), extended to application-specific operational logic
- Day-2 operations that Operators automate: coordinating application-specific rolling upgrades, scheduling and restoring backups, detecting and recovering from partial failures (e.g., reseeding a dead database replica), and scaling with data rebalancing — ongoing operational tasks that static manifests alone cannot express
- Operators vs. static manifest tooling: Helm and Kustomize (Topic 09) package and template Kubernetes manifests but do not observe or react to application state changes after deployment; an Operator continuously monitors the running application and responds to deviations — the distinction between declarative packaging and continuous operational control
- Operator ecosystem: OperatorHub.io is the community registry listing Operators for common software (Prometheus, PostgreSQL, Kafka, MongoDB, Elasticsearch); the Operator SDK and Kubebuilder are frameworks that scaffold operator projects using Kubernetes controller-runtime, reducing the work of building a new Operator from scratch

------------------------------------------------------------------------------

# 09 Helm and Kustomize

## [09.01 Helm](<Contents/09-Helm and Kustomize/09.01-Helm.lesson.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.01-Helm.lesson.md -->

- Helm as the Kubernetes package manager: bundles Kubernetes manifests and configuration defaults into a reusable, versioned unit called a Chart — enabling consistent, repeatable deployment of a complete application stack (Deployments, Services, ConfigMaps, Ingress, etc.) with a single command
- Chart structure: a Chart is a directory containing `Chart.yaml` (name, version, description metadata), `values.yaml` (default configuration values), and a `templates/` directory of Go-template-parameterized Kubernetes manifests that reference `{{ .Values.xxx }}` to inject values at render time
- Releases: installing a Chart into a cluster creates a named "release" — a Helm-tracked, versioned instance of that Chart with its own configuration; multiple releases of the same Chart can coexist independently (e.g., `myapp-prod` and `myapp-staging`), each with separate values and upgrade histories
- Values and configuration overrides: `values.yaml` provides Chart-wide defaults; users override them per release with `--set key=value` (inline) or `-f custom-values.yaml` (file); overrides are merged with defaults at render time, enabling the same Chart to be deployed consistently or differently across environments
- Core Helm commands: `helm install <release> <chart>` deploys a Chart; `helm upgrade <release> <chart>` updates an existing release (optionally with new values); `helm rollback <release>` reverts to a prior revision; `helm list` shows all installed releases; `helm uninstall <release>` removes a release; `helm get manifest <release>` shows the rendered Kubernetes YAML that Helm applied
- Chart repositories and discovery: Charts are published to repositories; `helm repo add <name> <url>` registers a source; `helm search repo <term>` searches it locally; Artifact Hub (artifacthub.io) is the central public registry for community-maintained Charts (Bitnami, Prometheus community, Jetstack, and many others)
- Helm vs. Kustomize: Helm uses a Go templating engine — Charts are parameterized and require `helm` to render; Kustomize patches plain Kubernetes YAML using overlay layers with no templating engine and is built directly into `kubectl apply -k` — the two tools suit different needs and are sometimes used together (Kustomize covered in 09.02)

## [09.02 Kustomize](<Contents/09-Helm and Kustomize/09.02-Kustomize.lesson.md>)
<!-- lesson: Contents/09-Helm and Kustomize/09.02-Kustomize.lesson.md -->

- Kustomize as a configuration customization tool: generates Kubernetes manifests from plain YAML using a layered overlay approach — no templating engine, no custom DSL, no special syntax added to the YAML; Kustomize manipulates native Kubernetes manifests directly, keeping them readable and applicable without special tooling
- `kustomization.yaml` as the control file: every Kustomize directory contains a `kustomization.yaml` that lists resources, generators, transformers, and patches to apply; the CLI reads this file to determine what to assemble and how to transform it — its presence makes a directory a Kustomize base or overlay
- Bases and overlays: a base directory holds the canonical Kubernetes manifests for an application; overlay directories (e.g., `overlays/dev`, `overlays/prod`) reference the base and add or patch resources for their specific environment — the DRY pattern for managing environment-specific configuration without duplicating base YAML
- Patch types: strategic merge patches apply a partial YAML fragment that is merged into the matching resource (by name and kind), modifying only the specified fields; JSON patches (RFC 6902) make precise, path-based edits (`add`, `replace`, `remove`) — both allow overlays to modify base resources without touching the base files
- Built-in transformers: Kustomize applies cross-cutting transformations to all resources in scope — `namePrefix`/`nameSuffix` append to every resource name, `namespace` sets the namespace uniformly, `commonLabels` and `commonAnnotations` attach metadata across all resources — enabling clean environment differentiation without per-resource manual edits
- `kubectl apply -k` and the standalone `kustomize` CLI: Kustomize is built into `kubectl` since v1.14; `kubectl apply -k <dir>` renders and applies a Kustomize directory in one step; `kubectl kustomize <dir>` (or `kustomize build <dir>`) outputs the rendered YAML without applying — the standalone `kustomize` CLI releases faster and offers additional features
- ConfigMapGenerator and SecretGenerator: `kustomization.yaml` can declare generators that produce ConfigMaps or Secrets from literal values, environment files, or raw files; Kustomize appends a content-hash suffix to the generated resource name (e.g., `my-config-abc12345`) and updates all referencing Pod templates automatically — triggering a rolling restart whenever the content changes
