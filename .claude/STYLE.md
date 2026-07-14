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
  - "v1: intial version"
---

# Style Guide

This file collects the binding format rules for generated artifacts. `CLAUDE.md` remains the single source of truth for scope and process — consult this file whenever a task involves producing or editing one of the file types below. Practices.md's analogous format is not yet defined; it will be added here at a later point in time.

# Numbering

## Workshop topic numbering

Workshop topics are the Level 1 headings in `Contents.md` except `# Further Reading / Links`.
These are numbered starting at 1. 
Numbering format is `01`, `02`, ...
The numbering is refered to as `<#topic>`.
The text of the topic is refered to as `<topic title>`
The contents of the Level 1 heading is refered to as `<topic contents>`

## Workshop subtopic numbering

Workshop subtopics are the Level 2 headings in `Contents.md`.
These are numbered starting at 1 for each topic. 
Numbering format is `<#topic>.01`, `<#topic>.02`, ... where the `<#topic>` is the topic numbering of their respective topic.
The numbering after `<#topic>.` is refered to as `<#subtopic>`.
The text of the subtopic is refered to as `<subtopic title>`
The contents of the Level 2 heading is refered to as `<subtopic contents>`

## Subject numbering

Subjects are the bulletpoints of Level 2 headings in `Contents.md`.
These are numbered starting at 1 for each subtopic. 
Numbering format is `<#topic>.<#subtopic>.01`, `<#topic>.<#subtopic>.02`, ... where the `<#topic>` is the topic numbering of their respective topic and the `<#subtopic>` is the subtopic numbering of their respective subtopic.
The numbering after `<#topic>.<#subtopic>.` is refered to as `<#subject>`.
The first line of the list item is refered to as `<subject title>`.
The full contents of the list item is refered to as `<subject contents>`.

# Frontmatter for Generated `.md` Files

**Applies to:** every generated or regenerated `.md` file in this repository.

    ---
    revision: <int, starts at 1, incremented on every regenerated version>
    path: <path to the file>
    title: "<title>"
    abstract: "<one-sentence description>"
    state: <not started|in progress|done>
    lang: en
    numbersections: <true|false>
    history: [ ]
    ---

Rules:
- `state` must be exactly one of `not started`, `in progress`, `done` — no other values.
- On regeneration: increment `revision`; move `state` from `not started` to `in progress`. Claude Code never sets `done` — that's set manually by the workshop author.
- Append one entry to `history` per regenerated version, summarizing what changed.
- Additional information may be present and will remain untouched.

# Format of Contents.md

`Contents.md` contains the frontmatter header.
The overall format of `Contents.md` is:

    # <#topic> <topic title>

    ## [<#topic>.<#subtopic> <subtopic title>](<file link to `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md`>)
    <!-- lesson: Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md -->

    - [<#topic>.<#subtopic>.<#subject> <subject title>](<file link to `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md#<#topic>.<#subtopic>.<#subject>-<subject title>`>)
      <!-- anchor: Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md#<#topic>.<#subtopic>.<#subject>-<subject title> -->
      <subject contents if any>

    <repeat for all subject, subtopics and topics>

## Generated HTML comments

Directly below each Subtopic heading and each Subject list item, `Contents.md` carries a generated HTML comment mirroring that entry's file link. These comments let skills and tooling locate the target file/anchor without re-parsing the markdown link syntax, and let a stale link be detected against its comment.

- **Subtopic level** — `<!-- lesson: <path> -->`, placed directly below the Subtopic heading. `<path>` is the same lesson-file path used in the heading's link, without the `Contents/…` link wrapper.
- **Subject level** — `<!-- anchor: <path>#<anchor> -->`, placed directly below the Subject's list item (before any `<subject contents>`). `<path>#<anchor>` is the same path+anchor used in the Subject's link.

Rules:
- If the comment is missing for a Subtopic/Subject that should have one per the format above, create it.
- If the comment already exists but no longer matches the current link (e.g. after a rename/renumber), update it to match — never leave a stale comment.
- Comments use `lesson` at Subtopic level and `anchor` at Subject level — no other comment keys are used in `Contents.md`.

# Lesson File Format

The files `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md` contain the frontmatter header.
The overall format of `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md` is:

    # <#topic> <topic title>

    ## <#topic>.<#subtopic> <subtopic title>

    - <#topic>.<#subtopic>.<#subject> <subject title>
      <subject contents if any>

    <repeat for all subject, for one subtopic and one topic>

# Practice File Format

** TO BE DONE **

# Solution File Format

** TO BE DONE **

