---
revision: 21
path: ".claude/TASKS.md"
title: "Task Backlog"
abstract: "Single, cumulative task list for all workshop phases (0-8), grouped by phase. Status model: [ ] Open, [~] In Progress, [R] Needs Rework, [B] Blocked, [X] Done."
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
  - "v12: completed task 1.4 — recorded how the old Contents.qmd draft's structure was reused/deviated from in .claude/Memory.md, closing out Phase 1"
  - "v13: added Follow-up Refinement Subtask 1.3.1 (per-lesson `<!-- lesson: ... -->` path comments in Contents.md, via /improve) for Task 1.3"
  - "v14: reworded task 2.1/2.2 to reference the folder:/lesson: HTML comments as the binding path source (CLAUDE.md v12); reworded task 2.3 to reference the new Styleguide → Lesson File Body Format (CLAUDE.md v13) instead of the vague 'fill in actual lesson content' phrasing"
  - "v15: renumbered per CLAUDE.md v14 (9-phase model, 0–8). Phase 2 narrowed to skeleton creation only (2.1–2.3: folders, lesson-file skeletons with placeholders, Contents.md links — content-fill removed). Added new Phase 3 planning placeholders (3.1–3.2, planning Phase 4 content-fill tasks) and new Phase 4 execution placeholder (Contents.md lesson content). Former Phase 3 planning tasks → Phase 5 (5.1–5.2). Former Phase 4 Practices.md topic-list placeholder → Phase 6. Former Phase 5 planning tasks → Phase 7 (7.1–7.2). Former Phase 6 exercise-content placeholder → Phase 8."
  - "v16: updated tasks 2.2, 2.3, and 3.2 to reference the new `.claude/STYLE.md` (CLAUDE.md v15) instead of the now-removed CLAUDE.md → Styleguide → Lesson File Body Format section."
  - "v17: completed task 2.1 — created all 13 `Contents/<nr>-<section>/` folders per the `folder:` comments in Contents.md"
  - "v18: completed task 2.2 — created all 32 lesson-file skeletons (H1, linked Overview, per-bullet placeholder headings) at the exact `lesson:` comment paths, per .claude/STYLE.md → Lesson File Format; `## Practice: ...` topics correctly excluded (7 of them, no lesson file)"
  - "v19: completed task 2.3 — linked all 32 `##` topic headings in Contents.md to their lesson files; Phase 2 complete"
  - "v20: added Follow-up Refinement Subtask 2.3.1 (bullet-level links to lesson-file anchors in Contents.md, via /improve) for Task 2.3"
  - "v21: reworded task 3.2 — Phase 4 tasks are now generated per lesson-file subheading (one task per `## <bullet>` heading, excluding `## Overview`) instead of one per lesson file/module; added a dedicated per-lesson-file review task (subheading consistency; fit of each subheading and of the whole file against its topic heading and against the workshop), inserted after that file's subheading tasks. Review tasks are explicitly regular `4.x` tasks, not Follow-up Refinement Subtasks. Per CLAUDE.md v16."
  - "v22: completed task 3.1 (executed by Claude Code per user instruction) — reviewed Phase 1/2 output, found no scope/content issues, and fixed one spec/reality drift in .claude/STYLE.md (bullet-anchor-link convention from 2.3.1 was undocumented)"
---

# Task Backlog

Status model, task-selection algorithm and the Follow-up Refinement Subtasks convention are defined in `CLAUDE.md` → Styleguide → Task Definition. File-format rules referenced below live in `.claude/STYLE.md`. Numbering is `<phase>.<sequence>`, with optional follow-up-refinement subtasks `<phase>.<sequence>.<subsequence>`.

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
  - 1.3.1 [X] Added a stable full-path `<!-- lesson: Contents/<nr>-<section>/<nr>-<lesson>.md -->` comment under each `##` topic heading (per-section local numbering), analogous to the section-level `folder:` comments; `## Practice: ...` headings excluded (Phase 8 scheme)
- 1.4 [X] Note in `.claude/Memory.md` how the old draft's structure was reused or deviated from, so Phase 2 stays consistent (file: .claude/Memory.md)

## Phase 2 — Execution (Claude Code agent, this repo) — Contents.md structure (folders + lesson-file skeletons)

- 2.1 [X] Create the 13 folders `Contents/<nr>-<section>/` named by the `<!-- folder: ... -->` comments in Contents.md, if they don't exist yet (file: Contents/<nr>-<section>/)
- 2.2 [X] For every `<!-- lesson: Contents/<nr>-<section>/<local-nr>-<lesson>.md -->` comment in Contents.md, create the lesson file at exactly that path with correct frontmatter (`state: not started`) and the skeleton body per `.claude/STYLE.md` → Lesson File Format (H1, linked `## Overview`, one empty `##` heading per bullet with a `_Content pending (Phase 4)._` placeholder) — no prose yet. Use the path from the comment verbatim (file: Contents/<nr>-<section>/<local-nr>-<lesson>.md)
- 2.3 [X] Update Contents.md: turn each `##` topic heading into a Markdown link to its `lesson:` file (link format per `.claude/STYLE.md` → Format of Contents.md), keeping the underlying `<!-- lesson: ... -->` comment intact; leave `## Practice: ...` headings untouched (file: Contents.md)
  - 2.3.1 [X] Replaced all 197 bullet points under linked topics with links to their own anchor in the corresponding lesson file, reusing the anchors from each file's `## Overview`; bullets under `## Practice: ...` topics left as plain text (no lesson file); `.claude/STYLE.md` intentionally left unchanged per user instruction

## Phase 3 — Planning (done in Claude Project chat)

- 3.1 [X] Review Phase 1/2 output (Contents.md + lesson-file skeletons); update CLAUDE.md/.claude/STYLE.md if needed
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

_Tasks added during Phase 3 planning, once the Contents.md skeleton structure from Phase 1/2 is final._

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
