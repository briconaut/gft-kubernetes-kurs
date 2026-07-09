---
revision: 3
path: ".claude/STYLE.md"
title: "Style Guide"
abstract: "Binding format specifications for generated artifacts: frontmatter header, lesson-file structure, and the format of Contents.md. Referenced from CLAUDE.md."
state: in progress
lang: en
numbersections: true
finished_sections: [ ]
history:
  - "v1: extracted from CLAUDE.md v14 (Frontmatter for generated .md files, Lesson File Body Format) per user request. Added a new 'Format of Contents.md' section, consolidating rules previously scattered across CLAUDE.md → Process/Phases and .claude/Memory.md → 'Folder & lesson-file numbering convention' into a single explicit style spec."
  - "v2: documented the bullet-anchor-link convention (Task 2.3.1) in 'Format of Contents.md' — Contents.md's bullets were changed to link to their lesson-file anchor via /improve, but that change intentionally left this file unedited at the time; Task 3.1 review reconciles the spec with the actual, now-established format."
  - "v3: documented the heading-numbering convention added to Contents.md's `#`/`##` headings per direct user request — `# <folder-nr> - <title>` and `## <folder-nr>.<lesson-nr> - <title>`, derived from the existing `folder:`/`lesson:` comments; unnumbered exceptions (Further Reading, Practice headings) match the pre-existing folder:/lesson:-comment exclusions"
---

# Style Guide

This file collects the binding format rules for generated artifacts. `CLAUDE.md` remains the single source of truth for scope, phases, and process — consult this file whenever a task involves producing or editing one of the file types below. Practices.md's analogous format is not yet defined; it will be added here once Phase 5 planning fixes it.

# Numbering

## Workshop topic numbering

Workshop topics are the Level 1 headings in `Contents.md` except `# Further Reading / Links`.
These are numbered starting at 1. 
Numbering format is `01`, `02`, ...
The numbering is refered to as `<#topic>`.

## Workshop subtopic numbering

Workshop topics are the Level 1 headings in `Contents.md`.
These are numbered starting at 1. 
Numbering format is `<topic-number>.01`, `<topic-number>.02`, ... where the `<topic-number>` is the topic numbering of their respective topic.
The numbering is refered to as `<#subtopic>`.

## Subject numbering

Subjects are the bulletpoints of Level 2 headings in `Contents.md`.
These are numbered starting at 1. 
Numbering format is `<topic-number>.<subtopic-number>.01`, `<topic-number>.<subtopic-number>.02`, ... where the `<topic-number>.<subtopic-number>` is the subtopic numbering of their respective subtopic.
This numbering is exclusively used to identify a subjet in the prompts. It never appears in workshop related contents but is allowed in the scaffolding (`.claude/TASKS.md`, `.claude/MEMORY.md`, ... )
The numbering is refered to as `<#subject>`.

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
    history: [ ]
    ---

Rules:
- `state` must be exactly one of `not started`, `in progress`, `done` — no other values.
- On regeneration: increment `revision`; move `state` from `not started` to `in progress`. Claude Code never sets `done` — that's set manually by the workshop author.
- Append one entry to `history` per regenerated version, summarizing what changed.
- Additional information may be present and will remain untouched.

