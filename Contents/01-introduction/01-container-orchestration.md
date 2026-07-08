---
revision: 10
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
  - "v5: added prose for '## Desired-state reconciliation' per Task 4.2"
  - "v6: reviewed the manual edit to '## Desired-state reconciliation' via /review — removed the redundant second sentence of the control-loop paragraph, which restated the first sentence and preempted the upcoming 'Self-healing' bullet's content; kept the new 'declarative approach' opening sentence"
  - "v7: added prose for '## Self-healing / auto-restart of failed containers' per Task 4.3"
  - "v8: added prose for '## Horizontal & vertical scaling' per Task 4.4"
  - "v9: added prose for '## Rolling updates without downtime' per Task 4.5"
  - "v10: added prose for '## Declarative configuration via manifests' per Task 4.6"
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

Kubernetes allows a declarative approach to defining its state. You tell Kubernetes the state you want — for example, "3 replicas of this container should be running" — instead of the individual steps to get there.

A background control loop continuously compares this desired state against the cluster's actual state and implements the necessary changes.

This is different from a plain `docker run` or `docker compose up`, which execute once and then stop watching. If a container dies afterwards, nothing brings it back automatically — you'd have to notice and restart it yourself.

## Self-healing / auto-restart of failed containers

If a container crashes, or the node it runs on becomes unreachable, Kubernetes notices and replaces it automatically — the same reconciliation loop from the previous section keeps doing its job.

With plain Docker, a crashed container only comes back if you explicitly configured a restart policy (--restart=always), and even then only on the same host. Kubernetes continuously enforces the desired state cluster-wide by default, including rescheduling onto a different node if the original one fails.

## Horizontal & vertical scaling

Kubernetes can adjust capacity in two ways: **horizontally**, by running more (or fewer) copies of the same container, and **vertically**, by giving each container more or less CPU/memory. Horizontal scaling is the more common approach in Kubernetes and is covered in more depth later.

With plain Docker, scaling out means manually starting more containers yourself. Kubernetes instead treats the replica count as part of the same declarative desired state described above — you change one number, and the reconciliation loop does the rest.

## Rolling updates without downtime

When you deploy a new version of your container image, Kubernetes replaces the old Pods with new ones gradually — a few at a time — instead of stopping everything at once. Enough of the old version keeps running until enough of the new version is up, so the application stays reachable throughout the update.

This is different from replacing a single `docker run` container, where stopping the old one before starting the new one causes a brief gap. The mechanics of rollouts and rollbacks are covered in more depth later.

## Declarative configuration via manifests

The desired state described above isn't just a mental model — you write it down as YAML (or JSON) **manifest** files, one per resource (a Deployment, a Service, and so on), and hand them to Kubernetes with `kubectl apply -f`. These files are the source of truth for what should exist in the cluster, and since they're plain text, you can check them into version control alongside your application code.

This replaces a sequence of imperative `docker run` commands with a description of the end result. Reapplying the same file is safe to repeat — Kubernetes only changes what's actually different from the current state.

## Resource requests & limits (brief mention)

_Content pending (Phase 4)._
