---
name: build-contents
description: Synchronize a Kubernetes course Contents.md with .claude/TOPICS.md at Topic/Subtopic level, preserving existing Subject content where possible, moving removed Topics/Subtopics (including all their Subjects) to Contents-removed.md, and rebuilding numbering, links, and comments exactly as specified in .claude/STYLE.md. Does not create, rename, or edit lesson/practice/solution content files.
---

# build-contents

Use this skill when the user wants `Contents.md` rebuilt from `.claude/TOPICS.md` while preserving existing Subject content and moving obsolete Topics/Subtopics out of the active contents file.

This skill only maintains the structure of `Contents.md` itself (Topics, Subtopics, Subjects, their numbering, links, and comments) and `Contents-removed.md`. It never creates, renames, or edits the actual `.lesson.md` / `.practice.md` / `.solution.md` content files — those are out of scope, to avoid any conflict with `.claude/STYLE.md`'s file-format specifications for those files.

## Inputs

- `.claude/TOPICS.md`
- `Contents.md`
- `.claude/STYLE.md` — authoritative for all naming, numbering, and formatting conventions used below. Read it before making any change; if this skill's instructions and `.claude/STYLE.md` ever appear to disagree, `.claude/STYLE.md` wins.
- Optional existing `Contents-removed.md`

## Output files

- Updated `Contents.md`
- Appended/updated `Contents-removed.md`, containing Topics/Subtopics (with all their Subjects) that exist in `Contents.md` but no longer exist in `.claude/TOPICS.md`

Not in scope: `.lesson.md`, `.practice.md`, `.solution.md` files, and any per-module `Memory.md`. This skill never creates, renames, or edits them.

## Terminology and formatting

Use "Topic", "Subtopic", and "Subject" exactly as defined in `.claude/STYLE.md` → Numbering (Level-1 heading = Topic, Level-2 heading = Subtopic, bullet point under a Subtopic = Subject). Do not use other terms (e.g. "Point", "Step") for these.

All of the following are taken directly from `.claude/STYLE.md` and are not restated here — re-read them before formatting output:

- Topic/Subtopic/Subject numbering format → `.claude/STYLE.md` → Numbering.
- Heading, link, and file-path format for `Contents.md` → `.claude/STYLE.md` → Format of Contents.md.
- Any generated HTML comments (e.g. lesson/anchor references) → `.claude/STYLE.md` → Format of Contents.md.

## Source interpretation

### `.claude/TOPICS.md`

- Read only the section below the level-1 heading `# Topics`.
- Inside that section, Level-2 headings (`##`) are canonical Topics and Level-3 headings (`###`) are canonical Subtopics.
- Ignore all other heading levels and all body content.
- Ignore numbering prefixes in headings.
- Ignore markdown links in headings; compare only the visible link text.

### `Contents.md`

- Preserve YAML frontmatter as-is.
- Treat headings as Topics/Subtopics per `.claude/STYLE.md` → Numbering.
- Ignore numbering prefixes when comparing headings.
- Ignore markdown links in headings; compare only the visible link text.
- Preserve existing content under kept Subtopics — including all Subjects — except for generated numbering, generated comments, and generated Subject links/comments, which are rebuilt per `.claude/STYLE.md`.

### Subjects

- A Subject exists only when a Subtopic body consists exclusively of a top-level markdown list, ignoring blank lines and generated HTML comments.
- Each top-level list item is one Subject.
- Ignore numbering prefixes and markdown links when comparing or renumbering Subject titles.
- `.claude/TOPICS.md` does not track Subjects — reconciliation against `.claude/TOPICS.md` happens at Topic/Subtopic level only. Subject content under a kept Subtopic is preserved as-is, never regenerated or reconciled by this skill (that's `/fill-subtopic`'s job).

## Reconciliation rules

1. Compare Topics and Subtopics by normalized title:
   - Remove existing numbering prefixes.
   - Replace markdown links with their visible text.
   - Collapse internal whitespace.
   - Compare case-sensitively after normalization unless the user explicitly requests case-insensitive matching.
2. The canonical Topic/Subtopic order comes from `.claude/TOPICS.md`.
3. A Topic/Subtopic present in `.claude/TOPICS.md` but missing in `Contents.md` is inserted into `Contents.md` at the canonical position, empty (no Subjects) until `/fill-subtopic` populates it.
4. A Topic/Subtopic present in both files keeps its existing body content, including all of its Subjects, unchanged.
5. A Topic/Subtopic present in `Contents.md` but missing in `.claude/TOPICS.md` is removed from `Contents.md` and appended to `Contents-removed.md`, together with all of its Subjects — preserved verbatim (numbering, links, comments, nested content) exactly as they appeared in `Contents.md`, not summarized or reformatted.
6. If a whole Topic is removed, move the full Topic block, including all Subtopics and all of their Subjects.
7. If only individual Subtopics are removed from a kept Topic, move those Subtopic blocks — including all of their Subjects — under a heading for the parent Topic in `Contents-removed.md`.

## Numbering, links, and comments

After reconciliation, rebuild `Contents.md`'s numbering, headings, links, and any generated comments exactly as specified in `.claude/STYLE.md` → Numbering and → Format of Contents.md. Do not invent or reuse any numbering/path/comment convention not documented there — if something needed here isn't covered by `.claude/STYLE.md`, stop and ask whether to extend `.claude/STYLE.md` first, rather than improvising.

## `Contents-removed.md` format

    -------------------------------------------------------------------------------

    # Removed Topics/Subtopics

    ## <topic title>

    ### <subtopic title>

    Moved from `Contents.md` by `build-contents`.

    <original Subject list, verbatim>

If `Contents-removed.md` already exists, append a new removal block; do not overwrite previous removals.

## Out of scope

- Does not create, rename, or edit `.lesson.md`, `.practice.md`, or `.solution.md` files.
- Does not reconcile or regenerate Subject content — only whole Topic/Subtopic presence/absence is reconciled against `.claude/TOPICS.md`.
- Does not modify `.claude/TOPICS.md`.
- Does not touch `.claude/Memory.md` or any per-module `Memory.md`.

## Response after execution

After editing, report briefly:

- Which Topics/Subtopics were inserted, kept, or removed.
- Whether `Contents-removed.md` was created or appended to.
- Any ambiguity encountered during matching, if applicable.
