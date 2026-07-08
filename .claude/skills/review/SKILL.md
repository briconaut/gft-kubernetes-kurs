---
name: review
description: Use when the user runs /review <prompt> to review a manual edit made to workshop content, assess its fit against the subheading/heading/workshop context, and — on acceptance — record a style/content note in .claude/Memory.md so future generation stays consistent with it. Distinct from /improve: /review creates no TASKS.md entries; its purpose is training future content generation on the user's own editing patterns, not task refinement.
---

# Review

## Purpose

Reviews a manual edit the user made to a file a task previously produced.
Produces a fit assessment (subheading / heading / workshop) and optional
improvement suggestions, and — once the user accepts the resulting state —
records what the edit reveals about the user's content/style preferences
in `.claude/Memory.md`, so later tasks generate more consistently with it.

This is **not** a task-refinement tool. It never touches `.claude/TASKS.md`
and is unrelated to Follow-up Refinement Subtasks — that's `/improve`'s
domain (`.claude/skills/improve/SKILL.md`).

## When this runs

- Invoked explicitly as `/review <prompt>`.
- Expected after the user has manually edited a file that a task in
  `.claude/TASKS.md` previously produced (typically a Phase 4 lesson file).
- `<prompt>` is optional. When given, it focuses the review (e.g. "check
  technical accuracy only") without dropping the fixed report structure.


## Step 1 — Identify target file and original content

1. If `<prompt>` names a file/section explicitly → candidate = that file
   (and, if named, that subheading). Skip to sub-step 4.
2. Otherwise read `.claude/TASKS.md` and take the `[X]` task with the
   highest task number, since tasks are processed sequentially per the Task
   Selection Algorithm.
3. Read the reference task's `file:` annotation as candidate file. If the
   task also names a specific subheading (as Phase 4 subheading tasks do),
   record that as the known structural context — reused directly in Step 3
   below, no need to re-derive it from the diff.
4. Validate: confirm the candidate file actually differs from its
   last-known-good state (see Original below). If it doesn't, the wrong
   task/file was picked — report this and ask the user to name the file
   directly, rather than silently reviewing an unchanged file.
5. If no task reference is found at all (e.g. no completed tasks, or the
   task has no `file:` annotation) → fall back to
   `git diff --name-only` (uncommitted changes). Exactly one → use it;
   more than one, or none → ask once.

Determine the **Original**, in this order:
   a. The content this agent itself produced for the candidate
      file/subheading earlier in the current session — recalled from the
      session's own prior output, not read from disk. Only applies if the
      reference task was resolved via the session-context branch above.
   b. Otherwise `git diff HEAD -- <candidate file>` (working tree vs.
      last commit).
   c. If neither yields a usable original → say so and ask the user to
      point at the reference version. Do not guess.

## Step 2 — Short-circuit: pure orthographic correction?

Before any structural analysis: check whether the diff consists **only**
of spelling/typo fixes — character-level corrections that change no word
choice, meaning, or structure. Grammar, phrasing, tone, and structural
edits do **not** qualify, even if small.

- **Yes** → present Original + Änderung with a one-line note ("reine
  Rechtschreibkorrektur, keine inhaltliche Bewertung nötig") and ask for
  confirmation.
  - Confirmed → **stop here**. No Step 4 report, no Step 6 edits, no
    Step 7 version bump, no Step 8 memory entry.
  - Rejected / "review anyway" → continue at Step 3.
- **No** → continue at Step 3.

## Step 3 — Locate structural context

- If Step 1 already resolved the subheading via a Phase 4 task reference,
  reuse it directly. Only derive subheading(s) from the diff/Contents.md
  comments when Step 1 didn't yield one (e.g. `<prompt>`-named file
  without subheading, or a whole-file task from Phase 1/6).
- Determine the affected `##` subheading(s), their enclosing `##` topic
  heading, and the parent `#` section — via `Contents.md`'s
  `folder:`/`lesson:` comments and the file's own structure (per
  `.claude/STYLE.md` → Lesson File Format).
- If the diff spans more than one subheading, review each affected
  subheading separately within a single combined report.

## Step 4 — Assess fit

Using `CLAUDE.md` → Workshop Scope, Non-Goals, Language and audience
conventions, and `.claude/STYLE.md` as the yardstick, assess:

- Eignung der Änderung für den Zweck des betroffenen Subheadings.
- Eignung der Änderung für den Zweck des übergeordneten Headings.
- Eignung der Änderung für den Zweck des Workshops insgesamt.
- **Formale Konformität** (separate Kategorie, nicht Teil obiger Punkte):
  Verstößt die Änderung gegen `.claude/STYLE.md` — insbesondere gegen die
  Phase-4-Regel, dass nur Prosa unter fixen Headings verändert werden darf,
  keine Struktur/Headings selbst?

If `<prompt>` was given, weight the report toward its focus without
dropping the other categories entirely.

## Step 5 — Report and present

Present, in one message, without editing anything yet:

- **Original** and **manuelle Änderung** (diff or clear before/after).
- **Bericht**:
  - Eignung für das Subheading
  - Eignung für das Heading
  - Eignung für den Workshop
  - Entdeckte Fehler (inhaltlich, technisch, formal)
  - Verbesserungsvorschläge (concrete; may be empty if the edit is already sound)

## Step 6 — Handle the response

- **Rejected / no reply** → stop. Manual edit stays on disk as-is; still
  proceed to Step 7/8 (the manual edit itself is the data point worth
  recording, independent of whether suggestions were adopted).
- **Accepted as-is** (no suggestions needed, or user declines them) →
  proceed to Step 7 with no additional edits.
- **Accepted with Verbesserungsvorschläge** (as drafted, or after the
  user adjusts them) → apply the approved refinements now.

## Step 7 — Version bump

Bump `revision`/`history` in the file's frontmatter per
`.claude/STYLE.md`, summarizing: that a manual edit was reviewed, whether
refinements were applied, and a one-line description of the result.

## Step 8 — Record a Review Note in `.claude/Memory.md`

- Under a dedicated `## Review Notes` section (create it, seeded empty,
  the first time this skill runs if it doesn't exist yet) — **not** the
  module-scoped `Memory.md`.
- One entry per concluded review (Step 6/7), containing:
  - Reference to the changed file/section (path + subheading).
  - Analyse der inhaltlichen Änderung — was inhaltlich geändert wurde und
    wieso die manuelle Änderung so vorgenommen wurde.
  - Analyse des Stils — Ton, Formulierungsmuster, strukturelle Gewohnheiten,
    die in der manuellen Änderung erkennbar sind.
- This section is a **deliberate exception** to `CLAUDE.md` → Memory
  Structure's "current state, not append-only log" rule (see there).
  Entries accumulate; they are never condensed or overwritten.

## Out of scope

- No `.claude/TASKS.md` entries, ever — not a Follow-up Refinement Subtask
  mechanism.
- Structural changes revealed by the diff (new headings, reordered
  bullets, renamed sections) are flagged under "Entdeckte Fehler" as scope
  violations — never silently accepted or auto-fixed. Phase 2/4 structure
  is fixed per `CLAUDE.md`.
