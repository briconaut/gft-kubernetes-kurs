---
revision: 1
path: ".claude/STYLE.md"
title: "Style Guide"
abstract: "Binding format specifications for generated artifacts: frontmatter header, lesson-file structure, and the format of Contents.md. Referenced from CLAUDE.md."
state: in progress
lang: en
numbersections: true
finished_sections: [ ]
history:
  - "v1: extracted from CLAUDE.md v14 (Frontmatter for generated .md files, Lesson File Body Format) per user request. Added a new 'Format of Contents.md' section, consolidating rules previously scattered across CLAUDE.md → Process/Phases and .claude/Memory.md → 'Folder & lesson-file numbering convention' into a single explicit style spec."
---

# Style Guide

This file collects the binding format rules for generated artifacts. `CLAUDE.md` remains the single source of truth for scope, phases, and process — consult this file whenever a task involves producing or editing one of the file types below. Practices.md's analogous format is not yet defined; it will be added here once Phase 5 planning fixes it.

# Frontmatter for Generated `.md` Files

**Applies to:** every generated or regenerated `.md` file in this repository, in every phase — `Contents.md`, `Practices.md`, every lesson file, every exercise/solution file, and both `Memory.md` levels.

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

# Lesson File Format

**Applies to:** `Contents/<nr>-<section>/<local-nr>-<lesson>.md` files. Produced in two stages by two different phases:
- **Phase 2** creates the file with this structure as an empty skeleton (placeholders instead of prose).
- **Phase 4** fills in the prose, without altering the structure fixed in Phase 2.

**Phase 2 — skeleton:** create the file with frontmatter (`state: not started`, per Frontmatter format above) and this body — no explanatory prose yet:

    # <title of the enclosing `#` section heading> / <title of the `##` topic heading>

    ## Overview

    - [<bullet 1 text, verbatim>](#<anchor-of-bullet-1>)
    - [<bullet 2 text, verbatim>](#<anchor-of-bullet-2>)
    - ...

    ## <bullet 1 text, verbatim>

    _Content pending (Phase 4)._

    ## <bullet 2 text, verbatim>

    _Content pending (Phase 4)._

    ...

**Phase 4 — content:** replace each `_Content pending (Phase 4)._` placeholder with the actual explanatory prose for that bullet — a concise explanation in the audience's terms, consistent with `CLAUDE.md` → Language and audience conventions. Once a file's placeholders are all replaced, bump `state` to `in progress` per the Frontmatter format above. The H1, `## Overview` links, and the `##` bullet headings themselves are fixed in Phase 2 and must **not** be changed in Phase 4 — Phase 4 only fills in prose beneath them.

Rules (apply to both stages):
- The H1 combines the enclosing `#` section title and the `##` topic title from `Contents.md`, joined by ` / ` — no numbering, no folder slug (e.g. `# Kubernetes Architecture / What is a cluster, and what is a node?`).
- `## Overview` is a table of contents: one link per bullet under this topic's `##` heading in `Contents.md`, in original order, pointing to that bullet's own `##` section further down in the same file.
- Anchor slugs follow the standard GitHub heading-anchor convention: lowercase, spaces → `-`, strip everything outside `[a-z0-9-]` (drops punctuation, backticks, parentheses), collapse repeated `-`. Most Markdown renderers (incl. GitHub) generate this automatically from the heading text, so it only needs to be computed explicitly for link validation.
- Every bullet from `Contents.md` becomes its own `##` heading, using the bullet's exact text verbatim — including any `(brief mention)` suffix. No rewording, no merging or splitting of bullets.
- Heading level stays flat: no `###` subheadings within a bullet's section, to keep lesson files skimmable and consistent across modules.
- `## Practice: ...` topics in `Contents.md` are out of scope for this format — they get no lesson file (Phase 8 handles exercises separately).

# Format of `Contents.md`

**Applies to:** `Contents.md` itself. Established in Phase 1 (topic list); extended with structural comments in Task 1.3/1.3.1; kept in sync (topic headings turned into links) in Phase 2.3. The overall structure must not change outside these phases, except via `/improve` follow-up.

Structure, top to bottom:
- One `#` top-level heading per section, each immediately followed by a `<!-- folder: <nr>-<section> -->` HTML comment giving its stable Phase-2 folder name (global sequence `01`–`13`).
- Within a section, one `##` heading per topic, phrased as a concrete, answerable question in the audience's terms (e.g. "What is a Pod?") rather than an abstract chapter title. Each is immediately followed by a `<!-- lesson: Contents/<nr>-<section>/<local-nr>-<lesson>.md -->` HTML comment giving its stable Phase-2 lesson-file path (local sequence restarting at `01` within each section — see `CLAUDE.md` → Folder & File Conventions).
- Directly under each `##` topic heading, a flat bullet list answering that question — headings + bullet points only, **no explanatory prose**. Established practice targets at least ~6 bullets per topic for completeness (per Task 1.1.1); review new topics against this bar.
- Exercise placeholder headings use `## Practice: ...` instead of a question, carry **no** `lesson:` comment (Phase 8 uses its own `<nr>.<subnr>` scheme derived from `Practices.md`, not from these comments), and have no bullet-count expectation.
- The final section, `# Further Reading / Links`, is reference-only: a flat list of links, no `folder:`/`lesson:` comments, no Phase-2 folder at all.
- Both comment kinds are HTML comments (invisible in rendered Markdown) — they don't violate the "headings + bullets only" rule. Later phases should `grep` `Contents.md` for `folder:`/`lesson:` to get exact paths rather than re-deriving slugs from heading text.
- Once a topic heading has a corresponding lesson file (Phase 2.3), the heading text itself becomes a Markdown link to that file, with the `<!-- lesson: ... -->` comment left in place underneath it.
