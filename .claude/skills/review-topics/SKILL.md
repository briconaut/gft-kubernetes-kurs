---
name: review-topics
description: Use when the user runs /review-topics to analyze the # Topics section of .claude/TOPICS.md against .claude/VISION.md — checking subtopic redundancy (within and across topics), coverage of each topic by its subtopics, coverage of the workshop goal by topics alone and by topics+subtopics together, and per-subtopic fitness against VISION.md's guardrails. Produces a report with concrete suggestions; makes no file changes.
---

# Review Topics

## Purpose

Produces a structured quality report on `.claude/TOPICS.md` → `# Topics`,
evaluated against `.claude/VISION.md` → `## Content Guardrails`: redundancy,
coverage gaps, and guardrail incompatibilities, each with concrete,
non-redundant suggestions grounded in already-analyzed source material
where possible.

This is a **read-only review** — no file is modified. Suggestions are
presented for the user to act on manually (e.g. by editing `# Topics`
directly, or promoting something into it).

## Prerequisite

- Requires both `.claude/TOPICS.md` and `.claude/VISION.md` to exist. If
  either is missing → stop, tell the user which one and point to
  `/build-topics` / `/build-vision` respectively.

## Isolation

Reads only `.claude/TOPICS.md` and `.claude/VISION.md`, plus — solely to
ground suggestions in real material rather than inventing content —
`.claude/TOPICS-ORIGINAL.md` if it exists (see Step 4). Does not read
`CLAUDE.md`, `.claude/STYLE.md`, `Original/`, or any other repository
file. "Workshop goal" in this skill means `.claude/VISION.md` → `##
Content Guardrails` specifically, not `CLAUDE.md` → Workshop Scope —
consistent with the isolation already established for `VISION.md`/
`TOPICS.md`/`TOPICS-ORIGINAL.md`.

## Step 1 — Load and scope

- Load `.claude/VISION.md` → `## Content Guardrails`.
- Load `.claude/TOPICS.md`, extract **only** the `# Topics` section
  (`## <topic>` / `### <subtopic>` pairs). `# Exercises`, `# Excluded`,
  and `# New` are not analyzed as subjects of review — `# Excluded` and
  `# New` are consulted only in Step 4, to avoid contradicting or
  duplicating existing decisions when generating suggestions.

## Step 2 — Redundancy analysis

1. **Within each topic**: for every `## <topic>`, compare its `###
   <subtopic>` entries pairwise. Redundant = substantially the same
   conceptual ground, not necessarily identical wording. List redundant
   pairs per topic.
2. **Across all topics** (within `# Topics` only): compare every
   `### <subtopic>` against every other one system-wide, regardless of
   parent topic. Report only pairs **not already listed** under point 1
   (i.e. genuinely cross-topic redundancies) — avoids double-reporting
   same-topic pairs.

## Step 3 — Coverage and fitness analysis (against VISION.md)

For each `## <topic>`:

- **Topic coverage**: do its `### <subtopic>` entries adequately cover
  what the topic promises, per the guardrails? Rate as sufficient or
  gapped; if gapped, proceed to Step 4 for suggestions.

Across the full `# Topics` set:

- **Goal coverage by topics alone**: do the `## <topic>` headings, as a
  set, cover what `## Content Guardrails` calls for? Note any guardrail
  theme with no corresponding topic.
- **Goal coverage by topics + subtopics together**: re-check the same
  question, this time factoring in whether the *realized* subtopic depth
  actually delivers each topic's share of the guardrails — a topic can
  pass the first check (title-level) and fail this one (its subtopics are
  too shallow or off-target to actually deliver it).
- **Per-subtopic fitness**: for every individual `### <subtopic>`, check
  it against `## Content Guardrails` directly. Flag any that conflict
  with (not just fail to relate to) the guardrails as an incompatibility.

## Step 4 — Suggestions for coverage gaps

For every gap found in Step 3 (topic-level or workshop-goal-level):

- First look for a fitting, non-redundant candidate already present in
  `.claude/TOPICS-ORIGINAL.md` → `# Topics`/`# Exercises` (if the file
  exists) — reusing real, already-analyzed material rather than inventing
  new content.
- Before proposing any candidate (from `TOPICS-ORIGINAL.md` or newly
  drafted), check it isn't already in `.claude/TOPICS.md` → `# Excluded`
  (respect prior exclusion — do not re-propose) or already in `# New`
  (avoid duplicate suggestions of something already queued there).
- If no suitable candidate exists anywhere, draft a new
  topic/subtopic that fits `## Content Guardrails` and isn't redundant
  with anything already in `# Topics`.
- Missing subtopic coverage → propose additional `### <subtopic>` entries
  under the affected `## <topic>`.
- Missing workshop-goal coverage → propose additional `## <topic>`
  entries, each with its own `### <subtopic>` entries.

## Step 5 — Incompatibility reporting

For every guardrail conflict found in Step 3 (per-subtopic fitness, or a
topic/subtopic that actively contradicts a guardrail rather than merely
under-covering it):

- Report the conflicting topic/subtopic, and which part of `## Content
  Guardrails` it conflicts with.
- Propose a concrete resolution: reword, narrow scope, move to a
  different topic, or remove — whichever fits the specific conflict. Do
  not just flag without a proposed fix.

## Step 6 — Present the report

Present all of the above as a single structured report, in this order:
Redundancy (within-topic, then cross-topic), Coverage gaps with
suggestions (per-topic, then workshop-goal), Incompatibilities with
proposed resolutions. If a category has no findings, say so briefly
rather than omitting the section.

## Out of scope

- `# Exercises` is not analyzed and does not factor into "workshop goal
  coverage" here, even though exercises realistically contribute to it —
  this follows directly from the user's restriction to `# Topics`.
- No file is written or modified — not `.claude/TOPICS.md`, not `# New`.
  Acting on suggestions (editing `# Topics`, promoting a suggestion) is
  manual, outside this skill.
- Does not re-run or duplicate `/build-topics`'s own guardrail filter —
  that already happened when `.claude/TOPICS-ORIGINAL.md` was built; this
  skill reviews the current, possibly hand-edited state of `TOPICS.md`
  independently.
