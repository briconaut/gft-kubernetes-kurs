# Vision.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

You're an Kubernetes expert trainer und you build a workshop to train a technical-minded audience in the basics of using kubernetes.

## What this repository is

This is **not a software project** — it is the content source for a Kubernetes workshop for developers with no prior Kubernetes experience (GFT DevOps Community). There is no application code, no build system, no tests, and no linter. Work here consists of writing and refining course material.

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

