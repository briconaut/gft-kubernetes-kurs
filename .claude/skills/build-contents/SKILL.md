  ---
name: build-contents
description: Synchronize a Kubernetes course Contents.md with .claude/TOPICS.md, preserving existing content where possible, moving removed content to Contents-removed.md, and rebuilding numbering, lesson comments, point anchors, and markdown links.
---

# build-contents

Use this skill when the user wants `Contents.md` rebuilt from `.claude/TOPICS.md` while preserving existing lesson structure and moving obsolete content out of the active contents file.

## Inputs

- `.claude/TOPICS.md`
- `Contents.md`
- Optional existing `Contents-removed.md`

## Output files

- Updated `Contents.md`
- Appended/updated `Contents-removed.md` containing topics/subtopics that exist in `Contents.md` but no longer exist in `.claude/TOPICS.md`

## Source interpretation

### `.claude/TOPICS.md`

- Read only the section below the level-1 heading `# Topics`.
- Inside that section:
  - Level-2 headings (`##`) are canonical Topics.
  - Level-3 headings (`###`) are canonical Subtopics.
- Ignore all other heading levels and all body content.
- Ignore numbering prefixes in headings.
- Ignore markdown links in headings; compare only the visible link text.

### `Contents.md`

- Preserve YAML frontmatter as-is.
- Treat level-1 headings (`#`) as Topics.
- Treat level-2 headings (`##`) as Subtopics.
- Ignore numbering prefixes when comparing headings.
- Ignore markdown links in headings; compare only the visible link text.
- Preserve existing content under kept Subtopics except for generated numbering, generated comments, and generated point links/comments.

### Points

- A Point exists only when a Subtopic body consists exclusively of a top-level markdown list, ignoring blank lines and generated HTML comments.
- Each top-level list item is one Point.
- Ignore numbering prefixes and markdown links when comparing or renumbering Point titles.
- For Points, use `anchor` comments. If an existing generated Point comment uses `lesson`, update it to `anchor`.

## Reconciliation rules

1. Compare Topics and Subtopics by normalized title:
   - Remove existing numbering prefixes such as `01`, `01.02`, `01.02.03`.
   - Replace markdown links with their visible text.
   - Collapse internal whitespace.
   - Compare case-sensitively after normalization unless the user explicitly requests case-insensitive matching.
2. The canonical Topic/Subtopic order comes from `.claude/TOPICS.md`.
3. A Topic/Subtopic present in `.claude/TOPICS.md` but missing in `Contents.md` is inserted into `Contents.md` at the canonical position.
4. A Topic/Subtopic present in both files keeps its existing body content.
5. A Topic/Subtopic present in `Contents.md` but missing in `.claude/TOPICS.md` is removed from `Contents.md` and appended to `Contents-removed.md`, including its full original content.
6. If a whole Topic is removed, move the full Topic block including all Subtopics and content.
7. If only individual Subtopics are removed from a kept Topic, move those Subtopic blocks under a heading for the parent Topic in `Contents-removed.md`.

## Numbering and generated paths

Rebuild numbering after reconciliation:

- Topics: `01`, `02`, `03`, ...
- Subtopics: `01.01`, `01.02`, ... inside each Topic
- Points: `01.01.01`, `01.01.02`, ... inside each Subtopic

For generated lesson/anchor paths use this shape:

```text
Contents/<topic-nr>-<topic-title>/<subtopic-nr>-<subtopic-title>.md
Contents/<topic-nr>-<topic-title>/<subtopic-nr>-<subtopic-title>.md#<point-title>
```

Path title rules:

- Use normalized visible titles without numbering and without markdown links.
- Trim leading/trailing whitespace.
- Replace `/` with `-` to avoid unintended directories.
- Do not lowercase titles unless the user explicitly asks for slugified paths.

## Topic formatting

Each Topic heading in `Contents.md` must be rendered as:

```markdown
# 01 Topic Title
```

A separator line of 78 hyphens may be kept between Topics if already used by the file. Prefer preserving the existing separator style.

## Subtopic formatting

Each Subtopic heading in `Contents.md` must be rendered as a link:

```markdown
## [01.01 Subtopic Title](<Contents/01-Topic Title/01.01-Subtopic Title.md>)
<!-- lesson: Contents/01-Topic Title/01.01-Subtopic Title.md -->
```

Rules:

- If the lesson comment is missing, create it directly below the Subtopic heading.
- If the lesson comment already exists, update it directly below the Subtopic heading.
- Remove stale generated `lesson` comments immediately below the Subtopic heading before writing the new one.

## Point formatting

For list-only Subtopics, render each top-level list item as:

```markdown
- [01.01.01 Point Title](<Contents/01-Topic Title/01.01-Subtopic Title.md#Point Title>)
  <!-- anchor: Contents/01-Topic Title/01.01-Subtopic Title.md#Point Title -->
```

Rules:

- If the anchor comment is missing, create it directly below the Point list item.
- If an anchor or lesson comment already exists for the Point, update it to the canonical `anchor` comment.
- The Point title, not the Subtopic title, is linked to the anchor path.
- Preserve nested content only when it clearly belongs to the Point. Otherwise, leave non-list-only Subtopic bodies unchanged.

