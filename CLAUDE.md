---
revision: 11
path: "CLAUDE.md"
title: "CLAUDE.md"
abstract: "Guidance for the Claude Code agent that builds the GFT Kubernetes Workshop content and exercises in this repository."
state: in progress
lang: en
numbersections: true
current_phase: 1
finished_sections: [ ]
history:
  - "v1 (preliminary): initial description of repository purpose, phase model and file styleguide"
  - "v2: added workshop scope and non-goals, fixed frontmatter inconsistencies (state enum, missing abstract), clarified task-file locations and task format, added current_phase tracking"
  - "v3: confirmed Contents/<nr>-<section>/<nr>-<lesson>.md as binding folder convention; .claude/TASKS.md now created in Phase 1 (not Phase 3); Phase 1 deliverables complete, current_phase advanced to 2"
  - "v4: consolidated all per-phase task lists into a single .claude/TASKS.md; replaced [TODO]/[DONE] task format with the five-state model ([ ]/[~]/[R]/[B]/[X]), task selection algorithm and blocker documentation policy"
  - "v5: confirmed [!] exception maps to [B]; replaced Recherche-based blocker documentation with a two-tier Memory structure (.claude/Memory.md global, Contents/<nr>-<section>/Memory.md per module); .claude/Memory.md added as a Phase 1 deliverable"
  - "v6: renumbered phases — harness generation is now Phase 0 (was Phase 1); workshop-structure generation is now Phase 1 (was Phase 2); all subsequent phases shifted down by one (superseded by v7)"
  - "v7: split former Phase 1 into Phase 1 (Eckpunkte) and Phase 2 (verbose fill-in) (superseded by v8)"
  - "v8: replaced the Eckpunkte/verbose-fill model with a per-file workflow: Phase 1-2 fully process Contents.md (topic list, then folders/lesson files/content/links), Phase 3 plans Phase 4, Phase 4-6 do the analogous work for Practices.md. Dropped the Part 1/Part 2 split from all automated phases (kept only as background info, finalized manually by the workshop author after Phase 6). README.md is out of scope for phases 0-6. Exercise/solution file naming changed to <nr>.<subnr>-<practice>.md / <nr>.<subnr>-<solution>.md."
  - "v9: added Follow-up Refinement Subtasks convention to Task Definition — records content/formatting follow-up prompts issued after a task's completion as <phase>.<sequence>.<subsequence> subtasks, consolidating related small prompts and excluding tooling/process prompts."
  - "v10: Added 'path' to the header of md-files."
  - "v11: Follow-up Refinement Subtasks are now scoped to changes executed via the `/improve` skill (`.claude/skills/improve/`); ad-hoc follow-up prompts outside the skill are still carried out but no longer logged as subtasks."
---

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not a software project** — it is the content source for a Kubernetes workshop for developers with no prior Kubernetes experience (GFT DevOps Community). There is no application code, no build system, no tests, and no linter. Work here consists of writing and refining course material.

`CLAUDE.md` and `.claude/TASKS.md` are produced and maintained in a separate planning session (a Claude Project chat) and handed to the Claude Code agent working in this repository. Claude Code should treat this file — and the tasks it currently points to in `.claude/TASKS.md` — as the authoritative brief for what to produce next, not as something to redesign on its own initiative.

## Language and audience conventions

- Language of all files and content is English. Propose translations if you find German text.
- The audience has no Kubernetes experience but is technical (developers, DevOps/SysOps/SRE, testers) and is assumed to already know Docker/container basics (CLI, images). Keep explanations conceptual-first with a concrete `kubectl`/exercise immediately after — this is the pattern used throughout `Contents.md` (concept section followed by a "Practice: ..." section).

# Workshop Scope

- **Structure**: two parts — a mandatory introduction (~4h) and an optional deep-dive (~4h: StatefulSet, RBAC, Storage, …). **Not handled by phases 0–6** — this split is applied manually by the workshop author after all content and exercises exist.
- **Focus**: concepts *within* Kubernetes (Pods, Deployments, Services, Config, …). Underlying infrastructure (nodes, networking, storage backends) is mentioned briefly, not taught in depth.
- **Prerequisites**: Docker/container basics (CLI, images). No prior Kubernetes knowledge assumed.
- **Target Kubernetes version**: whatever ships with Docker Desktop's built-in Kubernetes (currently kubeadm-based, single-node).
- **Exercise environment**: Kubernetes as bundled with Docker Desktop. No cloud cluster, no Rancher-specific features.
- **Artifact format**: Markdown for all content and exercise files.

# Non-Goals

- No infrastructure/cluster-ops deep dive (networking internals, storage classes, cluster provisioning).
- No cloud-provider-specific content (EKS/GKE/AKS particulars) — content stays generic/portable.
- No CI/CD tool-specific implementation — CI/CD is covered conceptually only.
- No production-hardening / security deep-dive beyond what's covered in the optional deep-dive part.

# Folder & File Conventions

- Topic list (which concepts are covered, no prose): `Contents.md`
- Exercise list (which exercises are covered, no prose): `Practices.md`
- Actual lesson content: `Contents/<nr>-<section>/<nr>-<lesson>.md`
- Exercises: `Contents/<nr>-<section>/<nr>.<subnr>-<practice>.md`
- Solutions: `Contents/<nr>-<section>/<nr>.<subnr>-<solution>.md`
- Module-scoped memory: `Contents/<nr>-<section>/Memory.md` (see Memory Structure below)
- Project-wide task backlog: `.claude/TASKS.md`
- Project-wide memory: `.claude/Memory.md` (see Memory Structure below)
- `<nr>-<section>` folder slugs are assigned once in Phase 1 and must not change afterwards. Phase 2 creates the folders/lesson files and fills lesson content; Phase 6 adds exercise/solution files inside the existing folders — no new folders are created in Phase 6.
- `README.md` is **out of scope** for phases 0–6; it is maintained manually by the workshop author, together with the Part 1/Part 2 split.

# Process / Phases

Work proceeds in seven sequential phases (0–6): a one-time harness setup (Phase 0), then two parallel per-file passes — one for `Contents.md` (Phases 1–2), one for `Practices.md` (Phases 3–6, with Phase 3 as its planning step):

| Phase | Type | Produces |
|---|---|---|
| 0 | Planning (harness, chat) | `CLAUDE.md`, `.claude/TASKS.md`, `.claude/Memory.md` (seed) |
| 1 | Execution (repo) | `Contents.md` — decide which topics are covered (e.g. "What is a Pod?", "What is a Service?"). Headings + bullet points only, no explanatory prose, no per-lesson files yet. |
| 2 | Execution (repo) | Create `Contents/<nr>-<section>/` folders + dummy `<nr>-<lesson>.md` stubs per `Contents.md`; fill in the actual lesson content; update `Contents.md` to link each topic to its lesson file. |
| 3 | Planning (chat) | `CLAUDE.md` (if needed), `.claude/TASKS.md` — add detailed Phase 4 tasks, based on the finished `Contents.md` and lesson content |
| 4 | Execution (repo) | `Practices.md` — decide which exercises are covered, analogous to Phase 1. Headings + bullet points only, no exercise description yet. |
| 5 | Planning (chat) | `CLAUDE.md` (if needed), `.claude/TASKS.md` — add detailed Phase 6 tasks, based on the finished `Practices.md` |
| 6 | Execution (repo) | Create dummy `<nr>.<subnr>-<practice>.md` / `<nr>.<subnr>-<solution>.md` files inside the existing module folders per `Practices.md`; fill in the actual exercise/solution content; update `Practices.md` to link each exercise to its file. |

Notes:
- `current_phase` in this file's frontmatter tracks the active phase. Claude Code reads this before doing anything else, instead of inferring it from prose.
- `.claude/TASKS.md` is the single, cumulative task file for the whole project, grouped by phase (see Task Definition below). It is created once, in Phase 0, and extended — never rewritten from scratch — during each subsequent planning phase.
- Phases 1 and 2 run back-to-back with **no intervening Planning phase** — Phase 2 is largely mechanical once Phase 1's topic list exists, so its tasks are pre-defined in Phase 0. Phases 4 and 6, by contrast, each get a dedicated Planning phase (3 and 5) beforehand, since Practices.md's structure can only be meaningfully planned once the corresponding lesson content exists.
- The task-selection algorithm below applies to the Claude Code agent during execution phases (1, 2, 4, 6). Planning-phase tasks (0, 3, 5) are carried out in the separate Claude Project chat and marked `[X]` there directly.
- During an execution phase, the overall structure (module list, ordering, folder slugs) must not change — only content within the fixed structure is added.

# Styleguide

## Frontmatter for generated `.md` files

    ---
    revision: <int, starts at 1, incremented on every regenerated version>
    path: <path to the file>
    title: "<title>"
    abstract: "<one-sentence description>"
    state: <not started|in progress|done>
    lang: en
    numbersections: true
    finished_sections: [ ]
    history: [ ]
    ---

Rules:
- `state` must be exactly one of `not started`, `in progress`, `done` — no other values.
- On regeneration: increment `revision`; move `state` from `not started` to `in progress`. Claude Code never sets `done` — that's set manually by the workshop author.
- When a section is finished, append it to `finished_sections`.
- Append one entry to `history` per regenerated version, summarizing what changed.

## Task Definition (`.claude/TASKS.md`)

All tasks across all phases live in the single file `.claude/TASKS.md`, grouped by phase, numbered `<phase>.<sequence>` (e.g. `2.3` = Phase 2, third task), so numeric order and phase order coincide. Follow-up refinement work on an already-completed task is recorded separately as a subtask — see Follow-up Refinement Subtasks below.

### Status values

- `[ ]` **Open** — task not yet worked on.
- `[~]` **In Progress** — task started but not yet complete.
- `[R]` **Needs Rework** — task must be reworked due to changed information or review feedback.
- `[B]` **Blocked** — task cannot be completed right now. The blocker must be documented in the relevant `Memory.md` (see Memory Structure below), with a one-line pointer as a sub-bullet under the task in `.claude/TASKS.md`.
- `[X]` **Done** — task is approved (if review-required) or fully completed (if not review-required).

### Allowed status transitions (Claude Code agent)

- `[ ]` → `[~]` when work begins.
- `[R]` → `[~]` when rework begins.
- `[~]` → `[X]` after full completion of a task that is not subject to review.
- `[~]` → `[B]` when a blocker occurs.
- `[B]` → `[~]` only if the blocker is resolved with new information within the same run.
- `[X]` must never be reset by the agent.
- `[R]` is set only by the user or via an explicit review decision — the agent may not set it itself, it may only *recommend* resetting a task to `[R]`.

### Task selection algorithm

When asked to work through `.claude/TASKS.md`, the agent:

1. reads `.claude/TASKS.md`;
2. finds the first task in numeric order with status `[ ]` or `[R]`;
3. checks whether an earlier task has status `[ ]`, `[R]`, `[~]`, or `[B]`;
4. if yes — works exclusively on that earlier task, or documents why it's blocked (full detail in the relevant `Memory.md`, one-line pointer as a sub-bullet under the task in `.claude/TASKS.md`), and gives the user a clear status update: task number, reason, recommended next step;
5. if no — works on the found task and stops once it is completed or blocked.

A later task may only be started once all earlier tasks have status `[X]`. Exception: the user explicitly instructs the agent to review a task currently marked `[B]`, or to set it to `[X]`.

### Task granularity

One task = one file or one clearly bounded edit. Avoid tasks like "write Contents.md" for an entire file — split per section/module. Tasks name the target file path so Claude Code doesn't have to infer it.

### Follow-up Refinement Subtasks

A task in `[X]` state can still receive follow-up refinement in the same session, via the `/improve <prompt>` skill (`.claude/skills/improve/SKILL.md`). The skill drafts a plan against the reference task's output, gets it reviewed, and — once approved as drafted or after the user's own manual edits — applies the change directly. **Only refinements executed through `/improve` are recorded as Follow-up Refinement Subtasks.** Ad-hoc follow-up prompts issued outside the skill are still carried out as requested, but are not logged as subtasks. This refinement work is recorded as a subtask numbered `<phase>.<sequence>.<subsequence>` (e.g. `1.1.1`, `1.1.2` for two `/improve` runs on task `1.1`).

Rules:
- Only prompts run through `/improve` **and** concerning the **content or formatting of the workshop material** are recorded (e.g. "improve wording", "restructure this section", "add a missing bullet point"). Prompts about tooling/process (e.g. `git commit`, environment setup, unrelated questions) are **not** recorded, even if run through `/improve`.
- Several small, closely related `/improve` prompts are consolidated into a **single** subtask entry summarizing the resulting change — not one subtask per literal prompt.
- Subtasks document work already completed, so they are logged directly as `[X]` (no intermediate `[ ]`/`[~]` state).
- Subtasks are nested directly under their parent task in `.claude/TASKS.md`, e.g.:

      - 1.1 [X] Produce a definitive topic list ... (file: Contents.md)
        - 1.1.1 [X] Reworded topic questions for consistency with the audience's terms
        - 1.1.2 [X] Merged two overlapping topics into one, per review feedback
- Subtasks do not participate in the task-selection algorithm above (which only considers top-level `<phase>.<sequence>` tasks); they exist purely as a record of iterative refinement.

## Memory Structure (`Memory.md`)

Purpose: give the agent the minimal context needed to work a task **consistently with previously completed tasks** — not a full history or diary. Only what would otherwise be lost or ambiguous belongs here; everything already visible in the produced file itself or in `CLAUDE.md` does not.

Two levels:
- **Global** — `.claude/Memory.md`: cross-cutting decisions/conventions relevant across the whole project (e.g. the module numbering scheme, terminology choices, how Practices.md topics were mapped to Contents.md modules). Read before, and updated after, tasks that span multiple modules or files (mainly Phase 1 and Phase 4, plus Phase 3/5 planning).
- **Per module** — `Contents/<nr>-<section>/Memory.md`: context scoped to one module (learning objectives already fixed, terminology used in that module, prerequisites established, deviations from the module template). Read before, and updated after, tasks scoped to a single module (mainly Phase 2 and Phase 6). Created the first time a task touches that module.

Rules:
- Before starting a task, the agent reads `.claude/Memory.md`, plus the module's `Memory.md` if the task is module-scoped.
- After finishing or blocking a task, the agent appends at most a few bullet points — only genuinely new, load-bearing context.
- `Memory.md` files hold *current* state, not an append-only diff log — if a fact becomes obsolete, replace it rather than leaving contradictory entries.
- Blocker entries include: what's blocking, why, what's needed to unblock.
