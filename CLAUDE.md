---
revision: 1
path: "CLAUDE.md"
title: "CLAUDE.md"
abstract: "Guidance for the Claude Code agent that builds the GFT Kubernetes Workshop content and exercises in this repository."
state: in progress
lang: en
numbersections: true
history: 
  - "v1: initial version"
---

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

You're an Kubernetes expert trainer und you build a workshop to train a technical-minded audience in the basics of using kubernetes.

## Agent Behavior

- Work directly in the checked-out project directory — do not create additional git worktrees.

## What this repository is

This is **not a software project** — it is the content source for a Kubernetes workshop for developers with no prior Kubernetes experience (GFT DevOps Community). There is no application code, no build system, no tests, and no linter. Work here consists of writing and refining course material.

`CLAUDE.md` is produced and maintained in a separate planning session (a Claude Project chat) and handed to the Claude Code agent working in this repository. Claude Code should treat this file as the authoritative brief for what to produce next, not as something to redesign on its own initiative.

## Language

- Language of all files and content is English.
- Automatically translate to english if an other language was used.

## Audience of the workshop

- Technical persons (developers, DevOps/SysOps/SRE, testers).
- Basic Docker/container knowledge (CLI, images, Docker Swarm, Docker Compose).
- Keep explanations conceptual-first.

# Workshop description

## Workshop Scope

- **Structure**: two parts — a mandatory introduction (~4h) and an optional deep-dive (~4h: StatefulSet, RBAC, Storage, …).
- **Focus**: concepts *within* Kubernetes (Pods, Deployments, Services, Config, …). Underlying infrastructure (nodes, networking, storage backends) is mentioned briefly, not taught in depth.
- **Prerequisites**: Docker/container basics (CLI, images, Docker Swarm, Docker Compose) and basic shell (bash) knowledge. No prior Kubernetes knowledge assumed.
- **Target Kubernetes version**: whatever ships with Docker/Rancher Desktop's built-in Kubernetes (currently kubeadm-based, single-node).
- **Exercise environment**: Kubernetes as bundled with Docker/Rancher Desktop. No cloud cluster, no Rancher-exclusive features.
- **Artifact format**: Markdown for all content and exercise files. Details in `.claude/STYLE.md`

## Non-Goals

- No infrastructure/cluster-ops deep dive (networking internals, storage classes, cluster provisioning).
- No cloud-provider-specific content (EKS/GKE/AKS particulars) — content stays generic/portable.
- No CI/CD tool-specific implementation — CI/CD is covered conceptually only.
- No production-hardening / security deep-dive beyond what's covered in the optional deep-dive part.

# How to work with this repository

## Folder & File Conventions

- Intent, audience and guardrails in `.claude/VISION.md` for the overarching structure of all components.
- Topic list (which concepts are covered, no prose): `.claude/TOPICS.md` — used as a central control for the topics/subtopics of the workshop.
- Format specifications for generated content files: `.claude/STYLE.md`
- Workshop details (topics, subtopics and subjects ) `Contents.md` — exact structure and formatting rules in `.claude/STYLE.md` → Format of Contents.md.
- Exercise list (which exercises are covered, no prose): `Practices.md`
- Actual lesson content: `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.lesson.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Lesson File Format.
- Exercises: `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.practice.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Practice File Format.
- Solutions: `Contents/<#topic>-<topic title>/<#topic>.<#subtopic>-<subtopic title>.solution.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Solution File Format.
- Topic-scoped memory: `Contents/<#topic>-<topic title>/Memory.md` (see Memory Structure below)
- Project-wide memory: `.claude/Memory.md` (see Memory Structure below)
- `README.md` is **out of scope**.

Only when the user's current prompt explicitly requests **Next task** or **Next subtopic**, then these files are relevant:

- Slide-generation tasks: `.claude/TASKS.md`
- Task execution process: `.claude/TASK-EXECUTION.md`
- Task-file format: `.claude/STYLE-TASKS.md`


## Styleguide

File-format specifications for generated artifacts — the frontmatter header, the lesson-file structure, and the format of `Contents.md` — are documented in `.claude/STYLE.md`. Consult it before producing or editing any of those file types. 

# Memory Structure (`Memory.md`)

Purpose: give the agent the minimal context needed to work a task **consistently with previously completed tasks** — not a full history or diary. Only what would otherwise be lost or ambiguous belongs here; everything already visible in the produced file itself, in `CLAUDE.md`, or in `.claude/STYLE.md` does not.

Two levels:
- **Global** — `.claude/Memory.md`: cross-cutting decisions/conventions relevant across the whole project (e.g. the topic numbering scheme, terminology choices, how Practices.md topics were mapped to Contents.md topics). Read before, and updated after, tasks that span multiple topics or files.
- **Per topic** — `Contents/<#topic>-<topic title>/Memory.md`: context scoped to one topic (learning objectives already fixed, terminology used in that topic, prerequisites established, deviations from the topic template). Read before, and updated after, tasks scoped to a single topic. Created the first time a task touches that topic.

Rules:
- Before starting a task, the agent reads `.claude/Memory.md`, plus the topic's `Memory.md` if the task is topic-scoped.
- After finishing or blocking a task, the agent appends at most a few bullet points — only genuinely new, load-bearing context.
- Section `# Project Memory` in `Memory.md` files hold *current* state, not an append-only diff log — if a fact becomes obsolete, replace it rather than leaving contradictory entries.
- Section `# Review Notes` in `Memory.md` is an append-only diff log — it will be exclusively maintained by certain skills.
- Blocker entries include: what's blocking, why, what's needed to unblock.

# Task Execution

Tasks are never executed implicitly.

Only when the user's current prompt explicitly requests **Next task** or **Next subtopic**:

1. Read `.claude/TASK-EXECUTION.md`.
2. Read `.claude/STYLE-TASKS.md`.
3. Read and validate `.claude/TASKS.md`.
4. Execute the requested mode according to `.claude/TASK-EXECUTION.md`.

Do not read `.claude/TASK-EXECUTION.md` or `.claude/STYLE-TASKS.md` during repository initialization or for requests unrelated to task execution.

Reading, displaying, or discussing `.claude/TASKS.md` does not authorize task execution.
