---
name: enumerate
description: Verify Contents.md is in sync with .claude/TOPICS.md at Topic/Subtopic level, then perform a full renumbering of every Topic, Subtopic, and Subject in Contents.md (filling in any missing numbers), rewrite all links and generated HTML comments (lesson:/anchor:) to match, and move/rename the corresponding .lesson.md/.practice.md/.solution.md files on disk to their new numbered paths. Aborts without changes if Contents.md and .claude/TOPICS.md are out of sync.
---

# enumerate

Use this skill when Contents.md's numbering needs to be (re-)established — after Topics/Subtopics were added, removed, or reordered by `/build-contents`, after manual edits to `Contents.md`, or whenever numbering, links, or file names might have drifted out of sync with each other.

This is the single authority for numbering, links, generated comments, and on-disk file paths in `Contents/`. `/build-contents` and `/fill-subtopic` deliberately do not renumber or rename anything themselves — that is always this skill's job, run afterward.

## Terminology and formatting

Use "Topic", "Subtopic", and "Subject" exactly as defined in `.claude/STYLE.md` → Numbering. All numbering formats, link formats, file-path formats, and the `lesson:`/`anchor:` HTML comment conventions are taken directly from `.claude/STYLE.md` → Numbering and → Format of Contents.md — not restated here. Re-read `.claude/STYLE.md` before formatting any output; if this skill's instructions and `.claude/STYLE.md` ever appear to disagree, `.claude/STYLE.md` wins.

## Input files

- `Contents.md`
- `.claude/TOPICS.md`
- `.claude/STYLE.md`
- The actual `Contents/<#topic>-<topic title>/` folders and their `.lesson.md` / `.practice.md` / `.solution.md` files, plus any per-module `Memory.md` inside them

## Step 1 — Sync check against `.claude/TOPICS.md` (abort gate)

- Read only `.claude/TOPICS.md` → `# Topics` (same scope `/build-contents` uses; `# Exercises`, `# Excluded`, `# New` are not considered).
- Compare its Topic/Subtopic titles against `Contents.md`'s actual Topic/Subtopic headings, using the same normalization rules as `/build-contents` (strip numbering prefixes, strip markdown links, collapse whitespace, case-sensitive compare).
- **Synced** means: the same set of Topic titles, and for each Topic the same set of Subtopic titles, appear in both files — ignoring order.
- **If not synced**: stop immediately. Do not renumber, rewrite links, or move any file. Report exactly which Topics/Subtopics are missing from which file, and point the user to `/build-contents` to reconcile first.
- **If synced**: proceed to Step 2.

## Step 2 — Determine the new numbering

- Use `Contents.md`'s current top-to-bottom order as authoritative — this skill does not reorder Topics, Subtopics, or Subjects, only (re-)numbers them in place.
- Assign Topic numbers `01`, `02`, ... in the order Topics currently appear.
- Within each Topic, assign Subtopic numbers `<#topic>.01`, `<#topic>.02`, ... in the order Subtopics currently appear.
- Within each Subtopic that has a Subject list (per `.claude/STYLE.md`'s definition of a Subject-bearing Subtopic), assign Subject numbers `<#topic>.<#subtopic>.01`, `<#topic>.<#subtopic>.02`, ... in the order Subjects currently appear.
- This is a full rebuild every run, not an incremental patch: every Topic/Subtopic/Subject gets (re-)assigned a number this way, whether it previously had a correct number, a wrong number, or no number at all — this is how missing numbering gets filled in.
- For every Topic and Subtopic, compute old path vs. new path (folder and/or file names) per `.claude/STYLE.md` → Format of Contents.md. No path changes result from Subject renumbering alone, since Subjects are anchors within their Subtopic's file, not separate files.

## Step 3 — Present the plan and ask for confirmation

Before changing anything, present:

- A diff-style summary of every Topic/Subtopic/Subject whose number changed or was newly assigned.
- The resulting list of file/folder moves (Step 4 below), including which of `.lesson.md`/`.practice.md`/`.solution.md` exist and will move for each affected Subtopic.
- Ask the user to confirm before proceeding. On rejection, stop — nothing is written.

## Step 4 — Move/rename files on disk

Only for Topics/Subtopics whose number and/or title changed:

- **Topic-level**: if a Topic's number or title changed, `git mv` the whole folder `Contents/<old #>-<old title>/` → `Contents/<new #>-<new title>/` in one step. This also moves every Subtopic file inside it, and the per-module `Memory.md` if present — do not additionally move files already relocated by the folder move.
- **Subtopic-level**: if only a Subtopic's number or title changed (its parent Topic's folder unchanged), individually `git mv` that Subtopic's `.lesson.md`, `.practice.md`, and `.solution.md` — whichever exist — to their new file names within the (possibly already-renamed) Topic folder.
- If a file referenced by `Contents.md` doesn't exist on disk yet (content not authored yet), skip the move for it — only update `Contents.md`'s own link/comment for that entry.
- If a computed new path is currently occupied by another file that will itself move in this same run, stage the moves via temporary intermediate names to avoid collisions or overwrites.
- After moving a per-module `Memory.md`, update its own frontmatter `path:` field to the new location, per `.claude/STYLE.md` → Frontmatter.
- Prefer `git mv` to preserve file history; fall back to a plain move only if the file isn't tracked by git.

## Step 5 — Rewrite `Contents.md`

- Update every Topic/Subtopic heading, every Subject list item, every markdown link, and every `lesson:`/`anchor:` HTML comment to the new numbering and new paths, exactly per `.claude/STYLE.md` → Format of Contents.md.
- Preserve all non-generated content (Subject prose, unrelated sections, separators) unchanged.
- Bump `revision`/`history` in `Contents.md`'s frontmatter per `.claude/STYLE.md` → Frontmatter, summarizing the renumbering in one line.

## Out of scope

- Does not modify `.claude/TOPICS.md` — read-only dependency, used only for the Step 1 sync check.
- Does not add or remove Topics/Subtopics — that's `/build-contents`.
- Does not generate, edit, or reorder Subject content — that's `/fill-subtopic`.
- Does not rewrite links inside the body/prose of `.lesson.md` / `.practice.md` / `.solution.md` files — only their own file/folder paths and `Contents.md`'s references to them.
- Does not touch `Contents-removed.md`.
- Does not touch `Practices.md` — its format isn't yet defined in `.claude/STYLE.md`.

## Response after execution

After completing, report briefly:

- How many Topics/Subtopics/Subjects were renumbered vs. newly numbered.
- Which folders/files were moved.
- Confirmation that `Contents.md`'s links and comments now match.
