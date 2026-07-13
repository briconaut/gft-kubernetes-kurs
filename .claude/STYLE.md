---
revision: 1
path: ".claude/STYLE.md"
title: "Style Guide"
abstract: "Binding format specifications for generated artifacts: frontmatter header, lesson-file structure, topic/subtopic/subject numbering, and the format of Contents.md, lessons/practice/solution files. Referenced from CLAUDE.md."
state: in progress
lang: en
numbersections: <true|false>
history:
  - "v1: initial version"
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
The numbering is refered to as `<#subtopic>`.
The text of the subtopic is refered to as `<subtopic title>`
The contents of the Level 2 heading is refered to as `<subtopic contents>`

## Subject numbering

Subjects are the bulletpoints of Level 2 headings in `Contents.md`.
These are numbered starting at 1 for each subtopic. 
Numbering format is `<#topic>.<#subtopic>.01`, `<#topic>.<#subtopic>.02`, ... where the `<#topic>` is the topic numbering of their respective topic and the `<#subtopic>` is the subtopic numbering of their respective subtopic.
The numbering is refered to as `<#subject>`.
The first line of the list item is refered to as `<subject title>`.
The full contents of the list item is refered to as `<subject contents>`.

# Frontmatter for Generated `.md` Files

**Applies to:** every generated or regenerated `.md` file in this repository: `Contents.md`, `Practices.md`, every lesson file, every exercise/solution file, and both `Memory.md` levels.

    ---
    revision: <int, starts at 1, incremented on every regenerated version>
    path: <path to the file>
    title: "<title>"
    abstract: "<one-sentence description>"
    state: <not started|in progress|done>
    lang: en
    numbersections: true
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

    ## [<#topic>.<#subtopic> <subtopic title>](<file link to `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md`)

    - [<#topic>.<#subtopic>.<#subject> <subject title>](<file link to `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md#<#topic>.<#subtopic>.<#subject>-<subject title>`>)
      <subject contents if any>

    <repeat for all subject, subtopics and topics>

# Lesson File Format

The files `Contents/<#topic>-<topic title>/<#subtopic>-<subtopic title>.md` contain the frontmatter header.
The overall format of `Contents/<#topic>-<topic title>/<#subtopic>-<subtopic title>.md` is:

    # <#topic> <topic title>

    ## <#topic>.<#subtopic> <subtopic title>

    - <#topic>.<#subtopic>.<#subject> <subject title>
      <subject contents if any>

    <repeat for all subject, for one subtopic and one topic>

# Practice File Format

** TO BE DONE **

# Solution File Format

** TO BE DONE **
