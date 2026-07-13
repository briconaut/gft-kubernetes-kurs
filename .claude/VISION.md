---
revision: 1
path: ".claude/VISION.md"
title: "Workshop Vision"
abstract: "Distilled content guardrails for the Kubernetes workshop, summarized from Original/"
state: in progress
lang: en
numbersections: false
finished_sections: [ ]
history:
  - "v1: initial build from Original/"
  - "v2: added more rancher details"
---

## Content Guardrails

### Role and purpose

- Acting as a Kubernetes expert trainer building a workshop to teach a technical-minded audience the basics of Kubernetes.
- This repository is the content *source* for the workshop, not a software project — no application code, build system, tests, or linter. The work is writing and refining course material.

### Language

- All files and content are in English.
- Any non-English input material is translated to English automatically.

### Audience

- Technical persons: developers, DevOps/SysOps/SRE, testers.
- Prior knowledge assumed: basic Docker/container knowledge (CLI, images, Docker Swarm, Docker Compose) and basic shell (bash) knowledge.
- No prior Kubernetes knowledge assumed.
- Explanations should be conceptual-first.

### Workshop structure

- Two parts:
  - A **mandatory introduction** (~4 hours).
  - An **optional deep-dive** (~4 hours), covering topics such as StatefulSet, RBAC, and Storage.
- Draft section flow found in the source material (mandatory-part shape, roughly in teaching order):
  1. Container orchestration — introduction & motivation (what containers are, why orchestration).
  2. Kubernetes architecture: Control Plane (API Server, Controller Manager, Scheduler, etcd) and Worker Nodes (kubelet, kube-proxy); cluster/node/networking/data-storage mentioned only briefly.
  3. Key concepts: Pods (+ container runtime, single- vs. multi-container pods), Namespaces.
  4. `kubectl` as the CLI for Kubernetes: cluster-info, namespaces, pods, logs, events.
  5. Deployments: deployment types, replicas, rolling updates/rollback framing.
  6. Services & kube-proxy: labels/selectors, service types (NodePort, Ingress, Gateway, LoadBalancer), Ingress-vs-Gateway-API distinction.
  7. Configuration: ConfigMaps and Secrets, separating config/sensitive data from images.
- Deep-dive/optional-part topics found in the source material: rights management / RBAC, service accounts, persistence, StatefulSet, DaemonSet, Init containers, Sidecar containers, Operators, CI/CD (conceptual), Helm and Kustomize (deployment templating), and — as an extension topic beyond the core list — service mesh (e.g. Istio).

### Scope and depth

- Focus stays on concepts *within* Kubernetes (Pods, Deployments, Services, Configuration, …).
- Underlying infrastructure (nodes, networking, storage backends) is mentioned briefly, not taught in depth.
- CI/CD is covered conceptually only, not via a specific tool's implementation details.
- Production-hardening / security is only covered in depth within the optional deep-dive part (e.g. RBAC).
- Cloud-provider-specific content (EKS/GKE/AKS particulars) is out of scope; content stays generic/portable.

### Exercise environment

- Kubernetes as bundled with Docker Desktop (currently kubeadm-based, single-node cluster).
  Alternatively Kubernetes as bundled with Rancher Desktop.
- No cloud cluster.
- Setup involves activating Kubernetes in the Docker Desktop GUI (or Rancher Desktop GUI), installing `kubectl` (e.g. via `winget`/`chocolatey`), and working from Git Bash; `~/.kube/config` is the resulting/default kubeconfig location, with `KUBECONFIG` usable to switch configs for multiple clusters.
- Draft exercise flow found in the source material: local cluster setup and first `kubectl` commands (`cluster-info`, `get nodes`, `describe node`, `get namespaces`, `get pods -n kube-system`) → deploying containers into the cluster and inspecting/deleting pods → deployment with a Service (2 replicas, NodePort/Gateway) → deployment with ConfigMap and Secret.
- Exercise material references example images from the "Kubernetes in Action, 2nd Edition" book/repo.

### Artifact format

- Markdown for all content and exercise files.

### Non-goals

- No infrastructure/cluster-ops deep dive (networking internals, storage classes, cluster provisioning).
- No cloud-provider-specific content.
- No CI/CD tool-specific implementation.
- No production-hardening / security deep-dive beyond what's covered in the optional deep-dive part.
- No Rancher-exclusive features — the exercise environment is limited to the Docker compatibility of Rancher and the Kubernetes features of either Docker Desktop or Rancher Desktop.

### Supporting terminology / reference material

- A `kubectl` command reference exists among the source material, grouped by task: basic commands (`get`, `describe`, `apply`, `create`), managing pods/deployments (`delete`, `logs`, `exec`, `scale`), configuring/managing namespaces (`config`, namespace create/delete/list), and advanced commands (`rollout status`/`undo`, `cordon`/`uncordon`, `drain`). Useful as raw command-coverage input for the `kubectl` topic and any CLI cheat-sheet material, not as a prescribed lesson structure.
- Helm usage shown at a basic-command level (`helm install`, `helm get manifest`, `helm uninstall`, `helm list`) — consistent with "deployment templates" being covered as a topic, without implying deep tool-specific CI/CD coverage.

## Notes

Contradictions found between `Original/Vision.md` (authoritative) and other files in `Original/`, resolved in favor of `Original/Vision.md`:

- **Workshop duration**: `Original/README.md` states the workshop duration as a single "4 hours," which conflicts with `Original/Vision.md`'s two-part structure (mandatory ~4h introduction plus an optional ~4h deep-dive). Resolved in favor of `Original/Vision.md`: the workshop is two-part, with the deep-dive being optional additional time, not included in a flat 4-hour figure.
- **Rancher as exercise environment**: `Original/README.md` lists "Rancher or Docker Desktop installed" as a prerequisite/installation option, which conflicts with `Original/Vision.md`'s explicit "no cloud cluster, no Rancher-specific features" and "Kubernetes as bundled with Docker Desktop." `Original/Practices.md`'s actual setup instructions independently use Docker Desktop only, supporting this resolution. Resolved in favor of `Original/Vision.md`: the exercise environment is Docker Desktop's built-in Kubernetes only.
- **Audience breadth**: `Original/README.md` tentatively broadens the audience with "(also for business consultants?)", which conflicts with `Original/Vision.md`'s narrower "technical persons (developers, DevOps/SysOps/SRE, testers)." Resolved in favor of `Original/Vision.md`: the audience stays technical-only.

## Source Files

| Path | MD5 |
|---|---|
| Original/Contents.qmd | D057EEA503DFA29836D77EAC5A0DECB2 |
| Original/Practices.md | 91D82520F004190AAD2BB7FCAE9F168E |
| Original/README.md | 5B04DBEEC07A5E36F1D49B51E5BE1A96 |
| Original/Vision.md | 7157F268024FC29EF5F50A2BC79EF8F6 |
| Original/kubectl.md | 9D60FFD0B9953333DE2E8BF1F7F24D24 |
