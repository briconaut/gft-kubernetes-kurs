---

revision: 1
path: ".claude/TASK-EXECUTION.md"
title: "Task Execution"
abstract: "Binding process for executing slide-generation tasks from .claude/TASKS.md."
state: in progress
lang: en
numbersections: true
history:

* "v1: extracted task execution process from CLAUDE.md."

---

# Task Execution

## Purpose

This file defines how tasks from `.claude/TASKS.md` are selected, executed, validated, and updated.

It is read only when the user's current prompt explicitly requests one of these execution modes:

* **Next task**
* **Next subtopic**

The binding syntax and validation rules for `.claude/TASKS.md` are defined in `.claude/STYLE-TASKS.md`.

## Authoritative Files

When task execution is explicitly requested, read these files in order:

1. `.claude/TASK-EXECUTION.md`
2. `.claude/STYLE-TASKS.md`
3. `.claude/TASKS.md`
4. `.claude/STYLE.md`
5. `Contents.md`

The selected task invokes the `fill-slide` skill. That skill reads its own authoritative files as defined by its `SKILL.md`.

## Execution Authorization

A task may be executed only when the user's current prompt explicitly requests:

* the next task; or
* the next Subtopic.

Semantically equivalent wording is allowed when the execution intent and mode are unambiguous.

The following requests do not authorize execution:

* show or list tasks;
* summarize task progress;
* inspect task statuses;
* validate the task file;
* explain the task workflow;
* edit the task-file format;
* create or regenerate the task list.

When execution is not authorized:

* do not invoke `fill-slide`;
* do not change task statuses;
* do not add or remove blocker metadata.

## Supported Execution Modes

Only these execution modes are supported:

1. **Next task**
2. **Next subtopic**

Do not execute:

* all remaining tasks;
* an entire Topic;
* an arbitrary task range;
* a specifically selected later task;
* tasks in parallel.

## Task Statuses

The supported statuses are:

* `[ ]` **Open** — execution has not started.
* `[~]` **In Progress** — execution started but did not finish.
* `[R]` **Needs Rework** — execution must be repeated after review or changed information.
* `[B]` **Blocked** — execution cannot currently be completed.
* `[X]` **Done** — execution and structural validation completed successfully.

`[X]` means technically completed. It does not imply manual approval.

## Allowed Status Transitions

The agent may perform these transitions:

* `[ ]` → `[~]` when execution starts.
* `[R]` → `[~]` when rework starts.
* `[~]` → `[X]` after successful execution and validation.
* `[~]` → `[B]` when execution cannot be completed.
* `[B]` → `[~]` when the documented blocker has been resolved.

The agent must not:

* set a task to `[R]`;
* reset an `[X]` task;
* skip an earlier incomplete task;
* mark a task `[X]` when `fill-slide` aborts;
* mark a task `[X]` when validation fails.

Only the user or an explicit review process may change `[X]` to `[R]`.

## Task Ordering

Tasks are ordered by their full Subject number:

```text
<#topic>.<#subtopic>.<#subject>
```

The order in `.claude/TASKS.md` must match the Subject order in `Contents.md`.

A task is incomplete when its status is one of:

```text
[ ]
[~]
[R]
[B]
```

The first incomplete task is the task with the lowest Subject number whose status is not `[X]`.

No task after the first incomplete task may be processed unless it belongs to the same selected Subtopic during **Next subtopic** execution.

## Initial Validation

Before selecting a task:

1. Validate the complete `.claude/TASKS.md` against `.claude/STYLE-TASKS.md`.
2. Verify its Topic, Subtopic, Subject, title, and ordering information against `Contents.md`.
3. Stop without changing any status when validation fails.
4. Report the precise validation error.

If every task has status `[X]`, report that all tasks are complete and modify no files.

## Selecting the First Task

Find the first task in numeric order whose status is not `[X]`.

Handle its status as follows:

### Open

For `[ ]`, begin execution and change the task to `[~]`.

### Needs Rework

For `[R]`, begin rework and change the task to `[~]`.

### In Progress

For `[~]`, resume execution.

Before resuming, inspect the target Slide to determine whether the previous execution produced a complete, partial, or unchanged result.

### Blocked

For `[B]`:

1. Read the task's `blocker` metadata.
2. Read the referenced `Memory.md`.
3. Determine whether the documented blocker has been resolved.

When resolved:

1. Remove the obsolete `blocker` metadata.
2. Update or remove the obsolete blocker information in `Memory.md`.
3. Change `[B]` to `[~]`.
4. Resume execution.

When unresolved:

1. Leave the task `[B]`.
2. Execute no task.
3. Report the blocker and the information required to resolve it.

## Execution Mode: Next Task

When the user requests **Next task**:

1. Select the first task whose status is not `[X]`.
2. Execute only that task.
3. Validate the result.
4. Stop after the task becomes:

   * `[X]`; or
   * `[B]`.

Never process a second task during this execution mode.

## Execution Mode: Next Subtopic

When the user requests **Next subtopic**:

1. Select the first task whose status is not `[X]`.

2. Determine its full Subtopic number from the first two components of its Subject number:

   ```text
   <#topic>.<#subtopic>
   ```

3. Fix this value as the selected Subtopic for the complete invocation.

4. Process the selected task.

5. Continue in ascending Subject order with every remaining task belonging to the same selected Subtopic.

6. Skip tasks in the selected Subtopic that already have status `[X]`.

7. Stop after the last task belonging to the selected Subtopic.

Do not continue into the next Subtopic.

Stop immediately when:

* a task becomes `[B]`;
* `fill-slide` aborts;
* task-file validation fails;
* Slide validation fails;
* a required read or write operation fails.

## Executing a `fill-slide` Task

For the selected task, invoke `fill-slide` logically as:

```text
/fill-slide "<subject number>" <element type> <prompt>
```

Use:

* `<subject number>` from the task header;
* `<element type>` from the task header;
* `<prompt>` exclusively from the task's `prompt` metadata.

Do not add these values to the Prompt:

* Subject number;
* Subject title;
* Subject contents;
* element type;
* task status;
* blocker information.

The `fill-slide` skill resolves the Subject title and Subject contents independently from `Contents.md`.

The current `fill-slide` interface accepts a full Subject number, one of the four supported element types, and an optional Prompt.

## Pre-Execution Checks

Before invoking `fill-slide`:

1. Resolve the Subject number in `Contents.md`.
2. Verify that it resolves exactly once.
3. Verify that the task's `subject` metadata exactly matches `<subject title>`.
4. Verify that the task is located under the correct Topic and Subtopic.
5. Verify that its element type is supported.
6. Verify that its Prompt is non-empty.
7. Change `[ ]` or `[R]` to `[~]`.
8. Persist the status change according to the frontmatter rules.

## Successful Results

These `fill-slide` results are potentially successful:

* `created`
* `added`
* `replaced`
* `unchanged`

After such a result:

1. Validate the complete target Slide.
2. Verify that the target Step exists exactly once.
3. Verify that the Step uses the requested element type.
4. Verify that the Step uses the expected render mode.
5. Verify that all Elements are structurally valid.
6. Verify that unrelated Steps remain present.
7. Change the task to `[X]`.

An `unchanged` result may be marked `[X]` when the existing Step passes all validation checks.

## Failed Results

When `fill-slide` returns `aborted`, or when result validation fails:

1. Change the task from `[~]` to `[B]`.
2. Record the full blocker in the relevant topic-scoped `Memory.md`.
3. Add one `blocker` metadata field to the task.
4. Stop the current execution mode.

Do not mark a task `[X]` solely because a file was modified.

## Blocker Metadata

A blocked task contains:

```markdown
  - blocker: `<Memory.md path>` — <one-line blocker summary>
```

Example:

```markdown
  - blocker: `Contents/03-Kubernetes Architecture/Memory.md` — required source information is unavailable.
```

The one-line task metadata is a pointer only.

The referenced `Memory.md` contains:

* what is blocked;
* why it is blocked;
* what is required to resolve it.

## Updating `.claude/TASKS.md`

During task execution, the agent may modify only:

* statuses of tasks processed in the current invocation;
* `blocker` metadata for the currently processed task;
* frontmatter fields required by the generated Markdown rules.

The agent must not:

* add tasks;
* remove tasks;
* reorder tasks;
* renumber tasks;
* change Subject titles;
* change element types;
* change Prompts;
* restructure Topic or Subtopic sections.

Those changes require a separate explicit task-list maintenance request.

## Persistence Rules

Each persisted modification of `.claude/TASKS.md` must:

* increment `revision` by exactly one;
* preserve unknown frontmatter fields;
* preserve `state: done`;
* change `state: not started` to `state: in progress`;
* append exactly one concise `history` entry.

Multiple status changes written in one atomic file update increment the revision only once.

A status must be persisted before executing work that depends on that status.

## Result Report

After **Next task**, report:

* processed Subject number;
* final status;
* generated Slide path;
* `fill-slide` result;
* blocker or validation error, if present.

After **Next subtopic**, report:

* selected Subtopic number and title;
* Subject numbers completed during the invocation;
* first remaining incomplete task, if any;
* blocker or validation error, if present.

