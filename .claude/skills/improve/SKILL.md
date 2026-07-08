---
name: improve
description: Use when the user runs /improve <prompt> after a task to propose and, on approval, apply a content/formatting refinement — then register it as a Follow-up Refinement Subtask in .claude/TASKS.md. This is the only path CLAUDE.md recognizes for such subtasks.
---

# Improve

## Purpose

Turns `/improve <prompt>` into a reviewed, then executed, refinement of a
just-completed task's output, and records it as a Follow-up Refinement
Subtask per `CLAUDE.md` → Task Definition → Follow-up Refinement Subtasks.
Per that section, **only** refinements run through this skill are logged
as subtasks — ad-hoc follow-up edits outside `/improve` are still carried
out if requested, but are never logged this way.

## When this runs

- Invoked explicitly as `/improve <prompt>`.
- Expected right after a task from `.claude/TASKS.md` was worked on in the
  current session.

## Step 1 — Identify the reference task

- If the user specified the task to modifiy in the prompt, use the specified task.
- The task most recently touched in this session, per `.claude/TASKS.md`.
- If more than one task was touched this session, or none, ask once which
  task number (`<phase>.<sequence>`) the improvement is about.

## Step 2 — Draft the change (no edits yet)

- Do not use Edit/Write on any content file at this step. Read-only
  analysis only.
- Compare `<prompt>` against the reference task's current output.
- Draft a concrete, short change plan: what changes, in which file(s), why.

## Step 3 — Assess fit against workshop goals

- Check the drafted change against `CLAUDE.md` → Workshop Scope, Non-Goals,
  and Language and audience conventions.
- Note explicitly whether the change fits better than the current content,
  or whether it conflicts with any of the above (e.g. introduces
  infrastructure depth, cloud-provider specifics, or content outside the
  target audience's assumed knowledge).
- If it conflicts, say so plainly — proceed to Step 4 regardless; the
  decision stays with the user.

## Step 4 — Present and wait for review

- Present the change plan together with the fit assessment as a single
  proposal via `ExitPlanMode` (or equivalent) and wait for the user's
  decision.

## Step 5 — Handle the response

- **Rejected / no reply** → stop. Nothing is edited, nothing is logged.
- **Approved as drafted, or approved after the user edited the wording
  themselves** → proceed to Step 4 with the final, user-confirmed prompt.

## Step 6 — Execute

- Apply the approved change directly to the target file(s) now.
- If the target file's own frontmatter convention requires it, bump
  `revision`/`history` per `CLAUDE.md` → Styleguide.

## Step 7 — Register as Follow-up Refinement Subtask

- Numbering: `<phase>.<sequence>.<subseq>` — e.g. reference task `2.3` →
  first `/improve` run on it this session → `2.3.1`, second → `2.3.2`.
- Insert the new line in `.claude/TASKS.md` directly after its reference
  task (and after any of that task's existing subtasks), status `[X]`
  (work is already done — no intermediate `[ ]`/`[~]` state).
- One-line summary of the resulting change — not a transcript of the
  prompt.
- Apply the content/formatting filter and consolidation rule from
  `CLAUDE.md` → Follow-up Refinement Subtasks: if `<prompt>` turns out to
  be tooling/process rather than workshop content or formatting, still
  execute it if reasonable, but do **not** log a subtask for it.

## Out of scope

- Structural changes (new sections, renumbered folders, moved modules)
  implied by `<prompt>` are out of scope for this skill — say so, and
  point the user to the relevant planning phase (0/3/5) instead. Nothing
  is executed or logged in that case.
