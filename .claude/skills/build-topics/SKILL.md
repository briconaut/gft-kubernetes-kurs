---
name: build-topics
description: Use when the user runs /build-topics [prompt] to (re)build .claude/TOPICS-ORIGINAL.md — a topic/subtopic outline distilled from Original/, split into Topics and Exercises, filtered against .claude/VISION.md's content guardrails — and to sync .claude/TOPICS.md (a curated tracking file with Topics/Exercises/Excluded/New sections) from it. Requires .claude/VISION.md to already exist. Same mechanics as build-vision (change detection, first-run vs. update, confirmation loop), with VISION.md as the one explicit exception to repo isolation.
---

# Build Topics

## Purpose

Maintains two files:

- **`.claude/TOPICS-ORIGINAL.md`** — the full, disposable analysis output:
  every topic/subtopic found in `Original/`, filtered against
  `.claude/VISION.md`'s guardrails, split into Topics and Exercises, with
  source content attached. Fully rebuilt on each accepted run, same as
  `build-vision`.
- **`.claude/TOPICS.md`** — the curated, long-lived tracking file. Created
  once from `TOPICS-ORIGINAL.md`'s heading structure, then maintained by
  the user (`# Topics`, `# Exercises`, `# Excluded`) and this skill
  (`# New` only).

## Prerequisite

- Requires `.claude/VISION.md` to exist. If it doesn't → stop
  immediately, tell the user to run `/build-vision` first, do nothing
  else.

## Isolation — read this first

Same isolation as `.claude/skills/build-vision/SKILL.md`, with exactly
one explicit exception: this skill **must** read `.claude/VISION.md` to
filter topics/subtopics against its `## Content Guardrails`. Everything
else in the repository remains off-limits — `CLAUDE.md`, `.claude/STYLE.md`,
`.claude/TASKS.md`, `.claude/Memory.md`, `Contents.md`, `Practices.md`,
and all lesson/exercise files must not be read or otherwise influence the
output.

- `VISION.md` is used only as a **filter** — never as a source of topics.
  Topics and subtopics come exclusively from files in `Original/`.
- Frontmatter is inlined (not read from `STYLE.md`), same reason as
  `build-vision`.

## Priority within `Original/`

Inherited unchanged from `build-vision`: if `Original/Vision.md` exists,
its topics/subtopics take priority over conflicting ones found in other
`Original/` files. Contradictions are recorded and surfaced in Step 6.

## When this runs

- Invoked as `/build-topics` or `/build-topics <prompt>`.
- `<prompt>` is optional and means different things depending on whether
  `Original/` (or `VISION.md`) has changed since the last
  `TOPICS-ORIGINAL.md` build (Step 2).
- Everything through Step 6 concerns `TOPICS-ORIGINAL.md` only. `TOPICS.md`
  is only ever touched in Step 7, and only as a consequence of
  `TOPICS-ORIGINAL.md` actually being written.

## Step 1 — Scan `Original/` and `VISION.md`, detect changes

- List all files in `Original/` (recursively), compute MD5 for each.
- Note the `revision` value currently in `.claude/VISION.md`'s
  frontmatter.
- If `.claude/TOPICS-ORIGINAL.md` does not exist yet → treat this as
  "changes detected" → go to Step 3 (Erstlauf).
- If it exists → compare against its own `## Source Files` table and its
  recorded `vision_revision`:
  - New files, changed MD5s, or a different `VISION.md` revision → changes
    detected.
  - None of the above → no changes detected.

## Step 2 — Branch on parameter and change state

| Parameter? | Changes detected? | Action |
|---|---|---|
| no | no | Report "no changes in `Original/` or `VISION.md`, `TOPICS-ORIGINAL.md` is current." Stop — nothing written, Step 7 not run. |
| no | yes | Full rebuild from all files in `Original/`, filtered against current `VISION.md`, no steering prompt → Step 4. |
| yes | no | Interpret `<prompt>` as an instruction to directly modify the **existing** `TOPICS-ORIGINAL.md` content (no rebuild from `Original/`) → Step 4. |
| yes | yes | Full rebuild, filtered against current `VISION.md`, using `<prompt>` to steer the rebuild → Step 4. |

Both "yes" rows route through Step 3 instead if this is the Erstlauf case.

## Step 3 — Erstlauf (`.claude/TOPICS-ORIGINAL.md` does not exist yet)

- Build `.claude/TOPICS-ORIGINAL.md` directly from all files in
  `Original/`, respecting the `Original/Vision.md` priority rule, filtered
  against `.claude/VISION.md` → `## Content Guardrails` (if `<prompt>`
  was given, use it to steer this initial build).
- **No confirmation step** — write the file directly.
- Frontmatter (inlined, not read from `STYLE.md`):

      ---
      revision: 1
      path: ".claude/TOPICS-ORIGINAL.md"
      title: "Workshop Topics (Analysis)"
      abstract: "<one-sentence description>"
      state: in progress
      lang: en
      numbersections: false
      finished_sections: [ ]
      vision_revision: <revision of .claude/VISION.md considered>
      history:
        - "v1: initial build from Original/, filtered against VISION.md rev <n>"
      ---

- Body, in this order: `# Topics`, `# Exercises`, `# Notes`, `# Source Files`
  (formats below).
- Done — proceed directly to Step 7 (sync `.claude/TOPICS.md`), no Step 4/5/6.

## Step 4 — Build the draft (no file write yet)

- **Rebuild case**: regenerate `# Topics` and `# Exercises` considering
  **all** files currently in `Original/` — a full rebuild, not an
  incremental merge — respecting the priority rule, filtered against the
  current `VISION.md`. If `<prompt>` given, use it to steer
  emphasis/focus/exclusions.
- **Targeted-edit case** (no changes, prompt given): apply `<prompt>` as
  an instruction to modify the existing `# Topics`/`# Exercises` content
  directly; `# Source Files` and `vision_revision` stay unchanged.
- Keep the draft in-session — do not write to `.claude/TOPICS-ORIGINAL.md`
  yet.

## Step 5 — Determine topics, subtopics, classification, and content

- **Topic identification**: derive topics from the structure/themes of
  each `Original/` file (explicit headings if present, inferred themes
  otherwise). Collapse topics that are clearly the same concept into a
  single topic, across all files.
- **Subtopic identification**: same, one level down, collapsed within
  their topic the same way.
- **Cross-topic duplicates**: if the same subtopic text is found under
  two different topics, keep both occurrences in their respective
  topics — do not merge across topics — but record it in `# Notes`.
- **Exercises vs. Topics classification**: for each subtopic, decide
  whether it involves exercises or concrete step-by-step instructions
  (e.g. explicit `kubectl` commands, hands-on walkthroughs) — if so, it
  belongs under `# Exercises`, grouped under a `## <topic>` there;
  otherwise under `# Topics`, grouped under a `## <topic>` there. The
  same topic name may legitimately appear as its own block in both
  sections — this is expected, not a duplicate to flag.
- **Guardrail filter**: drop any topic or subtopic that doesn't fit
  `.claude/VISION.md` → `## Content Guardrails`; record what was dropped
  and why in `# Notes` under "Filtered out (doesn't fit VISION.md
  guardrails)" — deliberately not called "Excluded", to avoid confusion
  with `.claude/TOPICS.md`'s `# Excluded` section, which is a separate,
  user-curated concept.
- **Content**: where a topic/subtopic has actual prose in the source
  material, place it under that `### <subtopic>` heading. Multiple source
  passages mapping to the same subtopic are concatenated, separated by
  `---`. Subtopics with no source content stay as a bare `###` heading.

## Step 6 — Present and ask

Present the draft (diff against the current `TOPICS-ORIGINAL.md` if one
exists), the `# Notes` contents (contradictions, cross-topic duplicates,
filtered-out entries), and ask the user to choose:

- **Ignorieren** — discard the draft entirely. Nothing is written — not
  `TOPICS-ORIGINAL.md`, and Step 7 does not run. Same changes are
  re-proposed on the next `/build-topics` run.
- **Übernehmen** — write the draft as the new `.claude/TOPICS-ORIGINAL.md`:
  bump `revision`/`history`, update `vision_revision`, replace `# Topics`/
  `# Exercises`/`# Notes`, and (rebuild case only) replace `# Source Files`
  with the current, complete file/MD5 list. Then proceed to Step 7.
- **Durch Prompts verfeinern** — ask for a prompt, apply it to the
  in-session draft, re-present, repeat. Loops until Ignorieren or
  Übernehmen is chosen.

## Step 7 — Sync `.claude/TOPICS.md`

Runs after any successful write to `.claude/TOPICS-ORIGINAL.md` (Step 3,
or Step 6's Übernehmen branch).

- **If `.claude/TOPICS.md` does not exist yet**: create it by copying the
  `# Topics` and `# Exercises` sections' heading structure (`##` topics,
  `###` subtopics — headings only, no content) from
  `.claude/TOPICS-ORIGINAL.md`. Add empty `# Excluded` and `# New`
  sections. Order: `# Topics`, `# Exercises`, `# Excluded`, `# New`. No
  confirmation step — write directly. Frontmatter:

        ---
        revision: 1
        path: ".claude/TOPICS.md"
        title: "Workshop Topics"
        abstract: "<one-sentence description>"
        state: in progress
        lang: en
        numbersections: false
        finished_sections: [ ]
        topics_original_revision: <revision of TOPICS-ORIGINAL.md just used>
        history:
          - "v1: initial copy of Topics/Exercises headings from TOPICS-ORIGINAL.md rev <n>"
        ---

  Done — nothing further this run.

- **If `.claude/TOPICS.md` already exists**: never touch `# Topics`,
  `# Exercises`, or `# Excluded` — those are under the user's manual
  control from this point on. Only update `# New`:
  - Compare every `## <topic>` / `### <subtopic>` pair just written to
    `.claude/TOPICS-ORIGINAL.md` against **all four** existing sections
    (`# Topics`, `# Exercises`, `# Excluded`, `# New`) of `.claude/TOPICS.md`.
  - Any topic/subtopic not found in any of the four sections → add it to
    `# New`, grouped under its `## <topic>`, heading-only (no content).
  - Entries already present anywhere are left alone — `# New` is not
    cleared and rebuilt from scratch, only appended to with genuinely
    unseen entries. Do not re-add an entry already in `# New`.
  - Bump `revision`/`history`, update `topics_original_revision`. Write
    directly — no confirmation (purely additive, nothing existing is
    altered or removed).

## `TOPICS-ORIGINAL.md` format

    # Topics

    ## <topic>

    ### <subtopic 1>

    <content, if found — omit if none>

    ---

    <content from another source, if any>

    ### <subtopic 2>

    ## <topic 2>

    ...

    # Exercises

    ## <topic>

    ### <subtopic 1>

    ...

    # Notes

    - Contradiction: `<subtopic under Original/Vision.md>` vs. `Original/<file>`: ...
    - Cross-topic duplicate: "<subtopic>" appears under both "<Topic A>" and "<Topic B>"
    - Filtered out (doesn't fit VISION.md guardrails): "<topic/subtopic>" — found in `Original/<file>`

    # Source Files

    | Path | MD5 |
    |---|---|
    | Original/Vision.md | <md5sum> |
    | Original/<file> | <md5sum> |

## `TOPICS.md` format

    # Topics

    ## <topic>

    ### <subtopic 1>

    ### <subtopic 2>

    # Exercises

    ## <topic>

    ### <subtopic 1>

    # Excluded

    ## <topic>

    ### <subtopic 1>

    # New

    ## <topic>

    ### <subtopic 1>

Topics may legitimately repeat across `# Topics` and `# Exercises` (their
subtopics differ). `# Excluded` and `# New` start empty and are populated
as described above/by the user.

## Out of scope

- Does not evaluate the "all subtopics of a topic excluded → topic drops
  out of the workshop" rule — that's documented for a later phase to
  apply when deriving `Contents.md` from `TOPICS.md`, not enforced here.
- Does not modify `# Topics`, `# Exercises`, or `# Excluded` in
  `.claude/TOPICS.md` once it exists — user-owned from creation onward.
- Does not modify `.claude/VISION.md` — read-only dependency.
- Does not create or modify `.claude/TASKS.md` entries.
- Does not touch `.claude/Memory.md`.
