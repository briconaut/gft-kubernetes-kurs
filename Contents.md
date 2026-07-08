---
revision: 12
path: "Contents.md"
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
  - "v9: added missing `path` frontmatter field per CLAUDE.md styleguide header-completeness check"
  - "v10: added `<!-- lesson: Contents/<nr>-<section>/<nr>-<lesson>.md -->` path comments under each `##` topic heading (per-section local numbering, 01..N), analogous to the `folder:` comments from task 1.3, to fix the Phase 2 lesson-file path per /improve request; `## Practice: ...` headings excluded (Phase 6 uses its own <nr>.<subnr> scheme)"
  - "v11: completed task 2.3 — turned all 32 `##` topic headings into Markdown links to their lesson files, keeping the `lesson:` comments in place; the 4 `## Practice: ...` headings left untouched"
  - "v12: replaced all 197 bullet points under linked topics with links to their own anchor in the corresponding lesson file (reusing the anchors already used in each file's `## Overview`), per /improve request; the 24 bullets under `## Practice: ...` topics were left as plain text (no lesson file to link to)"
---

# What is Kubernetes and Why Should I Care?
<!-- folder: 01-introduction -->

## [What is container orchestration?](Contents/01-introduction/01-container-orchestration.md)
<!-- lesson: Contents/01-introduction/01-container-orchestration.md -->

- [Automated scheduling & placement](Contents/01-introduction/01-container-orchestration.md#automated-scheduling-placement)
- [Desired-state reconciliation](Contents/01-introduction/01-container-orchestration.md#desired-state-reconciliation)
- [Self-healing / auto-restart of failed containers](Contents/01-introduction/01-container-orchestration.md#self-healing-auto-restart-of-failed-containers)
- [Horizontal & vertical scaling](Contents/01-introduction/01-container-orchestration.md#horizontal-vertical-scaling)
- [Rolling updates without downtime](Contents/01-introduction/01-container-orchestration.md#rolling-updates-without-downtime)
- [Declarative configuration via manifests](Contents/01-introduction/01-container-orchestration.md#declarative-configuration-via-manifests)
- [Resource requests & limits (brief mention)](Contents/01-introduction/01-container-orchestration.md#resource-requests-limits-brief-mention)

## [How is Kubernetes different from plain Docker?](Contents/01-introduction/02-kubernetes-vs-docker.md)
<!-- lesson: Contents/01-introduction/02-kubernetes-vs-docker.md -->

- [Single host vs. multi-node cluster](Contents/01-introduction/02-kubernetes-vs-docker.md#single-host-vs-multi-node-cluster)
- [Manual `docker run`/`compose` vs. declarative manifests](Contents/01-introduction/02-kubernetes-vs-docker.md#manual-docker-runcompose-vs-declarative-manifests)
- [No built-in scheduling in plain Docker](Contents/01-introduction/02-kubernetes-vs-docker.md#no-built-in-scheduling-in-plain-docker)
- [No built-in self-healing in plain Docker](Contents/01-introduction/02-kubernetes-vs-docker.md#no-built-in-self-healing-in-plain-docker)
- [No cross-host service discovery/networking in Docker Compose](Contents/01-introduction/02-kubernetes-vs-docker.md#no-cross-host-service-discoverynetworking-in-docker-compose)
- [When plain Docker is still sufficient](Contents/01-introduction/02-kubernetes-vs-docker.md#when-plain-docker-is-still-sufficient)

## [What are the key benefits of using Kubernetes?](Contents/01-introduction/03-key-benefits.md)
<!-- lesson: Contents/01-introduction/03-key-benefits.md -->

- [Scalability](Contents/01-introduction/03-key-benefits.md#scalability)
- [Self-healing](Contents/01-introduction/03-key-benefits.md#self-healing)
- [High availability](Contents/01-introduction/03-key-benefits.md#high-availability)
- [Portability](Contents/01-introduction/03-key-benefits.md#portability)
- [Resource efficiency](Contents/01-introduction/03-key-benefits.md#resource-efficiency)
- [Extensibility via API & ecosystem](Contents/01-introduction/03-key-benefits.md#extensibility-via-api-ecosystem)

# Kubernetes Architecture
<!-- folder: 02-architecture -->

## [What is a cluster, and what is a node?](Contents/02-architecture/01-cluster-and-node.md)
<!-- lesson: Contents/02-architecture/01-cluster-and-node.md -->

- [Cluster = set of nodes](Contents/02-architecture/01-cluster-and-node.md#cluster-set-of-nodes)
- [Control plane vs. worker roles](Contents/02-architecture/01-cluster-and-node.md#control-plane-vs-worker-roles)
- [Single-node vs. multi-node clusters](Contents/02-architecture/01-cluster-and-node.md#single-node-vs-multi-node-clusters)
- [Node = physical or virtual machine](Contents/02-architecture/01-cluster-and-node.md#node-physical-or-virtual-machine)
- [Cluster-wide vs. per-node resources](Contents/02-architecture/01-cluster-and-node.md#cluster-wide-vs-per-node-resources)
- [How Docker Desktop's single-node cluster maps to this model](Contents/02-architecture/01-cluster-and-node.md#how-docker-desktops-single-node-cluster-maps-to-this-model)

## [What is the difference between the control plane and worker nodes?](Contents/02-architecture/02-control-plane-vs-worker.md)
<!-- lesson: Contents/02-architecture/02-control-plane-vs-worker.md -->

- [Control plane: cluster-wide decisions](Contents/02-architecture/02-control-plane-vs-worker.md#control-plane-cluster-wide-decisions)
- [Worker nodes: run application containers](Contents/02-architecture/02-control-plane-vs-worker.md#worker-nodes-run-application-containers)
- [Control plane can be single or multi-instance (HA)](Contents/02-architecture/02-control-plane-vs-worker.md#control-plane-can-be-single-or-multi-instance-ha)
- [Node roles are labeled, not physically distinct](Contents/02-architecture/02-control-plane-vs-worker.md#node-roles-are-labeled-not-physically-distinct)
- [Communication direction: API Server as central hub](Contents/02-architecture/02-control-plane-vs-worker.md#communication-direction-api-server-as-central-hub)
- [Failure impact: control plane vs. worker node outage](Contents/02-architecture/02-control-plane-vs-worker.md#failure-impact-control-plane-vs-worker-node-outage)

## [What components make up the control plane?](Contents/02-architecture/03-control-plane-components.md)
<!-- lesson: Contents/02-architecture/03-control-plane-components.md -->

- [API Server](Contents/02-architecture/03-control-plane-components.md#api-server)
- [Scheduler](Contents/02-architecture/03-control-plane-components.md#scheduler)
- [Controller Manager](Contents/02-architecture/03-control-plane-components.md#controller-manager)
- [etcd](Contents/02-architecture/03-control-plane-components.md#etcd)
- [Cloud Controller Manager (brief mention)](Contents/02-architecture/03-control-plane-components.md#cloud-controller-manager-brief-mention)
- [All components communicate through the API Server](Contents/02-architecture/03-control-plane-components.md#all-components-communicate-through-the-api-server)

## [What components run on a worker node?](Contents/02-architecture/04-worker-node-components.md)
<!-- lesson: Contents/02-architecture/04-worker-node-components.md -->

- [kubelet](Contents/02-architecture/04-worker-node-components.md#kubelet)
- [kube-proxy](Contents/02-architecture/04-worker-node-components.md#kube-proxy)
- [Container runtime (containerd, CRI-O, etc.)](Contents/02-architecture/04-worker-node-components.md#container-runtime-containerd-cri-o-etc)
- [Container Runtime Interface (CRI) concept](Contents/02-architecture/04-worker-node-components.md#container-runtime-interface-cri-concept)
- [kubelet reports node-level resource status to the API Server](Contents/02-architecture/04-worker-node-components.md#kubelet-reports-node-level-resource-status-to-the-api-server)
- [kubelet manages Pod lifecycle on the node](Contents/02-architecture/04-worker-node-components.md#kubelet-manages-pod-lifecycle-on-the-node)

# Pods & Namespaces
<!-- folder: 03-pods-and-namespaces -->

## [What is a Pod?](Contents/03-pods-and-namespaces/01-pod.md)
<!-- lesson: Contents/03-pods-and-namespaces/01-pod.md -->

- [Smallest deployable unit](Contents/03-pods-and-namespaces/01-pod.md#smallest-deployable-unit)
- [Single- vs. multi-container pods](Contents/03-pods-and-namespaces/01-pod.md#single-vs-multi-container-pods)
- [Shared network namespace (localhost between containers)](Contents/03-pods-and-namespaces/01-pod.md#shared-network-namespace-localhost-between-containers)
- [Shared storage volumes within a pod](Contents/03-pods-and-namespaces/01-pod.md#shared-storage-volumes-within-a-pod)
- [Pod lifecycle & phases](Contents/03-pods-and-namespaces/01-pod.md#pod-lifecycle-phases)
- [Ephemeral nature (pods are not durable identities)](Contents/03-pods-and-namespaces/01-pod.md#ephemeral-nature-pods-are-not-durable-identities)
- [Each Pod gets its own (ephemeral) cluster-internal IP address](Contents/03-pods-and-namespaces/01-pod.md#each-pod-gets-its-own-ephemeral-cluster-internal-ip-address)

## [What are labels and selectors?](Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
<!-- lesson: Contents/03-pods-and-namespaces/02-labels-and-selectors.md -->

- [Key/value metadata on objects](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#keyvalue-metadata-on-objects)
- [Used by Deployments & Services to match pods](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#used-by-deployments-services-to-match-pods)
- [Arbitrary vs. well-known labels](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#arbitrary-vs-well-known-labels)
- [Selector expressions (equality vs. set-based)](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#selector-expressions-equality-vs-set-based)
- [Labels vs. annotations](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#labels-vs-annotations)
- [Common labeling conventions (app, version, environment)](Contents/03-pods-and-namespaces/02-labels-and-selectors.md#common-labeling-conventions-app-version-environment)

## [What is a Namespace?](Contents/03-pods-and-namespaces/03-namespace.md)
<!-- lesson: Contents/03-pods-and-namespaces/03-namespace.md -->

- [Logical partitioning of a cluster](Contents/03-pods-and-namespaces/03-namespace.md#logical-partitioning-of-a-cluster)
- [Environment separation (dev/staging/prod)](Contents/03-pods-and-namespaces/03-namespace.md#environment-separation-devstagingprod)
- [Namespace-scoped vs. cluster-scoped resources](Contents/03-pods-and-namespaces/03-namespace.md#namespace-scoped-vs-cluster-scoped-resources)
- [Default namespace](Contents/03-pods-and-namespaces/03-namespace.md#default-namespace)
- [Resource quotas per namespace (brief mention)](Contents/03-pods-and-namespaces/03-namespace.md#resource-quotas-per-namespace-brief-mention)
- [Naming & switching context with `kubectl`](Contents/03-pods-and-namespaces/03-namespace.md#naming-switching-context-with-kubectl)

# `kubectl` — CLI for Kubernetes
<!-- folder: 04-kubectl -->

## [How do I interact with a cluster using `kubectl`?](Contents/04-kubectl/01-kubectl-basics.md)
<!-- lesson: Contents/04-kubectl/01-kubectl-basics.md -->

- [cluster-info, namespaces, pods, logs, events](Contents/04-kubectl/01-kubectl-basics.md#cluster-info-namespaces-pods-logs-events)
- [Context & namespace switching](Contents/04-kubectl/01-kubectl-basics.md#context-namespace-switching)
- [`kubectl get` / `describe` / `logs` verbs](Contents/04-kubectl/01-kubectl-basics.md#kubectl-get-describe-logs-verbs)
- [`kubectl apply -f` / `create` / `delete` — creating and updating resources from manifests](Contents/04-kubectl/01-kubectl-basics.md#kubectl-apply-f-create-delete-creating-and-updating-resources-from-manifests)
- [Output formats (-o wide/yaml/json)](Contents/04-kubectl/01-kubectl-basics.md#output-formats-o-wideyamljson)
- [`kubectl explain` for discovering fields](Contents/04-kubectl/01-kubectl-basics.md#kubectl-explain-for-discovering-fields)
- [Interacting with kube-system components](Contents/04-kubectl/01-kubectl-basics.md#interacting-with-kube-system-components)

## Practice: First Steps with `kubectl`

- Inspect cluster & nodes
- List namespaces and system pods
- Switch active namespace
- View logs of a system pod
- List recent cluster events
- Explore a resource's fields via `kubectl explain`

# Deployments
<!-- folder: 05-deployments -->

## [What is a Deployment, and how does it relate to a ReplicaSet?](Contents/05-deployments/01-deployment-and-replicaset.md)
<!-- lesson: Contents/05-deployments/01-deployment-and-replicaset.md -->

- [Deployment manages a ReplicaSet](Contents/05-deployments/01-deployment-and-replicaset.md#deployment-manages-a-replicaset)
- [Declarative desired-state for Pods](Contents/05-deployments/01-deployment-and-replicaset.md#declarative-desired-state-for-pods)
- [ReplicaSet ensures pod count matches spec](Contents/05-deployments/01-deployment-and-replicaset.md#replicaset-ensures-pod-count-matches-spec)
- [Deployment adds versioned rollout history](Contents/05-deployments/01-deployment-and-replicaset.md#deployment-adds-versioned-rollout-history)
- [Relationship: Deployment → ReplicaSet → Pods](Contents/05-deployments/01-deployment-and-replicaset.md#relationship-deployment-replicaset-pods)
- [When to use a bare ReplicaSet vs. a Deployment](Contents/05-deployments/01-deployment-and-replicaset.md#when-to-use-a-bare-replicaset-vs-a-deployment)

## [How does Kubernetes scale and self-heal Pods?](Contents/05-deployments/02-scaling-and-self-healing.md)
<!-- lesson: Contents/05-deployments/02-scaling-and-self-healing.md -->

- [Scaling replica count](Contents/05-deployments/02-scaling-and-self-healing.md#scaling-replica-count)
- [Automatic pod replacement on failure](Contents/05-deployments/02-scaling-and-self-healing.md#automatic-pod-replacement-on-failure)
- [Horizontal scaling via `kubectl scale`](Contents/05-deployments/02-scaling-and-self-healing.md#horizontal-scaling-via-kubectl-scale)
- [Readiness affects traffic routing](Contents/05-deployments/02-scaling-and-self-healing.md#readiness-affects-traffic-routing)
- [Liveness probes trigger restarts (brief mention)](Contents/05-deployments/02-scaling-and-self-healing.md#liveness-probes-trigger-restarts-brief-mention)
- [Manual vs. automatic (HPA) scaling (brief mention)](Contents/05-deployments/02-scaling-and-self-healing.md#manual-vs-automatic-hpa-scaling-brief-mention)

## [How do rolling updates and rollbacks work?](Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
<!-- lesson: Contents/05-deployments/03-rolling-updates-and-rollbacks.md -->

- [Gradual version replacement](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#gradual-version-replacement)
- [Reverting to a previous revision](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#reverting-to-a-previous-revision)
- [Rollout strategies (RollingUpdate vs. Recreate)](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#rollout-strategies-rollingupdate-vs-recreate)
- [maxSurge / maxUnavailable concept](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#maxsurge-maxunavailable-concept)
- [Pausing & resuming a rollout](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#pausing-resuming-a-rollout)
- [Viewing rollout history & status](Contents/05-deployments/03-rolling-updates-and-rollbacks.md#viewing-rollout-history-status)

## Practice: Deploy Pod(s) into the Cluster

- Create & scale a Deployment
- Observe self-healing after deleting a pod
- Trigger a rolling update
- Roll back to a previous revision
- Inspect rollout status
- Clean up the Deployment

# Services & Networking
<!-- folder: 06-services-and-networking -->

## [What is a Service?](Contents/06-services-and-networking/01-service.md)
<!-- lesson: Contents/06-services-and-networking/01-service.md -->

- [Stable virtual IP/DNS name](Contents/06-services-and-networking/01-service.md#stable-virtual-ipdns-name)
- [Load balancing across matching pods](Contents/06-services-and-networking/01-service.md#load-balancing-across-matching-pods)
- [Decoupling consumers from pod IP churn](Contents/06-services-and-networking/01-service.md#decoupling-consumers-from-pod-ip-churn)
- [Service discovery via DNS](Contents/06-services-and-networking/01-service.md#service-discovery-via-dns)
- [Selector-based endpoint matching](Contents/06-services-and-networking/01-service.md#selector-based-endpoint-matching)
- [Headless services (brief mention)](Contents/06-services-and-networking/01-service.md#headless-services-brief-mention)

## [What types of Services are there?](Contents/06-services-and-networking/02-service-types.md)
<!-- lesson: Contents/06-services-and-networking/02-service-types.md -->

- [ClusterIP](Contents/06-services-and-networking/02-service-types.md#clusterip)
- [NodePort](Contents/06-services-and-networking/02-service-types.md#nodeport)
- [LoadBalancer](Contents/06-services-and-networking/02-service-types.md#loadbalancer)
- [ExternalName (brief mention)](Contents/06-services-and-networking/02-service-types.md#externalname-brief-mention)
- [Default type behavior](Contents/06-services-and-networking/02-service-types.md#default-type-behavior)
- [When to choose which type](Contents/06-services-and-networking/02-service-types.md#when-to-choose-which-type)

## [How do I expose a Service outside the cluster?](Contents/06-services-and-networking/03-exposing-services.md)
<!-- lesson: Contents/06-services-and-networking/03-exposing-services.md -->

- [Host/path-based external routing](Contents/06-services-and-networking/03-exposing-services.md#hostpath-based-external-routing)
- [Gateway API vs. Ingress](Contents/06-services-and-networking/03-exposing-services.md#gateway-api-vs-ingress)
- [TLS termination](Contents/06-services-and-networking/03-exposing-services.md#tls-termination)
- [Single entrypoint for multiple services](Contents/06-services-and-networking/03-exposing-services.md#single-entrypoint-for-multiple-services)
- [Ingress controller requirement](Contents/06-services-and-networking/03-exposing-services.md#ingress-controller-requirement)
- [Name-based virtual hosting](Contents/06-services-and-networking/03-exposing-services.md#name-based-virtual-hosting)

## Practice: Deployment with Services

- Expose a 2-replica Deployment
- Access via NodePort/Gateway
- Verify load balancing across replicas
- Inspect Service endpoints
- Test DNS-based service discovery
- Clean up Service & Deployment

# Configuration Management
<!-- folder: 07-configuration-management -->

## [What is a ConfigMap?](Contents/07-configuration-management/01-configmap.md)
<!-- lesson: Contents/07-configuration-management/01-configmap.md -->

- [Externalized non-sensitive configuration](Contents/07-configuration-management/01-configmap.md#externalized-non-sensitive-configuration)
- [Env vars vs. mounted files](Contents/07-configuration-management/01-configmap.md#env-vars-vs-mounted-files)
- [Updating a ConfigMap without rebuilding images](Contents/07-configuration-management/01-configmap.md#updating-a-configmap-without-rebuilding-images)
- [ConfigMap as command-line args source](Contents/07-configuration-management/01-configmap.md#configmap-as-command-line-args-source)
- [Immutable ConfigMaps (brief mention)](Contents/07-configuration-management/01-configmap.md#immutable-configmaps-brief-mention)
- [Referencing a ConfigMap in a Pod spec](Contents/07-configuration-management/01-configmap.md#referencing-a-configmap-in-a-pod-spec)

## [What is a Secret, and how does it differ from a ConfigMap?](Contents/07-configuration-management/02-secret.md)
<!-- lesson: Contents/07-configuration-management/02-secret.md -->

- [Externalized sensitive data](Contents/07-configuration-management/02-secret.md#externalized-sensitive-data)
- [Access restrictions vs. ConfigMaps](Contents/07-configuration-management/02-secret.md#access-restrictions-vs-configmaps)
- [Base64 encoding vs. encryption (clarify: not encryption)](Contents/07-configuration-management/02-secret.md#base64-encoding-vs-encryption-clarify-not-encryption)
- [Secret types (generic, docker-registry, tls)](Contents/07-configuration-management/02-secret.md#secret-types-generic-docker-registry-tls)
- [Mounting Secrets as files vs. env vars](Contents/07-configuration-management/02-secret.md#mounting-secrets-as-files-vs-env-vars)
- [Least-privilege access considerations](Contents/07-configuration-management/02-secret.md#least-privilege-access-considerations)

## Practice: Deployment with ConfigMap and Secret

- Mount ConfigMap & Secret into a Deployment
- Verify values inside the container
- Update a ConfigMap and observe (non-)propagation
- Inject a Secret as an environment variable
- Compare file-mount vs. env-var access
- Clean up ConfigMap, Secret & Deployment

# Access Control
<!-- folder: 08-access-control -->

## [What is RBAC (Role-Based Access Control)?](Contents/08-access-control/01-rbac.md)
<!-- lesson: Contents/08-access-control/01-rbac.md -->

- [Roles / RoleBindings](Contents/08-access-control/01-rbac.md#roles-rolebindings)
- [ClusterRoles / ClusterRoleBindings](Contents/08-access-control/01-rbac.md#clusterroles-clusterrolebindings)
- [Subjects (users, groups, service accounts)](Contents/08-access-control/01-rbac.md#subjects-users-groups-service-accounts)
- [Verbs & resources in a Role rule](Contents/08-access-control/01-rbac.md#verbs-resources-in-a-role-rule)
- [Namespace-scoped vs. cluster-scoped permissions](Contents/08-access-control/01-rbac.md#namespace-scoped-vs-cluster-scoped-permissions)
- [Principle of least privilege](Contents/08-access-control/01-rbac.md#principle-of-least-privilege)

## [What is a Service Account?](Contents/08-access-control/02-service-account.md)
<!-- lesson: Contents/08-access-control/02-service-account.md -->

- [Pod identity toward the API server](Contents/08-access-control/02-service-account.md#pod-identity-toward-the-api-server)
- [Default vs. custom service accounts](Contents/08-access-control/02-service-account.md#default-vs-custom-service-accounts)
- [Automatic token mounting](Contents/08-access-control/02-service-account.md#automatic-token-mounting)
- [Binding a Role to a Service Account](Contents/08-access-control/02-service-account.md#binding-a-role-to-a-service-account)
- [Use cases: CI/CD, Operators, in-cluster tooling](Contents/08-access-control/02-service-account.md#use-cases-cicd-operators-in-cluster-tooling)
- [Disabling auto-mount for security](Contents/08-access-control/02-service-account.md#disabling-auto-mount-for-security)

# Storage & State
<!-- folder: 09-storage-and-state -->

## [How does Kubernetes handle persistent storage?](Contents/09-storage-and-state/01-persistent-storage.md)
<!-- lesson: Contents/09-storage-and-state/01-persistent-storage.md -->

- [Volumes](Contents/09-storage-and-state/01-persistent-storage.md#volumes)
- [PersistentVolume / PersistentVolumeClaim](Contents/09-storage-and-state/01-persistent-storage.md#persistentvolume-persistentvolumeclaim)
- [StorageClass & dynamic provisioning (brief mention)](Contents/09-storage-and-state/01-persistent-storage.md#storageclass-dynamic-provisioning-brief-mention)
- [Access modes (ReadWriteOnce, ReadWriteMany, etc.)](Contents/09-storage-and-state/01-persistent-storage.md#access-modes-readwriteonce-readwritemany-etc)
- [Volume lifecycle vs. pod lifecycle](Contents/09-storage-and-state/01-persistent-storage.md#volume-lifecycle-vs-pod-lifecycle)
- [emptyDir vs. persistent volumes](Contents/09-storage-and-state/01-persistent-storage.md#emptydir-vs-persistent-volumes)
- [Docker Desktop's default `hostpath` StorageClass (exercise environment)](Contents/09-storage-and-state/01-persistent-storage.md#docker-desktops-default-hostpath-storageclass-exercise-environment)

## [What is a StatefulSet?](Contents/09-storage-and-state/02-statefulset.md)
<!-- lesson: Contents/09-storage-and-state/02-statefulset.md -->

- [Stable per-replica identity](Contents/09-storage-and-state/02-statefulset.md#stable-per-replica-identity)
- [Ordered deployment & scaling](Contents/09-storage-and-state/02-statefulset.md#ordered-deployment-scaling)
- [Stable network identity per replica](Contents/09-storage-and-state/02-statefulset.md#stable-network-identity-per-replica)
- [Stable storage per replica (via volumeClaimTemplates)](Contents/09-storage-and-state/02-statefulset.md#stable-storage-per-replica-via-volumeclaimtemplates)
- [Ordered, graceful termination](Contents/09-storage-and-state/02-statefulset.md#ordered-graceful-termination)
- [Use cases: databases, distributed systems](Contents/09-storage-and-state/02-statefulset.md#use-cases-databases-distributed-systems)

# Workload Patterns
<!-- folder: 10-workload-patterns -->

## [What is a DaemonSet?](Contents/10-workload-patterns/01-daemonset.md)
<!-- lesson: Contents/10-workload-patterns/01-daemonset.md -->

- [One pod per (selected) node](Contents/10-workload-patterns/01-daemonset.md#one-pod-per-selected-node)
- [Use case: log/monitoring agents](Contents/10-workload-patterns/01-daemonset.md#use-case-logmonitoring-agents)
- [Node selectors/affinity for targeting](Contents/10-workload-patterns/01-daemonset.md#node-selectorsaffinity-for-targeting)
- [Automatic scheduling on new nodes](Contents/10-workload-patterns/01-daemonset.md#automatic-scheduling-on-new-nodes)
- [Comparison to Deployment (no fixed replica count)](Contents/10-workload-patterns/01-daemonset.md#comparison-to-deployment-no-fixed-replica-count)
- [Update strategies for DaemonSets](Contents/10-workload-patterns/01-daemonset.md#update-strategies-for-daemonsets)

## [What is an Init Container?](Contents/10-workload-patterns/02-init-container.md)
<!-- lesson: Contents/10-workload-patterns/02-init-container.md -->

- [Run-to-completion before app containers](Contents/10-workload-patterns/02-init-container.md#run-to-completion-before-app-containers)
- [Use case: setup/dependency waits](Contents/10-workload-patterns/02-init-container.md#use-case-setupdependency-waits)
- [Sequential execution order](Contents/10-workload-patterns/02-init-container.md#sequential-execution-order)
- [Separate image/resource profile from app container](Contents/10-workload-patterns/02-init-container.md#separate-imageresource-profile-from-app-container)
- [Failure handling (pod restart on init failure)](Contents/10-workload-patterns/02-init-container.md#failure-handling-pod-restart-on-init-failure)
- [Common patterns: schema migration, config generation](Contents/10-workload-patterns/02-init-container.md#common-patterns-schema-migration-config-generation)

## [What is a Sidecar Container?](Contents/10-workload-patterns/03-sidecar-container.md)
<!-- lesson: Contents/10-workload-patterns/03-sidecar-container.md -->

- [Auxiliary container in the same pod](Contents/10-workload-patterns/03-sidecar-container.md#auxiliary-container-in-the-same-pod)
- [Use case: proxies, log shippers](Contents/10-workload-patterns/03-sidecar-container.md#use-case-proxies-log-shippers)
- [Shared network & volume with the main container](Contents/10-workload-patterns/03-sidecar-container.md#shared-network-volume-with-the-main-container)
- [Lifecycle coupling with the main container](Contents/10-workload-patterns/03-sidecar-container.md#lifecycle-coupling-with-the-main-container)
- [Native sidecar support (restartPolicy on init containers, brief mention)](Contents/10-workload-patterns/03-sidecar-container.md#native-sidecar-support-restartpolicy-on-init-containers-brief-mention)
- [Examples: service mesh proxies, log forwarders](Contents/10-workload-patterns/03-sidecar-container.md#examples-service-mesh-proxies-log-forwarders)

## [What is an Operator?](Contents/10-workload-patterns/04-operator.md)
<!-- lesson: Contents/10-workload-patterns/04-operator.md -->

- [Custom controller + CRD](Contents/10-workload-patterns/04-operator.md#custom-controller-crd)
- [Automates day-2 operational tasks](Contents/10-workload-patterns/04-operator.md#automates-day-2-operational-tasks)
- [Reconciliation loop pattern](Contents/10-workload-patterns/04-operator.md#reconciliation-loop-pattern)
- [Encoding operational knowledge as code](Contents/10-workload-patterns/04-operator.md#encoding-operational-knowledge-as-code)
- [Examples: database operators, certificate operators](Contents/10-workload-patterns/04-operator.md#examples-database-operators-certificate-operators)
- [Operator Framework / OperatorHub (brief mention)](Contents/10-workload-patterns/04-operator.md#operator-framework-operatorhub-brief-mention)

# CI/CD with Kubernetes
<!-- folder: 11-ci-cd -->

## [What is GitOps?](Contents/11-ci-cd/01-gitops.md)
<!-- lesson: Contents/11-ci-cd/01-gitops.md -->

- [Git as source of truth](Contents/11-ci-cd/01-gitops.md#git-as-source-of-truth)
- [Automated sync/reconciliation (conceptual)](Contents/11-ci-cd/01-gitops.md#automated-syncreconciliation-conceptual)
- [Pull-based vs. push-based deployment](Contents/11-ci-cd/01-gitops.md#pull-based-vs-push-based-deployment)
- [Declarative desired state stored in Git](Contents/11-ci-cd/01-gitops.md#declarative-desired-state-stored-in-git)
- [Drift detection & auto-correction](Contents/11-ci-cd/01-gitops.md#drift-detection-auto-correction)
- [Auditability via commit history](Contents/11-ci-cd/01-gitops.md#auditability-via-commit-history)
- [Examples: Argo CD, Flux (brief mention)](Contents/11-ci-cd/01-gitops.md#examples-argo-cd-flux-brief-mention)

## [How does a deployment pipeline work with Kubernetes?](Contents/11-ci-cd/02-deployment-pipeline.md)
<!-- lesson: Contents/11-ci-cd/02-deployment-pipeline.md -->

- [Build → test → package → deploy](Contents/11-ci-cd/02-deployment-pipeline.md#build-test-package-deploy)
- [Environment promotion (dev → staging → prod)](Contents/11-ci-cd/02-deployment-pipeline.md#environment-promotion-dev-staging-prod)
- [Image tagging & versioning strategy](Contents/11-ci-cd/02-deployment-pipeline.md#image-tagging-versioning-strategy)
- [Automated rollout triggers](Contents/11-ci-cd/02-deployment-pipeline.md#automated-rollout-triggers)
- [Rollback as part of the pipeline](Contents/11-ci-cd/02-deployment-pipeline.md#rollback-as-part-of-the-pipeline)
- [Separation of CI (build/test) and CD (deploy) concerns](Contents/11-ci-cd/02-deployment-pipeline.md#separation-of-ci-buildtest-and-cd-deploy-concerns)

# Package Management: Helm & Kustomize
<!-- folder: 12-package-management -->

## [What is Helm?](Contents/12-package-management/01-helm.md)
<!-- lesson: Contents/12-package-management/01-helm.md -->

- [Package manager ("charts") for Kubernetes](Contents/12-package-management/01-helm.md#package-manager-charts-for-kubernetes)
- [Install/upgrade/rollback as a unit](Contents/12-package-management/01-helm.md#installupgraderollback-as-a-unit)
- [Templating with values files](Contents/12-package-management/01-helm.md#templating-with-values-files)
- [Chart repositories](Contents/12-package-management/01-helm.md#chart-repositories)
- [Release versioning & history](Contents/12-package-management/01-helm.md#release-versioning-history)
- [Managing multi-resource applications as one unit](Contents/12-package-management/01-helm.md#managing-multi-resource-applications-as-one-unit)

## [What is Kustomize?](Contents/12-package-management/02-kustomize.md)
<!-- lesson: Contents/12-package-management/02-kustomize.md -->

- [Overlay-based YAML customization](Contents/12-package-management/02-kustomize.md#overlay-based-yaml-customization)
- [Built into `kubectl -k`](Contents/12-package-management/02-kustomize.md#built-into-kubectl-k)
- [Base + overlay pattern](Contents/12-package-management/02-kustomize.md#base-overlay-pattern)
- [Patches vs. templating (Kustomize vs. Helm)](Contents/12-package-management/02-kustomize.md#patches-vs-templating-kustomize-vs-helm)
- [Environment-specific overlays (dev/staging/prod)](Contents/12-package-management/02-kustomize.md#environment-specific-overlays-devstagingprod)
- [No templating language required](Contents/12-package-management/02-kustomize.md#no-templating-language-required)

# Service Mesh
<!-- folder: 13-service-mesh -->

## [What is a service mesh, and why would I need one?](Contents/13-service-mesh/01-service-mesh.md)
<!-- lesson: Contents/13-service-mesh/01-service-mesh.md -->

- [Service-to-service traffic layer (routing, retries, mTLS)](Contents/13-service-mesh/01-service-mesh.md#service-to-service-traffic-layer-routing-retries-mtls)
- [Examples: Istio, Traefik Mesh](Contents/13-service-mesh/01-service-mesh.md#examples-istio-traefik-mesh)
- [Sidecar proxy pattern](Contents/13-service-mesh/01-service-mesh.md#sidecar-proxy-pattern)
- [Observability (traffic metrics, tracing)](Contents/13-service-mesh/01-service-mesh.md#observability-traffic-metrics-tracing)
- [Traffic splitting / canary routing](Contents/13-service-mesh/01-service-mesh.md#traffic-splitting-canary-routing)
- [When a service mesh is (not) needed](Contents/13-service-mesh/01-service-mesh.md#when-a-service-mesh-is-not-needed)

# Further Reading / Links
<!-- no folder: reference links only, not a lesson module -->

- [What is Kubernetes? An Introduction With Examples](https://www.datacamp.com/blog/what-is-kubernetes)
- [Kubernetes: An Introduction for Beginners](https://tecadmin.net/kubernetes-introduction/)
- [GitHub: Kubernetes in Action, 2nd Edition](https://github.com/luksa/kubernetes-in-action-2nd-edition)
- [kubectl cheatsheet](https://kubernetes.io/de/docs/reference/kubectl/cheatsheet/)
