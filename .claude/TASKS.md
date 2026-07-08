---
revision: 11
path: ".claude/TASKS.md"
title: "Task Backlog"
abstract: "Single, cumulative task list for all workshop phases (0-6), grouped by phase. Status model: [ ] Open, [~] In Progress, [R] Needs Rework, [B] Blocked, [X] Done."
state: in progress
lang: en
numbersections: false
finished_sections: [ ]
history:
  - "v1: seeded during Phase 1 with phase-level milestones, [TODO]/[DONE] format"
  - "v2: consolidated former .claude/PHASE 2/TASKS.md into this file; switched to the five-state status model and <phase>.<sequence> numbering; added placeholder sections for Phase 4/6 (populated during Phase 3/5 planning)"
  - "v3: added task 1.3 for the .claude/Memory.md seed file"
  - "v4: renumbered all phases/tasks per CLAUDE.md v6 (superseded)"
  - "v5: split former Phase 1 into Phase 1 (Eckpunkte) and Phase 2 (verbose fill-in) per CLAUDE.md v7 (superseded)"
  - "v6: replaced with per-file workflow per CLAUDE.md v8 — Phase 1-2 fully process Contents.md, Phase 4/6 do the analogous work for Practices.md (planned in Phase 3/5). Dropped Part 1/Part 2 split tasks (now manual, out of scope)."
  - "v7: adopted Follow-up Refinement Subtasks convention (<phase>.<sequence>.<subsequence>) per CLAUDE.md v9 Task Definition update."
  - "v8: retroactively added Follow-up Refinement Subtasks 1.2.1 and 1.2.2 (bullet/question-fit review and audience-completeness review) for Task 1.2, per CLAUDE.md v9 convention"
  - "v9: retroactively added Follow-up Refinement Subtask 1.1.1 (expanded subtopic bullet lists to at least 6 points, commit 0e21a8d) for Task 1.1, per CLAUDE.md v9 convention"
  - "v10: added Follow-up Refinement Subtask 1.2.3 (added 'Resource requests & limits' bullet to Contents.md via /improve) for Task 1.2"
  - "v11: completed task 1.3 — assigned <nr>-<section> folder slugs (01-introduction .. 13-service-mesh) to all top-level sections in Contents.md; excluded 'Further Reading / Links' (not a lesson module)"
---

# Task Backlog

Status model, task-selection algorithm and the Follow-up Refinement Subtasks convention are defined in `CLAUDE.md` → Styleguide → Task Definition. Numbering is `<phase>.<sequence>`, with optional follow-up-refinement subtasks `<phase>.<sequence>.<subsequence>`.

## Phase 0 — Planning (done in Claude Project chat)

- 0.1 [X] Produce `CLAUDE.md` — workshop scope, non-goals, styleguide, phase model, task-file conventions
- 0.2 [X] Produce `.claude/TASKS.md` — consolidated task backlog for all phases (this file)
- 0.3 [X] Produce `.claude/Memory.md` — seeded, empty global memory file

## Phase 1 — Execution (Claude Code agent, this repo) — Contents.md topic list

- 1.1 [X] Review the existing Contents.md draft (inspiration only, not binding) and produce a definitive list of topics to cover, organized into logical sections — headings + bullet points only, no explanatory prose (file: Contents.md)
  - 1.1.1 [X] Expanded every subtopic's bullet list to at least 6 points (commit 0e21a8d)
- 1.2 [X] Phrase each topic as a concrete, answerable question in the audience's terms (e.g. "What is a container?", "What is a Node?", "What is a Pod?", "What is a Service?") rather than abstract chapter titles (file: Contents.md)
  - 1.2.1 [X] Verified bullets answer their subheading's question; tightened "What components run on a worker node?" to name components rather than responsibilities
  - 1.2.2 [X] Verified bullet completeness for the intro audience; added Pod IP address, `kubectl apply/create/delete`, Docker Desktop `hostpath` StorageClass, and GitOps tool-example bullets, and replaced a redundant Docker-comparison bullet
  - 1.2.3 [X] Added "Resource requests & limits (brief mention)" bullet under "What is container orchestration?" (kept as an addition, not a replacement, to avoid colliding with the dedicated Configuration Management section)
- 1.3 [X] Assign a stable `<nr>-<section>` folder slug to each top-level section, to be used as the folder name in Phase 2 (file: Contents.md)
- 1.4 [ ] Note in `.claude/Memory.md` how the old draft's structure was reused or deviated from, so Phase 2 stays consistent (file: .claude/Memory.md)

## Phase 2 — Execution (Claude Code agent, this repo) — Contents.md lesson content

- 2.1 [ ] For each top-level section from Contents.md, create the folder `Contents/<nr>-<section>/` if it doesn't exist yet (file: Contents/<nr>-<section>/)
- 2.2 [ ] For each topic/question within a section, create a dummy `<nr>-<lesson>.md` stub file with correct frontmatter and a one-line placeholder (file: Contents/<nr>-<section>/<nr>-<lesson>.md)
- 2.3 [ ] Fill in the actual lesson content for each `<nr>-<lesson>.md` stub, module by module, following the Language/Audience conventions and Styleguide (file: Contents/<nr>-<section>/<nr>-<lesson>.md)
- 2.4 [ ] Update Contents.md: replace each topic heading with a link to its corresponding `<nr>-<lesson>.md` file (file: Contents.md)

## Phase 3 — Planning (done in Claude Project chat)

- 3.1 [ ] Review Phase 1/2 output (Contents.md + lesson files); update CLAUDE.md if needed
- 3.2 [ ] Add detailed Phase 4 tasks (3.x → 4.x) to this file, analogous to Phase 1's tasks but for Practices.md

## Phase 4 — Execution (Claude Code agent, this repo) — Practices.md topic list

_Tasks added during Phase 3 planning, once Contents.md and the lesson content from Phase 1/2 are final._

## Phase 5 — Planning (done in Claude Project chat)

- 5.1 [ ] Review Phase 4 output (Practices.md); update CLAUDE.md if needed
- 5.2 [ ] Add detailed Phase 6 tasks (5.x → 6.x) to this file, analogous to Phase 2's tasks but for exercise/solution files

## Phase 6 — Execution (Claude Code agent, this repo) — Practices.md exercise content

_Tasks added during Phase 5 planning, once Practices.md from Phase 4 is final._
