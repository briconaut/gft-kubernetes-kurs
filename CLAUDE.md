---
revision: 0
path: "CLAUDE.md"
title: "CLAUDE.md"
abstract: "Guidance for the Claude Code agent that builds the GFT Kubernetes Workshop content and exercises in this repository."
state: in progress
lang: en
numbersections: true
current_phase: 4
finished_sections: [ ]
history: [ ]
---

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

You're an Kubernetes expert trainer und you build a workshop to train a technical-minded audience in the basics of using kubernetes.

## What this repository is

This is **not a software project** — it is the content source for a Kubernetes workshop for developers with no prior Kubernetes experience (GFT DevOps Community). There is no application code, no build system, no tests, and no linter. Work here consists of writing and refining course material.

`CLAUDE.md` is produced and maintained in a separate planning session (a Claude Project chat) and handed to the Claude Code agent working in this repository. Claude Code should treat this file — and the tasks it currently points to in `.claude/TASKS.md` — as the authoritative brief for what to produce next, not as something to redesign on its own initiative.

## Language

- Language of all files and content is English.
- Automatically translate to english if an other language was used.

## Audience of the workshop

- Technical persons (developers, DevOps/SysOps/SRE, testers).
- Basic Docker/container knowledge (CLI, images, Docker Swarm, Docker Compose).
- Keep explanations conceptual-first.

# Workshop description

## Workshop Scope

- **Structure**: two parts — a mandatory introduction (~4h) and an optional deep-dive (~4h: StatefulSet, RBAC, Storage, …).d
- **Focus**: concepts *within* Kubernetes (Pods, Deployments, Services, Config, …). Underlying infrastructure (nodes, networking, storage backends) is mentioned briefly, not taught in depth.
- **Prerequisites**: Docker/container basics (CLI, images). No prior Kubernetes knowledge assumed.
- **Target Kubernetes version**: whatever ships with Docker Desktop's built-in Kubernetes (currently kubeadm-based, single-node).
- **Exercise environment**: Kubernetes as bundled with Docker Desktop. No cloud cluster, no Rancher-specific features.
- **Artifact format**: Markdown for all content and exercise files. Details in `.claude/STYLES.md`

## Non-Goals

- No infrastructure/cluster-ops deep dive (networking internals, storage classes, cluster provisioning).
- No cloud-provider-specific content (EKS/GKE/AKS particulars) — content stays generic/portable.
- No CI/CD tool-specific implementation — CI/CD is covered conceptually only.
- No production-hardening / security deep-dive beyond what's covered in the optional deep-dive part.

# How to work with this repositoy

## Folder & File Conventions

- Topic list (which concepts are covered, no prose): `.claude/TOPICS.md` — used as a central control for the topics/subtopics of the workshop.
- Format specifications for generated content files: `.claude/STYLE.md`
- Workshop details (topics, subtopics and subjects ) `Contents.md` — exact structure and formatting rules in `.claude/STYLE.md` → Format of Contents.md.
- Exercise list (which exercises are covered, no prose): `Practices.md`
- Actual lesson content: `Contents/<#topic>-<topic title>/<#subtopic>-<subtopic title>.lesson.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Lesson File Format.
- Exercises: `Contents/<#topic>-<topic title>/<#subtopic>-<subtopic title>.practice.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Practice File Format.
- Solutions: `Contents/<#topic>-<topic title>/<#subtopic>-<subtopic title>.solution.md`
  - See `.claude/STYLE.md` for `<#topic>`, `<topic title>`, `<#subtopic>` and `<subtopic title>`.
  - Body structure of these files is fixed and built in two stages — see `.claude/STYLE.md` → Solution File Format.
- Module-scoped memory: `Contents/<nr>-<section>/Memory.md` (see Memory Structure below)
- Project-wide memory: `.claude/Memory.md` (see Memory Structure below)
- `README.md` is **out of scope**.

## Styleguide

File-format specifications for generated artifacts — the frontmatter header, the lesson-file structure, and the format of `Contents.md` — are documented in `.claude/STYLE.md`. Consult it before producing or editing any of those file types. This section covers only the two harness-process file formats that aren't generated *content* artifacts: the task backlog and the Memory files.

# Task handling

# Memory Structure (`Memory.md`)

Purpose: give the agent the minimal context needed to work a task **consistently with previously completed tasks** — not a full history or diary. Only what would otherwise be lost or ambiguous belongs here; everything already visible in the produced file itself, in `CLAUDE.md`, or in `.claude/STYLE.md` does not.

Two levels:
- **Global** — `.claude/Memory.md`: cross-cutting decisions/conventions relevant across the whole project (e.g. the module numbering scheme, terminology choices, how Practices.md topics were mapped to Contents.md modules). Read before, and updated after, tasks that span multiple modules or files (mainly Phase 1 and Phase 6, plus Phase 3/5/7 planning).
- **Per module** — `Contents/<nr>-<section>/Memory.md`: context scoped to one module (learning objectives already fixed, terminology used in that module, prerequisites established, deviations from the module template). Read before, and updated after, tasks scoped to a single module (mainly Phase 2, Phase 4, and Phase 8). Created the first time a task touches that module.

Rules:
- Before starting a task, the agent reads `.claude/Memory.md`, plus the module's `Memory.md` if the task is module-scoped.
- After finishing or blocking a task, the agent appends at most a few bullet points — only genuinely new, load-bearing context.
- `Memory.md` files hold *current* state, not an append-only diff log — if a fact becomes obsolete, replace it rather than leaving contradictory entries.
- Blocker entries include: what's blocking, why, what's needed to unblock.
