---
revision: 4
path: "Contents/01-introduction/01-container-orchestration.md"
title: "What is Kubernetes and Why Should I Care? / What is container orchestration?"
abstract: "Lesson skeleton for this topic; explanatory prose pending Phase 4."
state: not started
lang: en
numbersections: true
finished_sections: [ ]
history:
  - "v1: created skeleton (H1, Overview links, placeholder bullet headings) per Task 2.2"
  - "v2: added prose for '## Automated scheduling & placement' per Task 4.1"
  - "v3: manually improved 4.1"
  - "v4: reviewed the manual edit via /review — fixed 'Kubernetes' capitalization and 'distribution strategies' wording, corrected the labels/selectors reference to node selectors/affinity, and added paragraph breaks between the three sentences; kept the Docker Swarm mention as accepted by the user"
---

# What is Kubernetes and Why Should I Care? / What is container orchestration?

## Overview

- [Automated scheduling & placement](#automated-scheduling-placement)
- [Desired-state reconciliation](#desired-state-reconciliation)
- [Self-healing / auto-restart of failed containers](#self-healing-auto-restart-of-failed-containers)
- [Horizontal & vertical scaling](#horizontal-vertical-scaling)
- [Rolling updates without downtime](#rolling-updates-without-downtime)
- [Declarative configuration via manifests](#declarative-configuration-via-manifests)
- [Resource requests & limits (brief mention)](#resource-requests-limits-brief-mention)

## Automated scheduling & placement

In a multi-host Kubernetes cluster, Kubernetes uses several distribution strategies to place your container. These can be influenced by node selectors and affinity rules (briefly covered later), so containers can be placed on hosts that offer specific features. With plain Docker, you pick the host yourself — you run `docker run` on a specific machine, or `docker compose up` on the one machine Compose knows about. In a Kubernetes cluster, you instead describe what you want to run and how much CPU/memory it needs, and the **scheduler** picks a suitable node for it automatically, based on which nodes currently have enough free capacity.

In case a node fails or a new one joins the cluster, that placement decision is made again automatically.

Docker swarm offers a similar feature, although greatly reduced in scope.

## Desired-state reconciliation

_Content pending (Phase 4)._

## Self-healing / auto-restart of failed containers

_Content pending (Phase 4)._

## Horizontal & vertical scaling

_Content pending (Phase 4)._

## Rolling updates without downtime

_Content pending (Phase 4)._

## Declarative configuration via manifests

_Content pending (Phase 4)._

## Resource requests & limits (brief mention)

_Content pending (Phase 4)._
