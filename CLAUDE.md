---
revision: 15
path: "CLAUDE.md"
title: "CLAUDE.md"
abstract: "Guidance for the Claude Code agent that builds the GFT Kubernetes Workshop content and exercises in this repository."
state: in progress
lang: en
numbersections: true
current_phase: 2
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
  - "v12: Phase 1 complete (all tasks [X] per TASKS.md v13), advanced current_phase to 2. Clarified Folder & File Conventions: the lesson-file `<nr>` is a per-section counter restarting at 01, independent of the section folder's own `<nr>` — previously both used the same `<nr>` token, which was ambiguous. Made explicit that Phase 2 must take exact paths from the `<!-- folder: ... -->` / `<!-- lesson: ... -->` HTML comments in Contents.md verbatim, not re-derive numbering from heading order."
  - "v13: added new Styleguide subsection 'Lesson File Body Format (Phase 2)' — fixes the exact body structure of lesson files (H1 = section/topic title, `## Overview` as a linked table of contents, one `## <bullet>` heading per Contents.md bullet with explanatory prose), including the anchor-slug rule for Overview links; task 2.3 now references this section instead of the vague 'fill in actual lesson content' phrasing."
  - "v14: renumbered the phase model from 7 phases (0–6) to 9 phases (0–8), per user correction — Phase 2 no longer fills lesson-file prose. Former Phase 2 split into Phase 2 (folders + lesson-file skeletons: H1, linked Overview, empty bullet headings with a placeholder) and Phase 4 (fill in the actual prose beneath those headings), with a new Phase 3 planning step in between. Former Phases 3–6 (Practices.md planning/topic-list/planning/exercise-content) shifted to Phases 5–8. Updated Folder & File Conventions, Process/Phases table and notes, Lesson File Body Format (now spans Phases 2 & 4, added `_Content pending (Phase 4)._` placeholder convention), and Memory Structure phase references accordingly. current_phase stays 2 — effectively unchanged, now more narrowly scoped to skeleton creation only."
  - "v15: moved all file-format styleguides (Frontmatter for generated .md files, Lesson File Format) out of this file into the new `.claude/STYLE.md`, plus a newly consolidated 'Format of Contents.md' section (previously scattered across this file's Process/Phases table and .claude/Memory.md). Styleguide section here now only covers Task Definition and Memory Structure (process-facing formats, not generated-content formats) and points to `.claude/STYLE.md` for the rest. Folder & File Conventions and the Process/Phases table now reference `.claude/STYLE.md` instead of restating format details."
---

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not a software project** — it is the content source for a Kubernetes workshop for developers with no prior Kubernetes experience (GFT DevOps Community). There is no application code, no build system, no tests, and no linter. Work here consists of writing and refining course material.

`CLAUDE.md` and `.claude/TASKS.md` are produced and maintained in a separate planning session (a Claude Project chat) and handed to the Claude Code agent working in this repository. Claude Code should treat this file — and the tasks it currently points to in `.claude/TASKS.md` — as the authoritative brief for what to produce next, not as something to redesign on its own initiative.

## Language and audience conventions

- Language of all files and content is English. Propose translations if you find German text.
- The audience has no Kubernetes experience but is technical (developers, DevOps/SysOps/SRE, testers) and is assumed to already know Docker/container basics (CLI, images). Keep explanations conceptual-first with a concrete `kubectl`/exercise immediately after — this is the pattern used throughout `Contents.md` (concept section followed by a "Practice: ..." section; exact structure in `.claude/STYLE.md` → Format of Contents.md).

# Workshop Scope

- **Structure**: two parts — a mandatory introduction (~4h) and an optional deep-dive (~4h: StatefulSet, RBAC, Storage, …). **Not handled by phases 0–8** — this split is applied manually by the workshop author after all content and exercises exist.
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

- Topic list (which concepts are covered, no prose): `Contents.md` — exact structure and formatting rules in `.claude/STYLE.md` → Format of Contents.md.
- Exercise list (which exercises are covered, no prose): `Practices.md`
- Actual lesson content: `Contents/<nr>-<section>/<local-nr>-<lesson>.md`
  - `<nr>` (folder) is the section's global slug number, assigned once in Phase 1 (`01`–`13`).
  - `<local-nr>` (file) is a **separate, per-section counter that restarts at `01` in every section** — it is *not* the same number as the folder's `<nr>`.
  - The exact, authoritative path for every lesson file is fixed by its `<!-- lesson: Contents/<nr>-<section>/<local-nr>-<lesson>.md -->` HTML comment in `Contents.md` (added in Task 1.3.1). Phase 2 must copy these paths verbatim (e.g. via `grep` for `folder:`/`lesson:`) rather than re-deriving numbering from heading order or from the pattern shown here.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Lesson File Format.
- Exercises: `Contents/<nr>-<section>/<nr>.<subnr>-<practice>.md`
  - Here `<nr>` is the section's own folder number (same as above) and `<subnr>` a per-section exercise counter — a dot-separated scheme, deliberately distinct from the lesson-file scheme above. Assigned during Phase 7 planning, analogous to how `folder:`/`lesson:` comments are assigned in Phase 1.
- Solutions: `Contents/<nr>-<section>/<nr>.<subnr>-<solution>.md` (same numbering as its matching exercise).
- Module-scoped memory: `Contents/<nr>-<section>/Memory.md` (see Memory Structure below)
- Project-wide task backlog: `.claude/TASKS.md`
- Project-wide memory: `.claude/Memory.md` (see Memory Structure below)
- Format specifications for generated content files: `.claude/STYLE.md`
- `<nr>-<section>` folder slugs and lesson `<local-nr>` values are assigned once in Phase 1 and must not change afterwards. Phase 2 creates the folders and the lesson-file skeletons (structure only); Phase 4 fills in the lesson content within that fixed structure; Phase 8 adds exercise/solution files inside the existing folders — no new folders are created in Phase 8.
- `README.md` is **out of scope** for phases 0–8; it is maintained manually by the workshop author, together with the Part 1/Part 2 split.

# Process / Phases

Work proceeds in nine sequential phases (0–8): a one-time harness setup (Phase 0), then two parallel per-file passes — one for `Contents.md` (Phases 1–4), one for `Practices.md` (Phases 5–8, with Phase 5 as its planning step):

| Phase | Type | Produces |
|---|---|---|
| 0 | Planning (harness, chat) | `CLAUDE.md`, `.claude/TASKS.md`, `.claude/Memory.md` (seed) |
| 1 | Execution (repo) | `Contents.md` — decide which topics are covered (e.g. "What is a Pod?", "What is a Service?"), no per-lesson files yet. Format: `.claude/STYLE.md` → Format of Contents.md. |
| 2 | Execution (repo) | Create `Contents/<nr>-<section>/` folders + lesson-file **skeletons** (structure only, no prose); update `Contents.md` to link each topic to its lesson file. Format: `.claude/STYLE.md` → Lesson File Format and → Format of Contents.md. |
| 3 | Planning (chat) | `CLAUDE.md` (if needed), `.claude/TASKS.md` — add detailed Phase 4 tasks (one per lesson file/module), based on the finished skeletons from Phase 2 |
| 4 | Execution (repo) | Replace each skeleton's placeholders with the actual lesson content. Structure/headings from Phase 2 are not changed. Format: `.claude/STYLE.md` → Lesson File Format. |
| 5 | Planning (chat) | `CLAUDE.md` (if needed), `.claude/TASKS.md` — add detailed Phase 6 tasks, based on the finished `Contents.md` and lesson content |
| 6 | Execution (repo) | `Practices.md` — decide which exercises are covered, analogous to Phase 1. Headings + bullet points only, no exercise description yet. |
| 7 | Planning (chat) | `CLAUDE.md` (if needed), `.claude/TASKS.md` — add detailed Phase 8 tasks, based on the finished `Practices.md` |
| 8 | Execution (repo) | Create dummy `<nr>.<subnr>-<practice>.md` / `<nr>.<subnr>-<solution>.md` files inside the existing module folders per `Practices.md`; fill in the actual exercise/solution content; update `Practices.md` to link each exercise to its file. |

Notes:
- `current_phase` in this file's frontmatter tracks the active phase. Claude Code reads this before doing anything else, instead of inferring it from prose.
- `.claude/TASKS.md` is the single, cumulative task file for the whole project, grouped by phase (see Task Definition below). It is created once, in Phase 0, and extended — never rewritten from scratch — during each subsequent planning phase.
- Phases 1 and 2 run back-to-back with **no intervening Planning phase** — Phase 2 is largely mechanical once Phase 1's topic list exists (it only builds the folder/file skeleton), so its tasks are pre-defined in Phase 0. Phases 4, 6 and 8, by contrast, each get a dedicated Planning phase (3, 5, 7) beforehand: Phase 4 because writing the actual lesson content is substantial work best scoped module-by-module once the skeleton exists; Phase 6/8 because `Practices.md`'s structure and content can only be meaningfully planned once `Contents.md` and its lesson content are final.
- The task-selection algorithm below applies to the Claude Code agent during execution phases (1, 2, 4, 6, 8). Planning-phase tasks (0, 3, 5, 7) are carried out in the separate Claude Project chat and marked `[X]` there directly.
- During an execution phase, the overall structure (module list, ordering, folder slugs) must not change — only content within the fixed structure is added. Concretely: Phase 2 fixes the skeleton (headings, `## Overview` links); Phase 4 may only add prose beneath the existing headings, not alter them.

# Styleguide

File-format specifications for generated artifacts — the frontmatter header, the lesson-file structure, and the format of `Contents.md` — are documented in `.claude/STYLE.md`. Consult it before producing or editing any of those file types. This section covers only the two harness-process file formats that aren't generated *content* artifacts: the task backlog and the Memory files.

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

Purpose: give the agent the minimal context needed to work a task **consistently with previously completed tasks** — not a full history or diary. Only what would otherwise be lost or ambiguous belongs here; everything already visible in the produced file itself, in `CLAUDE.md`, or in `.claude/STYLE.md` does not.

Two levels:
- **Global** — `.claude/Memory.md`: cross-cutting decisions/conventions relevant across the whole project (e.g. the module numbering scheme, terminology choices, how Practices.md topics were mapped to Contents.md modules). Read before, and updated after, tasks that span multiple modules or files (mainly Phase 1 and Phase 6, plus Phase 3/5/7 planning).
- **Per module** — `Contents/<nr>-<section>/Memory.md`: context scoped to one module (learning objectives already fixed, terminology used in that module, prerequisites established, deviations from the module template). Read before, and updated after, tasks scoped to a single module (mainly Phase 2, Phase 4, and Phase 8). Created the first time a task touches that module.

Rules:
- Before starting a task, the agent reads `.claude/Memory.md`, plus the module's `Memory.md` if the task is module-scoped.
- After finishing or blocking a task, the agent appends at most a few bullet points — only genuinely new, load-bearing context.
- `Memory.md` files hold *current* state, not an append-only diff log — if a fact becomes obsolete, replace it rather than leaving contradictory entries.
- Blocker entries include: what's blocking, why, what's needed to unblock.
