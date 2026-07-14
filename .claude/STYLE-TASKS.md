---

revision: 1
path: ".claude/STYLE-TASKS.md"
title: "Task File Specification"
abstract: "Binding format and validation rules for the slide-generation task file."
state: in progress
lang: en
numbersections: true
history:

* "v1: initial task-file specification."

---

# Task File Specification

## Purpose

This file defines the binding syntax, structure, ordering, and validation rules for:

```text
.claude/TASKS.md
```

It does not contain executable tasks.

Task execution order, status transitions, and execution modes are defined in `CLAUDE.md`.

## Authoritative Sources

Task-file generation and validation use:

1. `.claude/STYLE.md` for numbering terminology and generic Markdown frontmatter.
2. `Contents.md` for Topics, Subtopics, Subjects, titles, and ordering.
3. The `fill-slide` skill for supported element types and task execution.
4. This file for the structure of `.claude/TASKS.md`.

## Frontmatter

`.claude/TASKS.md` must start with:

```yaml
---
revision: 1
path: ".claude/TASKS.md"
title: "Slide Generation Tasks"
abstract: "Ordered fill-slide tasks for the workshop Subjects."
state: in progress
lang: en
numbersections: false
format: workshop-tasks
format_version: 1
history:
  - "v1: created slide generation task list."
---
```

Rules:

* `format` must be `workshop-tasks`.
* `format_version` must be `1`.
* Generic frontmatter rules from `.claude/STYLE.md` apply.
* Every persisted task-status or blocker change increments `revision`.
* Every persisted change appends exactly one concise `history` entry.
* Multiple task changes written in one file update increment `revision` only once.

## Topic Sections

Each Topic containing tasks is represented by a Level 1 heading:

```markdown
# <#topic> <topic title>
```

Example:

```markdown
# 01 Local Kubernetes Cluster Setup
```

Rules:

* The number must exactly match `Contents.md`.
* The title must exactly match `Contents.md`.
* Topics must appear in ascending numeric order.
* A Topic without tasks may be omitted.

## Subtopic Sections

Each Subtopic containing tasks is represented by a Level 2 heading:

```markdown
## <#topic>.<#subtopic> <subtopic title>
```

Example:

```markdown
## 01.01 Installing Docker Desktop
```

Rules:

* `<#subtopic>` is the local two-digit Subtopic number.
* `<#subtopic>` never contains `<#topic>`.
* The heading displays the full number `<#topic>.<#subtopic>`.
* The Topic component must match the enclosing Level 1 heading.
* The title must exactly match `Contents.md`.
* Subtopics must appear in ascending numeric order within their Topic.
* A Subtopic without tasks may be omitted.

## Task Syntax

Each task is a top-level Markdown list item:

```markdown
- [<status>] fill-slide <#topic>.<#subtopic>.<#subject> <element type>
```

Example:

```markdown
- [ ] fill-slide 01.01.01 text
```

Rules:

* The leading `-` list marker is mandatory.
* The task status must be enclosed in square brackets.
* The command must be exactly `fill-slide`.
* The Subject number must have the exact form `NN.NN.NN`.
* A trailing period after the Subject number is not allowed.
* The element type must be exactly one of:

  * `text`
  * `code`
  * `image`
  * `diagram`
* No Prompt text may appear on the task-header line.

## Status Characters

The following status characters are valid:

```text
[ ] Open
[~] In Progress
[R] Needs Rework
[B] Blocked
[X] Done
```

No other status character is allowed.

Status semantics and transitions are defined in `CLAUDE.md`.

## Task Metadata

Each task must contain these indented metadata fields in this order:

```markdown
  - subject: <subject title>
  - prompt: |
      <prompt contents>
```

A blocked task additionally contains:

```markdown
  - blocker: `<Memory.md path>` — <one-line blocker summary>
```

Unknown metadata fields are not allowed.

## Subject Metadata

The `subject` field is mandatory.

Syntax:

```markdown
  - subject: <subject title>
```

Example:

```markdown
  - subject: Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
```

Rules:

* The value must exactly equal `<subject title>` from `Contents.md`.
* The Subject number is not included in the value.
* The value is validation and readability metadata.
* The value is never passed to `fill-slide` as Prompt content.

`<subject contents>` must not be copied into `.claude/TASKS.md`.

The `fill-slide` skill reads `<subject contents>` directly from `Contents.md`.

## Prompt Metadata

The `prompt` field is mandatory.

Syntax:

```markdown
  - prompt: |
      <prompt contents>
```

Example:

```markdown
  - prompt: |
      Present the installation workflow as a concise visual sequence.
      Cover obtaining the installer, completing installation, starting
      Docker Desktop, and verifying that it is operational.
```

Rules:

* The Prompt must contain at least one non-whitespace character.
* All lines indented beneath `prompt: |` belong to the Prompt.
* The common indentation prefix is removed before invocation.
* The Prompt ends at:

  * the next metadata item at the task metadata indentation level;
  * the next task;
  * the next Subtopic;
  * the next Topic;
  * or the end of the file.
* The Prompt is passed to `fill-slide` without automatically adding metadata.
* The Prompt must not automatically include:

  * `<subject number>`;
  * `<subject title>`;
  * `<subject contents>`;
  * element type;
  * status;
  * blocker information.
* The Prompt may refer to the Subject semantically, but it must not duplicate the Subject title merely to identify the target.
* An empty Prompt is invalid for `.claude/TASKS.md`.

An empty direct `fill-slide` Prompt would generate placeholders. Task-file entries are intended to generate completed content and therefore require a non-empty Prompt.

## Blocker Metadata

A task with status `[B]` must contain exactly one `blocker` field:

```markdown
  - blocker: `<Memory.md path>` — <one-line blocker summary>
```

Example:

```markdown
  - blocker: `Contents/01-Local Kubernetes Cluster Setup/Memory.md` — required installation screenshot is unavailable.
```

Rules:

* The path must point to the relevant global or topic-scoped `Memory.md`.
* The summary must fit on one line.
* Full blocker details belong in the referenced `Memory.md`.
* A task whose status is not `[B]` must not contain a `blocker` field.
* The `blocker` field follows the `prompt` field.

## Complete Example

```markdown
---
revision: 1
path: ".claude/TASKS.md"
title: "Slide Generation Tasks"
abstract: "Ordered fill-slide tasks for the workshop Subjects."
state: in progress
lang: en
numbersections: false
format: workshop-tasks
format_version: 1
history:
  - "v1: created slide generation task list."
---

# 01 Local Kubernetes Cluster Setup

## 01.01 Installing Docker Desktop

- [ ] fill-slide 01.01.01 text
  - subject: Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
  - prompt: |
      Present the installation workflow as a concise conceptual sequence.
      Cover obtaining the correct installer, completing installation,
      starting Docker Desktop, and verifying successful operation.

- [ ] fill-slide 01.01.02 image
  - subject: Enable Kubernetes in Docker Desktop's settings/preferences
  - prompt: |
      Define a progressive visual sequence showing where Kubernetes is
      enabled in Docker Desktop and how the user recognizes that cluster
      provisioning has completed successfully.

- [B] fill-slide 01.01.03 diagram
  - subject: Docker Desktop provisions a single-node, kubeadm-based Kubernetes cluster
  - prompt: |
      Show the relationship between Docker Desktop, the local Kubernetes
      cluster, the Control Plane components, and the Worker Node role.
  - blocker: `Contents/01-Local Kubernetes Cluster Setup/Memory.md` — required architecture decision is unresolved.

## 01.02 Installing Rancher Desktop

- [ ] fill-slide 01.02.01 text
  - subject: Download and install Rancher Desktop for your operating system (Windows/macOS/Linux)
  - prompt: |
      Present the installation workflow and identify the major decisions
      the user must make during the initial setup.
```

## Prompt Isolation

For this task:

```markdown
- [ ] fill-slide 01.01.01 text
  - subject: Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
  - prompt: |
      Present the installation workflow as a concise conceptual sequence.
```

The effective invocation is logically equivalent to:

```text
/fill-slide "01.01.01" text "Present the installation workflow as a concise conceptual sequence."
```

The following values are not part of the Prompt:

```text
01.01.01
text
Download and install Docker Desktop for your operating system (Windows/macOS/Linux)
[ ]
```

## Ordering Rules

Tasks must follow the order in `Contents.md`.

Rules:

* Topics are ordered by `<#topic>`.
* Subtopics are ordered by `<#subtopic>` within their Topic.
* Tasks are ordered by `<#subject>` within their Subtopic.
* Each full Subject number may occur at most once.
* A task must appear beneath the Topic and Subtopic to which its Subject belongs.
* The Topic component of the Subject number must match the enclosing Topic.
* The Subtopic component of the Subject number must match the enclosing Subtopic.
* Tasks must not be reordered by:

  * status;
  * element type;
  * generated Slide path;
  * expected complexity.
* Multiple consecutive tasks may modify the same `.slide.md` file.

## Synchronization with `Contents.md`

For every task:

* the Subject number must resolve uniquely in `Contents.md`;
* the enclosing Topic heading must match the resolved Topic;
* the enclosing Subtopic heading must match the resolved Subtopic;
* the `subject` field must exactly match the resolved `<subject title>`;
* the task order must match the Subject order in `Contents.md`.

If any value is stale or inconsistent, `.claude/TASKS.md` is invalid.

`<subject contents>` are intentionally not duplicated in the task file.

## Validation Rules

`.claude/TASKS.md` is invalid if any of the following applies:

* Frontmatter is missing or invalid.
* `format` is not `workshop-tasks`.
* `format_version` is not supported.
* A Topic heading does not match `Contents.md`.
* A Subtopic heading does not match `Contents.md`.
* A Topic or Subtopic is out of numeric order.
* A task is not a top-level Markdown list item.
* A task uses an unknown status.
* A task command is not exactly `fill-slide`.
* A task lacks a valid Subject number.
* A Subject number contains a trailing period.
* A Subject number occurs more than once.
* A task is grouped under the wrong Topic or Subtopic.
* A task is out of Subject order.
* A task lacks a supported element type.
* A task lacks the `subject` field.
* A task lacks the `prompt` field.
* A Prompt is empty.
* A `subject` value differs from `Contents.md`.
* `<subject contents>` are duplicated in task metadata.
* Metadata fields appear in the wrong order.
* Unknown metadata fields are present.
* A task with status `[B]` lacks a `blocker` field.
* A task whose status is not `[B]` contains a `blocker` field.

When validation fails:

* no task may be executed;
* no task status may be modified;
* the precise validation error must be reported.

