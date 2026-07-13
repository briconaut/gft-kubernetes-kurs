---
revision: 7
path: ".claude/Memory.md"
title: "Project Memory"
abstract: "Cross-cutting decisions and conventions needed for consistency across tasks. Minimal by design — see CLAUDE.md > Memory Structure for scope and update rules."
state: in progress
lang: en
numbersections: false
finished_sections: [ ]
history:
  - "v1: seeded, empty — populated as Phase 2+ tasks make cross-cutting decisions"
  - "v2: added task 1.4 entry — how the old Contents.qmd draft's structure was reused/deviated from in Contents.md, incl. section mapping, dropped/added topics, and a missing diagram asset"
  - "v3: fixed `path` frontmatter field (was \".claude/MEMORY.md\", wrong case, now \".claude/Memory.md\") per header-completeness check"
  - "v4: added cross-cutting entry for the folder/lesson-file numbering convention introduced in Tasks 1.3/1.3.1 (`folder:`/`lesson:` HTML comments in Contents.md), so Phase 2 knows where to find and how to interpret it"
  - "v5: condensed the 'Folder & lesson-file numbering convention' entry into a pointer to `.claude/STYLE.md` → Format of Contents.md, where the rule is now documented as binding style (previously duplicated here almost verbatim). This also fixes a stale reference to 'Phase 6' for exercise naming, which should have read 'Phase 8' after the CLAUDE.md v14 phase renumbering and was missed at the time."
  - "v6: added the 'Review Notes' section (per .claude/skills/review/SKILL.md) and its first entry, for the manually-edited Contents/01-introduction/01-container-orchestration.md / '## Automated scheduling & placement'"
  - "v7: added second Review Notes entry, for the manually-edited Contents/01-introduction/01-container-orchestration.md / '## Desired-state reconciliation' — confirms the no-blank-line-between-sentences habit and notes a tendency toward redundant trailing example sentences"
---

# Project Memory

Entries are added here only when a decision or convention from one task is needed to keep a later task consistent — not a running log of everything done.

## How the old Contents.md draft was reused/deviated from (Task 1.4)

- The intial draft is `Original/Contents.qmd` — a Quarto/LaTeX-PDF narrative doc, not the current `Contents.md`. It was inspiration only, not binding.
- **Section order/topics mostly reused**, but format was not: draft was prose with `##` narrative subsections; current `Contents.md` is a flat headings+bullets list, split further into audience-facing `##` questions (task 1.2).
- **Section mapping, old → new**:
  - "Core Components of Kubernetes / Kubernetes-Architecture" (Control Plane + Worker Nodes prose) → `02-architecture`, split into 4 granular question-topics.
  - "Key Concepts" (Pods + Container-Runtime, Namespaces) → `03-pods-and-namespaces`; added "What are labels and selectors?" as a new topic (not in draft at all, needed as a prerequisite for later Deployments/Services topics).
  - "`kubectl` – CLI für Kubernetes" (German title) → `04-kubectl`, translated to English per Language conventions.
  - "Additional/Advanced Concepts" (flat list incl. German "Rechte-Management", Service-Accounts, Persistence, StatefulSet, DaemonSet, Init-Container, Sidecar, Operators) was **split into three top-level sections**: `08-access-control` (RBAC + Service Account; "Rechte-Management" translated to "RBAC"), `09-storage-and-state` (Storage + StatefulSet), `10-workload-patterns` (DaemonSet, Init Container, Sidecar, Operator). This split anticipates the mandatory/optional Part 1/Part 2 divide from CLAUDE.md → Workshop Scope, but **no mandatory/optional tagging exists yet** — that split is still manual/future work by the workshop author.
- **Entirely new topics, not present in the draft at all**: "How is Kubernetes different from plain Docker?" (bridges the assumed Docker prerequisite explicitly), "What is GitOps?" (draft's "# CI / CD" heading was empty), the Docker Desktop `hostpath` StorageClass bullet, and the `kubectl apply/create/delete` bullet (draft's kubectl list only had read-only verbs: cluster-info/namespaces/pods/logs/events).
- **Dropped from the draft**: all inline explanatory prose and links (e.g. the Ingress-vs-Gateway-API blog link under the old Services section) — `Contents.md` keeps only the original 4 links under "Further Reading / Links". Such supplementary links can be reintroduced in Phase 4 lesson content if useful there.
- **Diagram assets**: the draft referenced two SVGs. Only `.media/components-of-kubernetes.svg` still exists in the repo; `KubernetesConcepts.svg` (used for the old Pods/Namespaces section) is missing. Phase 4 either needs a replacement diagram for `03-pods-and-namespaces` or should proceed without one.
