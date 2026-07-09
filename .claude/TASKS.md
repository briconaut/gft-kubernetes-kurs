---
revision: 0
path: ".claude/TASKS.md"
title: "Task Backlog"
abstract: "Single, cumulative task list for all workshop phases (0-8), grouped by phase. Status model: [ ] Open, [~] In Progress, [R] Needs Rework, [B] Blocked, [X] Done."
state: in progress
lang: en
numbersections: false
finished_sections: [ ]
history: [ ]
---

# Task Backlog

Status model, task-selection algorithm and the Follow-up Refinement Subtasks convention are defined in `CLAUDE.md` → Styleguide → Task Definition.
File-format rules referenced below live in `.claude/STYLE.md`.
Numbering is `<phase>.<sequence>`, with optional follow-up-refinement subtasks `<phase>.<sequence>.<subsequence>`.

## Phase 0 — Planning (done in Claude Project chat)

Artefacts created/modified by Phase 0:

- `CLAUDE.md`
- `.claude/TASKS.md`
- `.claude/MEMORY.md`

For all steps in this phase, read all files in `Original` consider the contents as inspirational.

- 0.00 [ ] Summarize the contents of the files in the `Original` directory.
  Create

- 0.01 [ ] Produce section `## What this repository is`.
- 0.02 [ ] Produce section `## Language`
- 0.03 [ ] Produce section `## Audience of the workshop`
- 0.04 [ ] Produce section `# Workshop description`
- 0.05 [ ] Produce section `## Workshop Scope`
- 0.06 [ ] Produce section `## Non-Goals`
- 0.07 [ ] Produce section `## Folder & File Conventions`
- 0.08 [ ] Produce section `## Process / Phases`
- 0.09 [ ] Produce section `## Styleguide`
- 0.10 [ ] Produce section `## Task Definition (`.claude/TASKS.md`)`
- 0.11 [ ] Produce section `### Status values`
- 0.12 [ ] Produce section `### Allowed status transitions (Claude Code agent)`
- 0.13 [ ] Produce section `## Task selection algorithm`
- 0.14 [ ] Produce section `## Task granularity`
- 0.15 [ ] Produce section `## Follow-up Refinement Subtasks`
- 0.16 [ ] Produce section `# Memory Structure`

  

- 0.2 [ ] Produce skill `l1-build` 


- X.2 [ ] Produce `.claude/TASKS.md` — consolidated task backlog for all phases (this file)
- X.3 [ ] Produce `.claude/Memory.md` — seeded, empty global memory file

## Phase 1 — Execution (Claude Code agent, this repo) — Contents.md topic list

- 1.1 [ ] Review the existing Contents.md draft (inspiration only, not binding) and produce a definitive list of topics to cover, organized into logical sections — headings + bullet points only, no explanatory prose (file: Contents.md)
  - 1.1.1 [ ] Expanded every subtopic's bullet list to at least 6 points (commit 0e21a8d)
- 1.2 [ ] Phrase each topic as a concrete, answerable question in the audience's terms (e.g. "What is a container?", "What is a Node?", "What is a Pod?", "What is a Service?") rather than abstract chapter titles (file: Contents.md)
  - 1.2.1 [ ] Verified bullets answer their subheading's question; tightened "What components run on a worker node?" to name components rather than responsibilities
  - 1.2.2 [ ] Verified bullet completeness for the intro audience; added Pod IP address, `kubectl apply/create/delete`, Docker Desktop `hostpath` StorageClass, and GitOps tool-example bullets, and replaced a redundant Docker-comparison bullet
  - 1.2.3 [ ] Added "Resource requests & limits (brief mention)" bullet under "What is container orchestration?" (kept as an addition, not a replacement, to avoid colliding with the dedicated Configuration Management section)
- 1.3 [ ] Assign a stable `<nr>-<section>` folder slug to each top-level section, to be used as the folder name in Phase 2 (file: Contents.md)
  - 1.3.1 [ ] Added a stable full-path `<!-- lesson: Contents/<nr>-<section>/<nr>-<lesson>.md -->` comment under each `##` topic heading (per-section local numbering), analogous to the section-level `folder:` comments; `## Practice: ...` headings excluded (Phase 8 scheme)
- 1.4 [ ] Note in `.claude/Memory.md` how the old draft's structure was reused or deviated from, so Phase 2 stays consistent (file: .claude/Memory.md)

## Phase 2 — Execution (Claude Code agent, this repo) — Contents.md structure (folders + lesson-file skeletons)

- 2.1 [ ] Create the 13 folders `Contents/<nr>-<section>/` named by the `<!-- folder: ... -->` comments in Contents.md, if they don't exist yet (file: Contents/<nr>-<section>/)
- 2.2 [ ] For every `<!-- lesson: Contents/<nr>-<section>/<local-nr>-<lesson>.md -->` comment in Contents.md, create the lesson file at exactly that path with correct frontmatter (`state: not started`) and the skeleton body per `.claude/STYLE.md` → Lesson File Format (H1, linked `## Overview`, one empty `##` heading per bullet with a `_Content pending (Phase 4)._` placeholder) — no prose yet. Use the path from the comment verbatim (file: Contents/<nr>-<section>/<local-nr>-<lesson>.md)
- 2.3 [ ] Update Contents.md: turn each `##` topic heading into a Markdown link to its `lesson:` file (link format per `.claude/STYLE.md` → Format of Contents.md), keeping the underlying `<!-- lesson: ... -->` comment intact; leave `## Practice: ...` headings untouched (file: Contents.md)
  - 2.3.1 [ ] Replaced all 197 bullet points under linked topics with links to their own anchor in the corresponding lesson file, reusing the anchors from each file's `## Overview`; bullets under `## Practice: ...` topics left as plain text (no lesson file); `.claude/STYLE.md` intentionally left unchanged per user instruction

## Phase 3 — Planning (done in Claude Project chat)

- 3.1 [ ] Review Phase 1/2 output (Contents.md + lesson-file skeletons); update CLAUDE.md/.claude/STYLE.md if needed
  - Executed by the Claude Code agent per explicit user instruction (normally a planning-chat task). Verified: all 13 folders, all 32 lesson-file skeletons match `.claude/STYLE.md` → Frontmatter and Lesson File Format (spot-checked `Contents/07-configuration-management/02-secret.md`); Contents.md structure (32 linked topics, 4 untouched `## Practice: ...`, 197 bullet-anchor links, `folder:`/`lesson:` comments) matches counts from Tasks 2.1–2.3.1. Found and fixed one spec/reality drift: `.claude/STYLE.md` → "Format of Contents.md" didn't document the bullet-anchor-link convention from Task 2.3.1 (intentionally left out of that `/improve` run) — added it now. No CLAUDE.md scope/content issues found.
- 3.2 [ ] Add detailed Phase 4 tasks (3.x → 4.x) to this file, based on the finished lesson-file skeletons from Phase 2. For each lesson file:
  - One task per `## <bullet>` subheading (excluding `## Overview`), replacing that heading's `_Content pending (Phase 4)._` placeholder with actual prose, per `.claude/STYLE.md` → Lesson File Format.
  - One additional task, inserted directly after that file's last subheading task, reviewing the now-complete lesson file for:
    - Consistency of phrasing/style across the file's subheadings
    - Fit of each subheading for the workshop (scope, audience, non-goals per CLAUDE.md)
    - Fit of each subheading for its parent `##` topic heading
    - Fit of the whole lesson file for its parent `##` topic heading
    - Fit of the whole lesson file for the workshop (scope, audience, non-goals per CLAUDE.md)
  - Review tasks are regular top-level `4.x` tasks — **not** Follow-up Refinement Subtasks (`4.x.y` stays reserved for post-completion `/improve` runs per CLAUDE.md → Follow-up Refinement Subtasks). A review task does not edit content itself; if it finds issues, it may recommend `[R]` rework for the affected subheading task(s) per CLAUDE.md → Task Definition.

## Phase 4 — Execution (Claude Code agent, this repo) — Contents.md lesson content

One task per `## <bullet>` subheading (replaces its `_Content pending (Phase 4)._` placeholder with prose, per `.claude/STYLE.md` → Lesson File Format), plus one review task per lesson file (per Task 3.2; does not edit content, may recommend `[R]` rework for specific subheading tasks).

**Contents/01-introduction/01-container-orchestration.md** — "What is container orchestration?"

- 4.1 [ ] Write prose for `## Automated scheduling & placement` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.2 [ ] Write prose for `## Desired-state reconciliation` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.3 [ ] Write prose for `## Self-healing / auto-restart of failed containers` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.4 [ ] Write prose for `## Horizontal & vertical scaling` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.5 [ ] Write prose for `## Rolling updates without downtime` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.6 [ ] Write prose for `## Declarative configuration via manifests` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.7 [ ] Write prose for `## Resource requests & limits (brief mention)` in Contents/01-introduction/01-container-orchestration.md (file: Contents/01-introduction/01-container-orchestration.md)
- 4.8 [ ] Review Contents/01-introduction/01-container-orchestration.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is container orchestration?" (file: Contents/01-introduction/01-container-orchestration.md)

**Contents/01-introduction/02-kubernetes-vs-docker.md** — "How is Kubernetes different from plain Docker?"

- 4.9 [ ] Write prose for `## Single host vs. multi-node cluster` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.10 [ ] Write prose for `## Manual \`docker run\`/\`compose\` vs. declarative manifests` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.11 [ ] Write prose for `## No built-in scheduling in plain Docker` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.12 [ ] Write prose for `## No built-in self-healing in plain Docker` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.13 [ ] Write prose for `## No cross-host service discovery/networking in Docker Compose` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.14 [ ] Write prose for `## When plain Docker is still sufficient` in Contents/01-introduction/02-kubernetes-vs-docker.md (file: Contents/01-introduction/02-kubernetes-vs-docker.md)
- 4.15 [ ] Review Contents/01-introduction/02-kubernetes-vs-docker.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How is Kubernetes different from plain Docker?" (file: Contents/01-introduction/02-kubernetes-vs-docker.md)

**Contents/01-introduction/03-key-benefits.md** — "What are the key benefits of using Kubernetes?"

- 4.16 [ ] Write prose for `## Scalability` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.17 [ ] Write prose for `## Self-healing` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.18 [ ] Write prose for `## High availability` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.19 [ ] Write prose for `## Portability` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.20 [ ] Write prose for `## Resource efficiency` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.21 [ ] Write prose for `## Extensibility via API & ecosystem` in Contents/01-introduction/03-key-benefits.md (file: Contents/01-introduction/03-key-benefits.md)
- 4.22 [ ] Review Contents/01-introduction/03-key-benefits.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What are the key benefits of using Kubernetes?" (file: Contents/01-introduction/03-key-benefits.md)

**Contents/02-architecture/01-cluster-and-node.md** — "What is a cluster, and what is a node?"

- 4.23 [ ] Write prose for `## Cluster = set of nodes` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.24 [ ] Write prose for `## Control plane vs. worker roles` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.25 [ ] Write prose for `## Single-node vs. multi-node clusters` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.26 [ ] Write prose for `## Node = physical or virtual machine` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.27 [ ] Write prose for `## Cluster-wide vs. per-node resources` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.28 [ ] Write prose for `## How Docker Desktop's single-node cluster maps to this model` in Contents/02-architecture/01-cluster-and-node.md (file: Contents/02-architecture/01-cluster-and-node.md)
- 4.29 [ ] Review Contents/02-architecture/01-cluster-and-node.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a cluster, and what is a node?" (file: Contents/02-architecture/01-cluster-and-node.md)

**Contents/02-architecture/02-control-plane-vs-worker.md** — "What is the difference between the control plane and worker nodes?"

- 4.30 [ ] Write prose for `## Control plane: cluster-wide decisions` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.31 [ ] Write prose for `## Worker nodes: run application containers` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.32 [ ] Write prose for `## Control plane can be single or multi-instance (HA)` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.33 [ ] Write prose for `## Node roles are labeled, not physically distinct` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.34 [ ] Write prose for `## Communication direction: API Server as central hub` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.35 [ ] Write prose for `## Failure impact: control plane vs. worker node outage` in Contents/02-architecture/02-control-plane-vs-worker.md (file: Contents/02-architecture/02-control-plane-vs-worker.md)
- 4.36 [ ] Review Contents/02-architecture/02-control-plane-vs-worker.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is the difference between the control plane and worker nodes?" (file: Contents/02-architecture/02-control-plane-vs-worker.md)

**Contents/02-architecture/03-control-plane-components.md** — "What components make up the control plane?"

- 4.37 [ ] Write prose for `## API Server` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.38 [ ] Write prose for `## Scheduler` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.39 [ ] Write prose for `## Controller Manager` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.40 [ ] Write prose for `## etcd` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.41 [ ] Write prose for `## Cloud Controller Manager (brief mention)` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.42 [ ] Write prose for `## All components communicate through the API Server` in Contents/02-architecture/03-control-plane-components.md (file: Contents/02-architecture/03-control-plane-components.md)
- 4.43 [ ] Review Contents/02-architecture/03-control-plane-components.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What components make up the control plane?" (file: Contents/02-architecture/03-control-plane-components.md)

**Contents/02-architecture/04-worker-node-components.md** — "What components run on a worker node?"

- 4.44 [ ] Write prose for `## kubelet` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.45 [ ] Write prose for `## kube-proxy` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.46 [ ] Write prose for `## Container runtime (containerd, CRI-O, etc.)` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.47 [ ] Write prose for `## Container Runtime Interface (CRI) concept` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.48 [ ] Write prose for `## kubelet reports node-level resource status to the API Server` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.49 [ ] Write prose for `## kubelet manages Pod lifecycle on the node` in Contents/02-architecture/04-worker-node-components.md (file: Contents/02-architecture/04-worker-node-components.md)
- 4.50 [ ] Review Contents/02-architecture/04-worker-node-components.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What components run on a worker node?" (file: Contents/02-architecture/04-worker-node-components.md)

**Contents/03-pods-and-namespaces/01-pod.md** — "What is a Pod?"

- 4.51 [ ] Write prose for `## Smallest deployable unit` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.52 [ ] Write prose for `## Single- vs. multi-container pods` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.53 [ ] Write prose for `## Shared network namespace (localhost between containers)` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.54 [ ] Write prose for `## Shared storage volumes within a pod` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.55 [ ] Write prose for `## Pod lifecycle & phases` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.56 [ ] Write prose for `## Ephemeral nature (pods are not durable identities)` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.57 [ ] Write prose for `## Each Pod gets its own (ephemeral) cluster-internal IP address` in Contents/03-pods-and-namespaces/01-pod.md (file: Contents/03-pods-and-namespaces/01-pod.md)
- 4.58 [ ] Review Contents/03-pods-and-namespaces/01-pod.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Pod?" (file: Contents/03-pods-and-namespaces/01-pod.md)

**Contents/03-pods-and-namespaces/02-labels-and-selectors.md** — "What are labels and selectors?"

- 4.59 [ ] Write prose for `## Key/value metadata on objects` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.60 [ ] Write prose for `## Used by Deployments & Services to match pods` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.61 [ ] Write prose for `## Arbitrary vs. well-known labels` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.62 [ ] Write prose for `## Selector expressions (equality vs. set-based)` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.63 [ ] Write prose for `## Labels vs. annotations` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.64 [ ] Write prose for `## Common labeling conventions (app, version, environment)` in Contents/03-pods-and-namespaces/02-labels-and-selectors.md (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)
- 4.65 [ ] Review Contents/03-pods-and-namespaces/02-labels-and-selectors.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What are labels and selectors?" (file: Contents/03-pods-and-namespaces/02-labels-and-selectors.md)

**Contents/03-pods-and-namespaces/03-namespace.md** — "What is a Namespace?"

- 4.66 [ ] Write prose for `## Logical partitioning of a cluster` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.67 [ ] Write prose for `## Environment separation (dev/staging/prod)` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.68 [ ] Write prose for `## Namespace-scoped vs. cluster-scoped resources` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.69 [ ] Write prose for `## Default namespace` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.70 [ ] Write prose for `## Resource quotas per namespace (brief mention)` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.71 [ ] Write prose for `## Naming & switching context with \`kubectl\`` in Contents/03-pods-and-namespaces/03-namespace.md (file: Contents/03-pods-and-namespaces/03-namespace.md)
- 4.72 [ ] Review Contents/03-pods-and-namespaces/03-namespace.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Namespace?" (file: Contents/03-pods-and-namespaces/03-namespace.md)

**Contents/04-kubectl/01-kubectl-basics.md** — "How do I interact with a cluster using `kubectl`?"

- 4.73 [ ] Write prose for `## cluster-info, namespaces, pods, logs, events` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.74 [ ] Write prose for `## Context & namespace switching` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.75 [ ] Write prose for `## \`kubectl get\` / \`describe\` / \`logs\` verbs` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.76 [ ] Write prose for `## \`kubectl apply -f\` / \`create\` / \`delete\` — creating and updating resources from manifests` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.77 [ ] Write prose for `## Output formats (-o wide/yaml/json)` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.78 [ ] Write prose for `## \`kubectl explain\` for discovering fields` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.79 [ ] Write prose for `## Interacting with kube-system components` in Contents/04-kubectl/01-kubectl-basics.md (file: Contents/04-kubectl/01-kubectl-basics.md)
- 4.80 [ ] Review Contents/04-kubectl/01-kubectl-basics.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How do I interact with a cluster using `kubectl`?" (file: Contents/04-kubectl/01-kubectl-basics.md)

**Contents/05-deployments/01-deployment-and-replicaset.md** — "What is a Deployment, and how does it relate to a ReplicaSet?"

- 4.81 [ ] Write prose for `## Deployment manages a ReplicaSet` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.82 [ ] Write prose for `## Declarative desired-state for Pods` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.83 [ ] Write prose for `## ReplicaSet ensures pod count matches spec` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.84 [ ] Write prose for `## Deployment adds versioned rollout history` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.85 [ ] Write prose for `## Relationship: Deployment → ReplicaSet → Pods` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.86 [ ] Write prose for `## When to use a bare ReplicaSet vs. a Deployment` in Contents/05-deployments/01-deployment-and-replicaset.md (file: Contents/05-deployments/01-deployment-and-replicaset.md)
- 4.87 [ ] Review Contents/05-deployments/01-deployment-and-replicaset.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Deployment, and how does it relate to a ReplicaSet?" (file: Contents/05-deployments/01-deployment-and-replicaset.md)

**Contents/05-deployments/02-scaling-and-self-healing.md** — "How does Kubernetes scale and self-heal Pods?"

- 4.88 [ ] Write prose for `## Scaling replica count` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.89 [ ] Write prose for `## Automatic pod replacement on failure` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.90 [ ] Write prose for `## Horizontal scaling via \`kubectl scale\`` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.91 [ ] Write prose for `## Readiness affects traffic routing` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.92 [ ] Write prose for `## Liveness probes trigger restarts (brief mention)` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.93 [ ] Write prose for `## Manual vs. automatic (HPA) scaling (brief mention)` in Contents/05-deployments/02-scaling-and-self-healing.md (file: Contents/05-deployments/02-scaling-and-self-healing.md)
- 4.94 [ ] Review Contents/05-deployments/02-scaling-and-self-healing.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How does Kubernetes scale and self-heal Pods?" (file: Contents/05-deployments/02-scaling-and-self-healing.md)

**Contents/05-deployments/03-rolling-updates-and-rollbacks.md** — "How do rolling updates and rollbacks work?"

- 4.95 [ ] Write prose for `## Gradual version replacement` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.96 [ ] Write prose for `## Reverting to a previous revision` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.97 [ ] Write prose for `## Rollout strategies (RollingUpdate vs. Recreate)` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.98 [ ] Write prose for `## maxSurge / maxUnavailable concept` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.99 [ ] Write prose for `## Pausing & resuming a rollout` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.100 [ ] Write prose for `## Viewing rollout history & status` in Contents/05-deployments/03-rolling-updates-and-rollbacks.md (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)
- 4.101 [ ] Review Contents/05-deployments/03-rolling-updates-and-rollbacks.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How do rolling updates and rollbacks work?" (file: Contents/05-deployments/03-rolling-updates-and-rollbacks.md)

**Contents/06-services-and-networking/01-service.md** — "What is a Service?"

- 4.102 [ ] Write prose for `## Stable virtual IP/DNS name` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.103 [ ] Write prose for `## Load balancing across matching pods` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.104 [ ] Write prose for `## Decoupling consumers from pod IP churn` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.105 [ ] Write prose for `## Service discovery via DNS` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.106 [ ] Write prose for `## Selector-based endpoint matching` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.107 [ ] Write prose for `## Headless services (brief mention)` in Contents/06-services-and-networking/01-service.md (file: Contents/06-services-and-networking/01-service.md)
- 4.108 [ ] Review Contents/06-services-and-networking/01-service.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Service?" (file: Contents/06-services-and-networking/01-service.md)

**Contents/06-services-and-networking/02-service-types.md** — "What types of Services are there?"

- 4.109 [ ] Write prose for `## ClusterIP` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.110 [ ] Write prose for `## NodePort` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.111 [ ] Write prose for `## LoadBalancer` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.112 [ ] Write prose for `## ExternalName (brief mention)` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.113 [ ] Write prose for `## Default type behavior` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.114 [ ] Write prose for `## When to choose which type` in Contents/06-services-and-networking/02-service-types.md (file: Contents/06-services-and-networking/02-service-types.md)
- 4.115 [ ] Review Contents/06-services-and-networking/02-service-types.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What types of Services are there?" (file: Contents/06-services-and-networking/02-service-types.md)

**Contents/06-services-and-networking/03-exposing-services.md** — "How do I expose a Service outside the cluster?"

- 4.116 [ ] Write prose for `## Host/path-based external routing` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.117 [ ] Write prose for `## Gateway API vs. Ingress` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.118 [ ] Write prose for `## TLS termination` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.119 [ ] Write prose for `## Single entrypoint for multiple services` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.120 [ ] Write prose for `## Ingress controller requirement` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.121 [ ] Write prose for `## Name-based virtual hosting` in Contents/06-services-and-networking/03-exposing-services.md (file: Contents/06-services-and-networking/03-exposing-services.md)
- 4.122 [ ] Review Contents/06-services-and-networking/03-exposing-services.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How do I expose a Service outside the cluster?" (file: Contents/06-services-and-networking/03-exposing-services.md)

**Contents/07-configuration-management/01-configmap.md** — "What is a ConfigMap?"

- 4.123 [ ] Write prose for `## Externalized non-sensitive configuration` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.124 [ ] Write prose for `## Env vars vs. mounted files` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.125 [ ] Write prose for `## Updating a ConfigMap without rebuilding images` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.126 [ ] Write prose for `## ConfigMap as command-line args source` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.127 [ ] Write prose for `## Immutable ConfigMaps (brief mention)` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.128 [ ] Write prose for `## Referencing a ConfigMap in a Pod spec` in Contents/07-configuration-management/01-configmap.md (file: Contents/07-configuration-management/01-configmap.md)
- 4.129 [ ] Review Contents/07-configuration-management/01-configmap.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a ConfigMap?" (file: Contents/07-configuration-management/01-configmap.md)

**Contents/07-configuration-management/02-secret.md** — "What is a Secret, and how does it differ from a ConfigMap?"

- 4.130 [ ] Write prose for `## Externalized sensitive data` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.131 [ ] Write prose for `## Access restrictions vs. ConfigMaps` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.132 [ ] Write prose for `## Base64 encoding vs. encryption (clarify: not encryption)` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.133 [ ] Write prose for `## Secret types (generic, docker-registry, tls)` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.134 [ ] Write prose for `## Mounting Secrets as files vs. env vars` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.135 [ ] Write prose for `## Least-privilege access considerations` in Contents/07-configuration-management/02-secret.md (file: Contents/07-configuration-management/02-secret.md)
- 4.136 [ ] Review Contents/07-configuration-management/02-secret.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Secret, and how does it differ from a ConfigMap?" (file: Contents/07-configuration-management/02-secret.md)

**Contents/08-access-control/01-rbac.md** — "What is RBAC (Role-Based Access Control)?"

- 4.137 [ ] Write prose for `## Roles / RoleBindings` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.138 [ ] Write prose for `## ClusterRoles / ClusterRoleBindings` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.139 [ ] Write prose for `## Subjects (users, groups, service accounts)` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.140 [ ] Write prose for `## Verbs & resources in a Role rule` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.141 [ ] Write prose for `## Namespace-scoped vs. cluster-scoped permissions` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.142 [ ] Write prose for `## Principle of least privilege` in Contents/08-access-control/01-rbac.md (file: Contents/08-access-control/01-rbac.md)
- 4.143 [ ] Review Contents/08-access-control/01-rbac.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is RBAC (Role-Based Access Control)?" (file: Contents/08-access-control/01-rbac.md)

**Contents/08-access-control/02-service-account.md** — "What is a Service Account?"

- 4.144 [ ] Write prose for `## Pod identity toward the API server` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.145 [ ] Write prose for `## Default vs. custom service accounts` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.146 [ ] Write prose for `## Automatic token mounting` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.147 [ ] Write prose for `## Binding a Role to a Service Account` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.148 [ ] Write prose for `## Use cases: CI/CD, Operators, in-cluster tooling` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.149 [ ] Write prose for `## Disabling auto-mount for security` in Contents/08-access-control/02-service-account.md (file: Contents/08-access-control/02-service-account.md)
- 4.150 [ ] Review Contents/08-access-control/02-service-account.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Service Account?" (file: Contents/08-access-control/02-service-account.md)

**Contents/09-storage-and-state/01-persistent-storage.md** — "How does Kubernetes handle persistent storage?"

- 4.151 [ ] Write prose for `## Volumes` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.152 [ ] Write prose for `## PersistentVolume / PersistentVolumeClaim` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.153 [ ] Write prose for `## StorageClass & dynamic provisioning (brief mention)` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.154 [ ] Write prose for `## Access modes (ReadWriteOnce, ReadWriteMany, etc.)` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.155 [ ] Write prose for `## Volume lifecycle vs. pod lifecycle` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.156 [ ] Write prose for `## emptyDir vs. persistent volumes` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.157 [ ] Write prose for `## Docker Desktop's default \`hostpath\` StorageClass (exercise environment)` in Contents/09-storage-and-state/01-persistent-storage.md (file: Contents/09-storage-and-state/01-persistent-storage.md)
- 4.158 [ ] Review Contents/09-storage-and-state/01-persistent-storage.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How does Kubernetes handle persistent storage?" (file: Contents/09-storage-and-state/01-persistent-storage.md)

**Contents/09-storage-and-state/02-statefulset.md** — "What is a StatefulSet?"

- 4.159 [ ] Write prose for `## Stable per-replica identity` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.160 [ ] Write prose for `## Ordered deployment & scaling` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.161 [ ] Write prose for `## Stable network identity per replica` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.162 [ ] Write prose for `## Stable storage per replica (via volumeClaimTemplates)` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.163 [ ] Write prose for `## Ordered, graceful termination` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.164 [ ] Write prose for `## Use cases: databases, distributed systems` in Contents/09-storage-and-state/02-statefulset.md (file: Contents/09-storage-and-state/02-statefulset.md)
- 4.165 [ ] Review Contents/09-storage-and-state/02-statefulset.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a StatefulSet?" (file: Contents/09-storage-and-state/02-statefulset.md)

**Contents/10-workload-patterns/01-daemonset.md** — "What is a DaemonSet?"

- 4.166 [ ] Write prose for `## One pod per (selected) node` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.167 [ ] Write prose for `## Use case: log/monitoring agents` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.168 [ ] Write prose for `## Node selectors/affinity for targeting` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.169 [ ] Write prose for `## Automatic scheduling on new nodes` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.170 [ ] Write prose for `## Comparison to Deployment (no fixed replica count)` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.171 [ ] Write prose for `## Update strategies for DaemonSets` in Contents/10-workload-patterns/01-daemonset.md (file: Contents/10-workload-patterns/01-daemonset.md)
- 4.172 [ ] Review Contents/10-workload-patterns/01-daemonset.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a DaemonSet?" (file: Contents/10-workload-patterns/01-daemonset.md)

**Contents/10-workload-patterns/02-init-container.md** — "What is an Init Container?"

- 4.173 [ ] Write prose for `## Run-to-completion before app containers` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.174 [ ] Write prose for `## Use case: setup/dependency waits` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.175 [ ] Write prose for `## Sequential execution order` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.176 [ ] Write prose for `## Separate image/resource profile from app container` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.177 [ ] Write prose for `## Failure handling (pod restart on init failure)` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.178 [ ] Write prose for `## Common patterns: schema migration, config generation` in Contents/10-workload-patterns/02-init-container.md (file: Contents/10-workload-patterns/02-init-container.md)
- 4.179 [ ] Review Contents/10-workload-patterns/02-init-container.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is an Init Container?" (file: Contents/10-workload-patterns/02-init-container.md)

**Contents/10-workload-patterns/03-sidecar-container.md** — "What is a Sidecar Container?"

- 4.180 [ ] Write prose for `## Auxiliary container in the same pod` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.181 [ ] Write prose for `## Use case: proxies, log shippers` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.182 [ ] Write prose for `## Shared network & volume with the main container` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.183 [ ] Write prose for `## Lifecycle coupling with the main container` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.184 [ ] Write prose for `## Native sidecar support (restartPolicy on init containers, brief mention)` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.185 [ ] Write prose for `## Examples: service mesh proxies, log forwarders` in Contents/10-workload-patterns/03-sidecar-container.md (file: Contents/10-workload-patterns/03-sidecar-container.md)
- 4.186 [ ] Review Contents/10-workload-patterns/03-sidecar-container.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a Sidecar Container?" (file: Contents/10-workload-patterns/03-sidecar-container.md)

**Contents/10-workload-patterns/04-operator.md** — "What is an Operator?"

- 4.187 [ ] Write prose for `## Custom controller + CRD` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.188 [ ] Write prose for `## Automates day-2 operational tasks` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.189 [ ] Write prose for `## Reconciliation loop pattern` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.190 [ ] Write prose for `## Encoding operational knowledge as code` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.191 [ ] Write prose for `## Examples: database operators, certificate operators` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.192 [ ] Write prose for `## Operator Framework / OperatorHub (brief mention)` in Contents/10-workload-patterns/04-operator.md (file: Contents/10-workload-patterns/04-operator.md)
- 4.193 [ ] Review Contents/10-workload-patterns/04-operator.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is an Operator?" (file: Contents/10-workload-patterns/04-operator.md)

**Contents/11-ci-cd/01-gitops.md** — "What is GitOps?"

- 4.194 [ ] Write prose for `## Git as source of truth` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.195 [ ] Write prose for `## Automated sync/reconciliation (conceptual)` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.196 [ ] Write prose for `## Pull-based vs. push-based deployment` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.197 [ ] Write prose for `## Declarative desired state stored in Git` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.198 [ ] Write prose for `## Drift detection & auto-correction` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.199 [ ] Write prose for `## Auditability via commit history` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.200 [ ] Write prose for `## Examples: Argo CD, Flux (brief mention)` in Contents/11-ci-cd/01-gitops.md (file: Contents/11-ci-cd/01-gitops.md)
- 4.201 [ ] Review Contents/11-ci-cd/01-gitops.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is GitOps?" (file: Contents/11-ci-cd/01-gitops.md)

**Contents/11-ci-cd/02-deployment-pipeline.md** — "How does a deployment pipeline work with Kubernetes?"

- 4.202 [ ] Write prose for `## Build → test → package → deploy` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.203 [ ] Write prose for `## Environment promotion (dev → staging → prod)` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.204 [ ] Write prose for `## Image tagging & versioning strategy` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.205 [ ] Write prose for `## Automated rollout triggers` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.206 [ ] Write prose for `## Rollback as part of the pipeline` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.207 [ ] Write prose for `## Separation of CI (build/test) and CD (deploy) concerns` in Contents/11-ci-cd/02-deployment-pipeline.md (file: Contents/11-ci-cd/02-deployment-pipeline.md)
- 4.208 [ ] Review Contents/11-ci-cd/02-deployment-pipeline.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "How does a deployment pipeline work with Kubernetes?" (file: Contents/11-ci-cd/02-deployment-pipeline.md)

**Contents/12-package-management/01-helm.md** — "What is Helm?"

- 4.209 [ ] Write prose for `## Package manager ("charts") for Kubernetes` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.210 [ ] Write prose for `## Install/upgrade/rollback as a unit` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.211 [ ] Write prose for `## Templating with values files` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.212 [ ] Write prose for `## Chart repositories` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.213 [ ] Write prose for `## Release versioning & history` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.214 [ ] Write prose for `## Managing multi-resource applications as one unit` in Contents/12-package-management/01-helm.md (file: Contents/12-package-management/01-helm.md)
- 4.215 [ ] Review Contents/12-package-management/01-helm.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is Helm?" (file: Contents/12-package-management/01-helm.md)

**Contents/12-package-management/02-kustomize.md** — "What is Kustomize?"

- 4.216 [ ] Write prose for `## Overlay-based YAML customization` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.217 [ ] Write prose for `## Built into \`kubectl -k\`` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.218 [ ] Write prose for `## Base + overlay pattern` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.219 [ ] Write prose for `## Patches vs. templating (Kustomize vs. Helm)` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.220 [ ] Write prose for `## Environment-specific overlays (dev/staging/prod)` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.221 [ ] Write prose for `## No templating language required` in Contents/12-package-management/02-kustomize.md (file: Contents/12-package-management/02-kustomize.md)
- 4.222 [ ] Review Contents/12-package-management/02-kustomize.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is Kustomize?" (file: Contents/12-package-management/02-kustomize.md)

**Contents/13-service-mesh/01-service-mesh.md** — "What is a service mesh, and why would I need one?"

- 4.223 [ ] Write prose for `## Service-to-service traffic layer (routing, retries, mTLS)` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.224 [ ] Write prose for `## Examples: Istio, Traefik Mesh` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.225 [ ] Write prose for `## Sidecar proxy pattern` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.226 [ ] Write prose for `## Observability (traffic metrics, tracing)` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.227 [ ] Write prose for `## Traffic splitting / canary routing` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.228 [ ] Write prose for `## When a service mesh is (not) needed` in Contents/13-service-mesh/01-service-mesh.md (file: Contents/13-service-mesh/01-service-mesh.md)
- 4.229 [ ] Review Contents/13-service-mesh/01-service-mesh.md: subheading consistency/style; fit of each subheading and the whole file for the workshop (scope/audience/non-goals per CLAUDE.md) and for its topic "What is a service mesh, and why would I need one?" (file: Contents/13-service-mesh/01-service-mesh.md)

## Phase 5 — Planning (done in Claude Project chat)

- 5.1 [ ] Review Phase 1/2/4 output (Contents.md + finished lesson content); update CLAUDE.md/.claude/STYLE.md if needed
- 5.2 [ ] Add detailed Phase 6 tasks (5.x → 6.x) to this file, analogous to Phase 1's tasks but for Practices.md

## Phase 6 — Execution (Claude Code agent, this repo) — Practices.md topic list

_Tasks added during Phase 5 planning, once Contents.md and its lesson content from Phase 1/2/4 are final._

## Phase 7 — Planning (done in Claude Project chat)

- 7.1 [ ] Review Phase 6 output (Practices.md); update CLAUDE.md/.claude/STYLE.md if needed
- 7.2 [ ] Add detailed Phase 8 tasks (7.x → 8.x) to this file, analogous to Phase 2's tasks but for exercise/solution files

## Phase 8 — Execution (Claude Code agent, this repo) — Practices.md exercise content

_Tasks added during Phase 7 planning, once Practices.md from Phase 6 is final._
