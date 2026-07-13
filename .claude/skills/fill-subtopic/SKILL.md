---
name: fill-subtopic
description: Fill exactly one selected Subtopic in Contents.md with a concise, non-redundant bullet list of Subjects aligned to .claude/VISION.md, moving any existing Subject list to Contents-removed.md. Produces plain bullet content only — numbering, links, and comments are rebuilt later by /build-contents per .claude/STYLE.md. No helper scripts are included or required.
---

# fill-subtopic

Use this skill when the user wants to populate one specific Subtopic in `Contents.md` with a compact list of Subjects.

This skill only edits `Contents.md` (and, when replacing an existing list, `Contents-removed.md`). It never creates, renames, or edits `.lesson.md` / `.practice.md` / `.solution.md` content files — those are out of scope, to avoid any conflict with `.claude/STYLE.md`'s file-format specifications for those files.

## Terminology

Use "Topic", "Subtopic", and "Subject" exactly as defined in `.claude/STYLE.md` → Numbering (Level-1 heading = Topic, Level-2 heading = Subtopic, bullet point under a Subtopic = Subject).

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
- `.claude/STYLE.md` — authoritative for Topic/Subtopic/Subject naming and numbering; consult it whenever this skill needs to recognize or match existing structure.
- Optional existing `Contents-removed.md`

## Output files

- Updated `Contents.md`
- Updated or created `Contents-removed.md`, but only when an existing Subject list was moved out of the selected Subtopic

## File interpretation

### `Contents.md`

- Preserve YAML frontmatter as-is.
- Preserve existing Topic order, Subtopic order, numbering, links, comments, separators, and unrelated content.
- Identify Topics, Subtopics, and Subjects per `.claude/STYLE.md` → Numbering.
- Ignore markdown links when matching headings; compare visible link text.
- Ignore numbering prefixes when matching headings or Subjects.
- The selected Subtopic block starts at its `##` heading and ends before the next `##` or `#` heading, or end of file.

### `.claude/VISION.md`

Use `.claude/VISION.md` as the content guardrail for all generated Subjects:

- Respect the stated audience, assumed prior knowledge, language, scope, non-goals, and workshop structure.
- Keep content in English.
- Prefer conceptual-first phrasing.
- Do not introduce cloud-provider-specific material.
- Do not introduce production/security deep dives unless the selected Subtopic belongs to the optional deep-dive/security area.
- Do not turn conceptual topics into implementation-heavy exercises unless the vision explicitly supports that depth.

## Existing list handling

A Subtopic has an existing list when, after the Subtopic heading (and any existing generated comment), the Subtopic body contains a top-level markdown list of Subjects.

Before inserting the new list:

1. Move the existing top-level list of Subjects from the selected Subtopic to `Contents-removed.md`.
2. Preserve the moved Subjects exactly, including existing numbering, links, comments, nested list items, and blank lines that belong to them.
3. Append the moved Subjects under a clear removal heading:

```markdown
-------------------------------------------------------------------------------

# Removed Subjects

## <topic title>

### <subtopic title>

Moved from `Contents.md` by `fill-subtopic`.

<old Subject list>
```

4. If `Contents-removed.md` already exists, append a new removal block; do not overwrite previous removals.
5. Remove the old Subject list from the selected Subtopic in `Contents.md` before writing the new one.
6. Preserve non-list prose in the Subtopic unless it is clearly part of the old list. Insert the new Subject list after the Subtopic heading (and any existing comment), before any preserved non-list prose.

## Generated list requirements

Generate one top-level markdown bullet list of Subjects in the selected Subtopic.

The list must satisfy all of these constraints:

- Minimum 4 entries.
- Maximum 8 entries.
- Each Subject is a concise bullet point, not a paragraph.
- Each Subject fits the selected Subtopic.
- The set of Subjects covers the Subtopic adequately for workshop contents planning.
- Subjects are mutually non-redundant.
- Subjects do not duplicate bullet points or obvious coverage already present in other Subtopics.
- Subjects require no explanations that belong only to later Topics.
- Subjects stay consistent with `.claude/VISION.md`.
- Subjects are written in English.
- Subjects should be specific enough to guide later lesson writing, but not so detailed that they become full lesson prose.

## Cross-subtopic redundancy check

Before writing the new list:

1. Read all existing Subjects in other Subtopics of `Contents.md`.
2. Normalize them for comparison by:
   - Removing numbering prefixes.
   - Removing markdown links while keeping visible text.
   - Removing generated HTML comments.
   - Collapsing whitespace.
3. Avoid creating Subjects with the same meaning as Subjects already present elsewhere.
4. If the selected Subtopic is closely related to another Subtopic, keep the boundary explicit.
   - Example: `Control Plane` should cover API Server, Scheduler, Controller Manager, and etcd at architecture level.
   - Example: `Worker Nodes` should cover kubelet, container runtime, Pods on nodes, and node-local responsibilities.
   - Example: `Services` should introduce stable access to Pods, while `Services & kube-proxy` can cover traffic routing mechanics and service types.

## Progression check

Use the order in `Contents.md` as the teaching progression:

- A Subject may rely on concepts introduced in earlier Topics/Subtopics.
- A Subject must not require detailed knowledge from later Topics/Subtopics.
- If a later concept must be mentioned for orientation, keep it as a short forward reference, not as a required explanation.

## Formatting rules

Preserve the selected Subtopic heading and any existing generated comment exactly unless the file format already requires a minor blank-line normalization.

Insert the generated list directly below the Subtopic heading (and its comment, if any):

```markdown
## [03.03 Control Plane](<...>)
<!-- lesson: ... -->

- API Server as the central Kubernetes API entry point
- Scheduler assigning pending Pods to suitable Worker Nodes
- Controller Manager reconciling desired and actual cluster state
- etcd as the persistent store for cluster state
```

This skill creates plain, unlinked, unnumbered Subject bullets only — no per-Subject links or comments. Numbering, links, and any generated comments for Subjects are rebuilt later by `/build-contents`, per `.claude/STYLE.md`.

Do not renumber Topics, Subtopics, or Subjects. Numbering and link maintenance belongs to `/build-contents`, not to `/fill-subtopic`.

## Document versioning

After all changes are done, increase the revision number in the header.
Add a one-line descriptive message to the history.

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
- `Contents-removed.md` was changed only if an existing Subject list was moved.
- The new list has 4 to 8 Subjects.
- The new list is under the selected Subtopic only.
- No generated Subject is a duplicate of another generated Subject.
- No generated Subject is a clear duplicate of a Subject in another Subtopic.
- The generated Subjects do not violate `.claude/VISION.md` scope or non-goals.
- Topic/Subtopic numbering and links were not rebuilt by this skill.

## Out of scope

- Does not create, rename, or edit `.lesson.md`, `.practice.md`, or `.solution.md` files.
- Does not renumber or relink Topics/Subtopics/Subjects — that's `/build-contents`.

## Response after execution

After editing, report briefly:

- Which Subtopic was filled.
- How many Subjects were generated.
- Whether an old Subject list was moved to `Contents-removed.md`.
- Any uncertainty or skipped change, if applicable.
