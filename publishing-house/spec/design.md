# Ansible Edge Automation Lab

## Problem Statement

Infrastructure engineers managing remote edge fleets — retail kiosks, industrial IoT gateways, or distributed RHEL devices — face a scalability wall when individual SSH access is impractical or impossible. Manual configuration and patching workflows that work for a handful of servers break at hundreds of devices. Red Hat Ansible Automation Platform 2.6 provides centralized fleet orchestration and event-driven remediation, but most Ansible practitioners have only applied these tools in traditional data center scenarios. This lab closes the gap by teaching the full device lifecycle management pattern in an edge context using AAP, Event-Driven Ansible, and RHEL for Edge.

## Target Audience

- **Role:** Sysadmins and infrastructure engineers
- **Experience level:** Intermediate
- **What they already know:** Basic Ansible (writing playbooks, managing inventory, running ad-hoc commands); familiarity with RHEL administration
- **What they don't know:** Using Ansible Automation Platform 2.6 for edge scenarios; Event-Driven Ansible for automated remediation; managing RHEL for Edge devices at scale through a central controller
- **Prerequisites:** Ansible Fundamentals or equivalent experience; basic RHEL/Linux administration

## Learning Objectives

1. Register remote edge devices with Ansible Automation Platform using dynamic inventory and device credentials
2. Deploy fleet-wide configuration changes to RHEL for Edge devices using AAP job templates and inventory groups
3. Execute rolling application updates across an edge device fleet using Ansible playbooks and AAP workflows
4. Detect and automatically remediate a security finding on edge devices using Event-Driven Ansible rulebooks

## Content Type

Lab (hands-on)

## Products & Technologies

- Red Hat Ansible Automation Platform 2.6
- Event-Driven Ansible
- Red Hat Enterprise Linux 9 (edge devices — simulated as VMs)
- Red Hat Ansible Automation Hub

## Module Map

| Module | Title | Duration |
|--------|-------|----------|
| 1 | Device Onboarding and Inventory Registration | ~20 min |
| 2 | Pushing Configuration to the Fleet | ~25 min |
| 3 | Deploying an Application Update | ~25 min |
| 4 | Detecting and Remediating a Security Finding | ~20 min |
| — | **Total hands-on** | **~90 min** |
| — | Intro / presentation | ~10 min |
| — | **Total lab** | **~100 min** |

## Difficulty Level

Intermediate

## Environment

**Learner view:** Students arrive with a fully deployed Ansible Automation Platform 2.6 environment: an AAP Controller and Automation Hub running on a dedicated RHEL 9 host, and 5 RHEL 9 VMs simulating remote edge kiosk devices. The edge VMs have a minimal base OS configuration — no applications installed, not yet registered with AAP. Students access the AAP Controller UI via browser. All interactions with edge devices go through AAP; students do not SSH directly into VMs. Automation Hub is pre-populated with the collections required for the lab exercises.

**Automation needed:** Yes
- AAP 2.6 Controller + Automation Hub deployment on a dedicated RHEL 9 host
- 5 RHEL 9 VMs per student provisioned via CNV, minimal base config (OS only)
- Automation Hub pre-seeded with required Ansible collections
- AAP initial stubs (organization, credential types) pre-created; device registration and job template configuration are completed by students in the lab

## Infrastructure Requirements

- **Base infrastructure:** cloud-vms-base — dedicated RHEL 9 host for AAP control plane + 5 CNV VMs per student for edge device simulation; CNV cluster running OCP 4.20+
- **Sizing:** TBD — estimating AAP host: 4 CPU, 16GB RAM, 100GB disk; edge VMs: 5 × (2 CPU, 4GB RAM, 20GB disk) per student; total scales with concurrent user count
- **Cloud provider:** CNV (default)
- **Automation approach:** Ansible
- **Existing workloads to reuse:** TBD — check AgnosticD for existing AAP 2.6 RHEL deployment roles
- **New workloads needed:** AAP 2.6 RHEL deployment workload (if not in AgnosticD); CNV-based edge VM provisioning with minimal RHEL 9 config
