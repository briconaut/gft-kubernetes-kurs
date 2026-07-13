---
name: build-vision
description: Use when the user runs /build-vision [prompt] to (re)build .claude/VISION.md — a distilled content guardrail summarizing the source material in Original/ — and to detect when that source material has changed since the last build. Deliberately isolated from the rest of the repository, including CLAUDE.md. If Original/Vision.md exists, it takes priority over all other files in Original/. Optional [prompt] steers a rebuild, or (if no source changes exist) directly guides a targeted edit of the existing VISION.md.
---

# Build Vision

## Purpose

Maintains `.claude/VISION.md`: a summary of the source material in
`Original/`, distilled into content guardrails. Tracks which source files
were considered, via MD5 hashes, so later runs can detect when
`Original/` has changed.

Whether and how `VISION.md` relates to `CLAUDE.md` → Workshop Scope, or to
already-generated content, is a separate, manual decision outside this
skill — see Isolation below and Out of scope.

## Isolation — read this first

This skill must not read, reference, or let its output be influenced by
**any file in this repository other than `Original/` and `.claude/VISION.md`
itself** (its own previous version — for diffing and the Source Files
table only). This explicitly includes `CLAUDE.md`, `.claude/STYLE.md`,
`.claude/Memory.md`, `Contents.md`, `Practices.md`, and all
lesson/exercise/solution files.

- The Content Guardrails text is derived exclusively from what's in
  `Original/` — never adjusted to match, avoid overlap with, or otherwise
  account for existing workshop scope or content.
- Mechanical repo operations (writing `.claude/VISION.md`, scanning
  `Original/`) are unaffected by this — the isolation is about
  *informational* influence on the summary, not about the skill's
  ability to function inside the repo.
- The frontmatter format below is copied from `.claude/STYLE.md`'s
  convention for structural consistency only — it is inlined here rather
  than read from that file at runtime, specifically to keep this skill's
  execution fully isolated.

## Priority within `Original/`

If `Original/Vision.md` exists, it is the **authoritative source among
the files in `Original/`** — not to be confused with the skill's own
output file `.claude/VISION.md` (different path, different filename
case; always refer to each by its full path to avoid confusion).

- All other files in `Original/` are subordinate: used to add supporting
  detail, terminology, or examples, but never to override or contradict
  `Original/Vision.md`.
- When generating `## Content Guardrails` (Step 3, and the rebuild branch
  of Step 4): read `Original/Vision.md` first and treat it as the
  framework; layer in the other files' content only where it doesn't
  conflict.
- Where another file in `Original/` contradicts `Original/Vision.md`,
  resolve in favor of `Original/Vision.md` — but record each such
  contradiction (source, what it said, what was used instead) so it can
  be shown to the user in Step 5. Silent overriding is not acceptable
  here.
- `Original/Vision.md` participates in change detection and the
  `## Source Files` table exactly like any other file in `Original/` — no
  exemption from MD5 tracking.
- **If `Original/Vision.md` exists but can't be read as plain text**
  (unlike other unreadable files, which are merely noted in the table):
  stop before building or presenting any draft, tell the user that the
  priority source is unreadable, and ask how to proceed. Its authoritative
  role can't be honored if its content is inaccessible.

## When this runs

- Invoked as `/build-vision` or `/build-vision <prompt>`.
- `<prompt>` is optional and means different things depending on whether
  `Original/` has changed since the last build (see Step 2).

## Step 1 — Scan `Original/` and detect changes

- List all files in `Original/` (recursively), compute MD5 for each.
- If `.claude/VISION.md` does not exist yet → treat this as "changes
  detected" (every file is new) → go to Step 3 (Erstlauf).
- If it exists → compare against the `## Source Files` table in the
  current `.claude/VISION.md`:
  - New files (not in the table), or files whose MD5 differs → changes
    detected.
  - No new/changed files → no changes detected.

## Step 2 — Branch on parameter and change state

| Parameter? | Changes detected? | Action |
|---|---|---|
| no | no | Report "no changes in `Original/`, `VISION.md` is current." Stop — nothing written. |
| no | yes | Full rebuild from all files in `Original/`, no steering prompt → Step 4. |
| yes | no | Interpret `<prompt>` as an instruction to directly modify the **existing** `VISION.md` content (no rebuild from `Original/`) → Step 4. |
| yes | yes | Full rebuild from all files in `Original/`, using `<prompt>` to steer the rebuild (emphasis, focus, exclusions, ...) → Step 4. |

Both "yes" rows route through Step 3 instead if this is the Erstlauf case
(`.claude/VISION.md` doesn't exist yet).

## Step 3 — Erstlauf (`.claude/VISION.md` does not exist yet)

- Build `.claude/VISION.md` directly from all files in `Original/`,
  respecting the priority rule above if `Original/Vision.md` exists (if
  `<prompt>` was given, use it to steer this initial build).
- **No confirmation step** — write the file directly.
- Frontmatter (inlined per Isolation above, not read from `STYLE.md`):

      ---
      revision: 1
      path: ".claude/VISION.md"
      title: "Workshop Vision"
      abstract: "<one-sentence description>"
      state: in progress
      lang: en
      numbersections: false
      finished_sections: [ ]
      history:
        - "v1: initial build from Original/"
      ---

- Body: `## Content Guardrails` (the distilled summary — themes,
  priorities, constraints, terminology found in the source material),
  followed by `## Source Files` (path + MD5 table, format below). If
  `Original/Vision.md` exists, add a short `## Notes` subsection listing
  any contradictions found and how they were resolved (per Priority
  within `Original/` above) — omit this subsection if none were found.
- If a non-priority file's format can't be read as plain text (e.g. a
  binary format with no available extraction tool), list it in `##
  Source Files` with its MD5 but note "unreadable — content not
  considered" next to it, and mention this to the user after writing the
  file.
- Done — no Step 4/5.

## Step 4 — Build the draft (no file write yet)

- **Rebuild case** (changes detected): regenerate `## Content Guardrails`
  considering **all** files currently in `Original/` — a full rebuild,
  not an incremental merge with the previous version — respecting the
  priority rule above. If `<prompt>` given, use it to steer
  emphasis/focus/exclusions.
- **Targeted-edit case** (no changes, prompt given): apply `<prompt>` as
  an instruction to modify the existing `## Content Guardrails` directly;
  `## Source Files` stays unchanged (nothing in `Original/` changed).
- Keep the draft in-session — do not write to `.claude/VISION.md` yet.

## Step 5 — Present and ask

Present the draft's `## Content Guardrails` (diff against the current
`VISION.md` if one exists), **any contradictions found and how they were
resolved** (rebuild case, if `Original/Vision.md` exists), and ask the
user to choose:

- **Ignorieren** — discard the draft entirely. Nothing is written —
  neither content nor the `## Source Files` table. The same changes will
  be detected and re-proposed on the next `/build-vision` run.
- **Übernehmen** — write the draft as the new `.claude/VISION.md`: bump
  `revision`/`history` (per the inlined frontmatter format above), replace
  `## Content Guardrails` (and `## Notes` if present), and (rebuild case
  only) replace `## Source Files` with the current, complete file/MD5
  list.
- **Durch Prompts verfeinern** — ask for a prompt, apply it to the
  in-session draft (not written to disk yet), re-present the updated
  draft, repeat this step. Loops until Ignorieren or Übernehmen is chosen.

## `## Source Files` format

    ## Source Files

    | Path | MD5 |
    |---|---|
    | Original/Vision.md | <md5sum> |
    | Original/<file> | <md5sum> |
    | Original/<file> | <md5sum> — unreadable, content not considered |

## Out of scope

- Does not check or reconcile already-generated content (`Contents.md`,
  lesson files) or `CLAUDE.md` → Workshop Scope against `VISION.md` —
  deliberately isolated (see Isolation above); that relationship is a
  separate, manual decision.
- Does not touch `.claude/Memory.md`.
