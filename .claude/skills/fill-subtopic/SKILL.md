---
name: fill-subtopic
description: Fill exactly one selected subtopic in Contents.md with a concise, non-redundant bullet list aligned to .claude/VISION.md, moving any existing list content to Contents-removed.md. No helper scripts are included or required.
---

# fill-subtopic

Use this skill when the user wants to populate one specific Subtopic in `Contents.md` with a compact list of content points.

## Required parameter

The user must identify exactly one Subtopic from `Contents.md` by one of these forms:

- Subtopic number, for example `03.03`.
- Subtopic title, for example `Control Plane`, if unique.
- Topic title plus Subtopic title, for example `Kubernetes Architecture / Control Plane`.
- Topic number plus Subtopic title, for example `03 / Control Plane`.

If the parameter does not identify exactly one Subtopic, stop and ask for a more precise Subtopic reference. Do not modify files on an ambiguous match.

## Input files

- `Contents.md`
- `.claude/VISION.md`
- Optional existing `Contents-removed.md`

## Output files

- Updated `Contents.md`
- Updated or created `Contents-removed.md`, but only when an existing list was moved out of the selected Subtopic

## File interpretation

### `Contents.md`

- Preserve YAML frontmatter as-is.
- Preserve existing topic order, subtopic order, numbering, links, lesson comments, separators, and unrelated content.
- Treat level-1 headings (`#`) as Topics.
- Treat level-2 headings (`##`) as Subtopics.
- Ignore markdown links when matching headings; compare visible link text.
- Ignore numbering prefixes when matching headings:
  - Topic numbers such as `01`.
  - Subtopic numbers such as `01.02`.
- The selected Subtopic block starts at its `##` heading and ends before the next `##` or `#` heading, or end of file.

### `.claude/VISION.md`

Use `.claude/VISION.md` as the content guardrail for all generated bullet points:

- Respect the stated audience, assumed prior knowledge, language, scope, non-goals, and workshop structure.
- Keep content in English.
- Prefer conceptual-first phrasing.
- Do not introduce cloud-provider-specific material.
- Do not introduce production/security deep dives unless the selected Subtopic belongs to the optional deep-dive/security area.
- Do not turn conceptual topics into implementation-heavy exercises unless the vision explicitly supports that depth.

## Existing list handling

A Subtopic has an existing list when, after the Subtopic heading and generated lesson comment, the Subtopic body contains a top-level markdown list.

Before inserting the new list:

1. Move the existing top-level list from the selected Subtopic to `Contents-removed.md`.
2. Preserve the moved list exactly, including existing numbering, links, comments, nested list items, and blank lines that belong to it.
3. Append the moved list under a clear removal heading:

```markdown
-------------------------------------------------------------------------------

# Removed Subtopic Points

## <topic title>

### <subtopic title>

Moved from `Contents.md` by `fill-subtopic`.

<old list>
```

4. If `Contents-removed.md` already exists, append a new removal block; do not overwrite previous removals.
5. Remove the old list from the selected Subtopic in `Contents.md` before writing the new one.
6. Preserve non-list prose in the Subtopic unless it is clearly part of the old list. Insert the new list after the Subtopic heading and lesson comment, before any preserved non-list prose.

## Generated list requirements

Generate one top-level markdown bullet list in the selected Subtopic.

The list must satisfy all of these constraints:

- Minimum 4 entries.
- Maximum 8 entries.
- Each entry is a concise bullet point, not a paragraph.
- Each entry fits the selected Subtopic.
- The set of entries covers the Subtopic adequately for workshop contents planning.
- Entries are mutually non-redundant.
- Entries do not duplicate bullet points or obvious point coverage already present in other Subtopics.
- Entries require no explanations that belong only to later Topics.
- Entries stay consistent with `.claude/VISION.md`.
- Entries are written in English.
- Entries should be specific enough to guide later lesson writing, but not so detailed that they become full lesson prose.

## Cross-subtopic redundancy check

Before writing the new list:

1. Read all existing bullet points in other Subtopics of `Contents.md`.
2. Normalize them for comparison by:
   - Removing numbering prefixes.
   - Removing markdown links while keeping visible text.
   - Removing generated HTML comments.
   - Collapsing whitespace.
3. Avoid creating bullets with the same meaning as bullets already present elsewhere.
4. If the selected Subtopic is closely related to another Subtopic, keep the boundary explicit.
   - Example: `Control Plane` should cover API Server, Scheduler, Controller Manager, and etcd at architecture level.
   - Example: `Worker Nodes` should cover kubelet, container runtime, Pods on nodes, and node-local responsibilities.
   - Example: `Services` should introduce stable access to Pods, while `Services & kube-proxy` can cover traffic routing mechanics and service types.

## Progression check

Use the order in `Contents.md` as the teaching progression:

- A bullet may rely on concepts introduced in earlier Topics/Subtopics.
- A bullet must not require detailed knowledge from later Topics/Subtopics.
- If a later concept must be mentioned for orientation, keep it as a short forward reference, not as a required explanation.

## Formatting rules

Preserve the selected Subtopic heading and its existing lesson comment exactly unless the file format already requires a minor blank-line normalization.

Insert the generated list directly below the Subtopic lesson comment:

```markdown
## [03.03 Control Plane](<Contents/03-Kubernetes Architecture/03.03-Control Plane.md>)
<!-- lesson: Contents/03-Kubernetes Architecture/03.03-Control Plane.md -->

- API Server as the central Kubernetes API entry point
- Scheduler assigning pending Pods to suitable Worker Nodes
- Controller Manager reconciling desired and actual cluster state
- etcd as the persistent store for cluster state
```

Do not add point-level lesson or anchor comments. This skill creates plain bullet lists only.

Do not renumber Topics, Subtopics, or Points. Numbering and link maintenance belongs to `build-contents`, not to `fill-subtopic`.

## Selection algorithm

When resolving the required Subtopic parameter:

1. Parse all Topics and Subtopics from `Contents.md`.
2. For each Topic/Subtopic, record:
   - Raw heading.
   - Visible title without markdown link syntax.
   - Numbering prefix, if present.
   - Normalized title without numbering.
   - Parent Topic title and number.
3. Match the user parameter against:
   - Exact Subtopic number.
   - Exact normalized Subtopic title.
   - Exact normalized `Topic / Subtopic` pair.
   - Exact `Topic number / Subtopic title` pair.
4. Prefer exact matches over fuzzy matches.
5. Use fuzzy matching only to suggest candidates, not to modify files.

## Quality gate before finalizing

Before saving the final `Contents.md`, verify:

- Exactly one Subtopic was modified.
- `Contents-removed.md` was changed only if an existing list was moved.
- The new list has 4 to 8 entries.
- The new list is under the selected Subtopic only.
- No generated bullet is a duplicate of another generated bullet.
- No generated bullet is a clear duplicate of a bullet in another Subtopic.
- The generated bullets do not violate `.claude/VISION.md` scope or non-goals.
- Topic/Subtopic numbering and links were not rebuilt by this skill.

## Response after execution

After editing, report briefly:

- Which Subtopic was filled.
- How many bullet points were generated.
- Whether an old list was moved to `Contents-removed.md`.
- Any uncertainty or skipped change, if applicable.

