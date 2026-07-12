---
revision: 2
path: "Contents/01-introduction/02-kubernetes-vs-docker.md"
title: "What is Kubernetes and Why Should I Care? / How is Kubernetes different from plain Docker?"
abstract: "Lesson content for this topic, contrasting plain Docker with Kubernetes across scheduling, self-healing, networking, and manifests."
state: in progress
lang: en
numbersections: true
finished_sections: [ ]
history:
  - "v1: created skeleton (H1, Overview links, placeholder bullet headings) per Task 2.2"
  - "v2: added prose for all 6 bullets per Tasks 4.9-4.14 — all placeholders filled, state moved to 'in progress' per .claude/STYLE.md"
---

# What is Kubernetes and Why Should I Care? / How is Kubernetes different from plain Docker?

## Overview

- [Single host vs. multi-node cluster](#single-host-vs-multi-node-cluster)
- [Manual `docker run`/`compose` vs. declarative manifests](#manual-docker-runcompose-vs-declarative-manifests)
- [No built-in scheduling in plain Docker](#no-built-in-scheduling-in-plain-docker)
- [No built-in self-healing in plain Docker](#no-built-in-self-healing-in-plain-docker)
- [No cross-host service discovery/networking in Docker Compose](#no-cross-host-service-discoverynetworking-in-docker-compose)
- [When plain Docker is still sufficient](#when-plain-docker-is-still-sufficient)

## Single host vs. multi-node cluster

Plain Docker runs everything on a single machine: the Docker daemon you talk to only ever knows about containers on that one host, and `docker compose up` starts all of a project's containers there too. A Kubernetes **cluster** is a group of machines (**nodes**) working together as one system, with containers — packaged as Pods — distributed across however many nodes are available.

Docker Desktop's built-in Kubernetes happens to run as a single-node cluster for local development, but the underlying model already assumes there could be many nodes to schedule onto. Cluster and node terminology is covered in depth in the next module.

## Manual `docker run`/`compose` vs. declarative manifests

With plain Docker, you tell the engine exactly what to do, step by step: `docker run` starts one container with the flags you give it, and a `docker-compose.yml` file lists the containers Compose should start with `docker compose up`. Either way you're describing *how* to start things, and running the same command twice can behave differently depending on what's already running.

Kubernetes manifests describe the state you want instead of the steps to get there — the same declarative approach covered in the previous lesson. `kubectl apply -f` is safe to rerun, since Kubernetes only changes what's actually different from the current state, rather than blindly starting new containers on top of existing ones.

## No built-in scheduling in plain Docker

Plain Docker has nothing to schedule: with a single Docker daemon there's only one machine to run on, and Docker Compose starts every service on that same machine too — there's no placement decision to make.

Kubernetes's scheduler, introduced in the previous lesson's "Automated scheduling & placement" section, exists specifically because a cluster gives it multiple nodes to choose from: it picks a suitable node for each Pod based on available CPU/memory and any placement rules. That's a capability plain Docker has no equivalent for, not a missing feature — a single-host tool has nothing to schedule between.

## No built-in self-healing in plain Docker

Docker can restart a crashed container on the same host if you explicitly set a restart policy (`--restart=always`, or `restart: always` in a Compose file) — but that's an opt-in, per-container setting, and it only ever restarts the container where it already was. If the host itself becomes unreachable, nothing brings the container back elsewhere.

Kubernetes enforces the desired state cluster-wide by default: the same reconciliation loop from the previous lesson notices a failed Pod or an unreachable node and replaces it, rescheduling onto a different node if needed, without any restart policy to configure.

## No cross-host service discovery/networking in Docker Compose

Docker Compose gives containers in the same project a shared network where they can reach each other by service name — but that network exists only on the single host Compose is running on. There's no built-in way for a container in one Compose project to discover or reach a container in another project on a different machine.

Kubernetes Services (covered in depth later) provide a stable virtual IP and DNS name that works across the whole cluster, regardless of which node a Pod actually lands on. Service discovery is a cluster-wide concept in Kubernetes, not something scoped to a single host's network.

## When plain Docker is still sufficient

None of the above makes plain Docker obsolete. For a single application running on one machine — a local development setup, a small internal tool, a single-server deployment with no real need for scaling or automatic failover — plain `docker run` or `docker compose` gets you running with far less setup and operational overhead than a cluster.

Kubernetes earns its complexity when you need several of the things covered in this module: scheduling across multiple machines, self-healing without manual intervention, or coordinated networking between many services. If a project doesn't need any of that, introducing a cluster is added complexity without a matching benefit.
