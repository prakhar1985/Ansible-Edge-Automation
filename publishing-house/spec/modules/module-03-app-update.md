# Module 3: Deploying an Application Update

## Brief Overview

Configuration management and application lifecycle management require different tooling within AAP.
Where a job template handles a single playbook run, an AAP workflow chains multiple job templates
into a coordinated sequence — enabling rolling update patterns that avoid taking the entire fleet
offline at once. This module builds on the registered fleet and the job template pattern from
Module 2 to execute a rolling application update across the five edge devices using an AAP
workflow. Students will observe the ordered progression of the update across the fleet.

## Audience and Time

- **Target personas:** Sysadmins and infrastructure engineers
- **Prerequisites:** Module 2 complete — inventory groups configured, at least one working job
  template, all five devices in a known base configuration state
- **Estimated duration:** ~25 min

## Learning Objectives

<!-- Maps to design spec objective 3:
     "Execute rolling application updates across an edge device fleet using Ansible playbooks
      and AAP workflows" -->

- Examine the application update playbook provided in Automation Hub to understand its role in
  the rolling update pattern
- Configure an AAP workflow that orchestrates the application update across the edge device fleet
- Launch the workflow and observe rolling update execution, verifying that each device completes
  the update before the next batch begins

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Reviewing the Update Playbook | ~5 min |
| 2 | Building the AAP Workflow | ~12 min |
| 3 | Launching and Observing the Rolling Update | ~8 min |

## Detailed Steps

### Section 1: Reviewing the Update Playbook

1. In the AAP Controller UI, navigate to **Projects** or the relevant Automation Hub content
   and locate the application update playbook provided for this module.
2. Review the playbook's stated purpose and the variables it accepts, as documented in the
   lab instructions.
3. Note any rolling update controls the playbook exposes (for example, batch size or serial
   execution settings) — these will inform how the workflow is constructed.
4. Identify the credential and inventory requirements for the update playbook before building
   the job template.

### Section 2: Building the AAP Workflow

5. Navigate to **Templates** and click **Add > Add workflow template**.
6. Name the workflow template to reflect its purpose (application update).
7. Assign the workflow to the pre-created organization and the inventory from Module 1.
8. Open the **Workflow Visualizer** to begin building the workflow graph.
9. Add the first node: create or reference a job template that runs the application update
   playbook against an initial subset of the fleet (rolling batch).
10. Configure the job template node with the device credential from Module 1 and the appropriate
    inventory group or host limit.
11. Add subsequent nodes in the workflow visualizer to represent the remaining device batches,
    chaining them on success from the previous node.
12. Review the completed workflow graph — confirm nodes are connected in the intended order
    and that each node targets the right hosts.
13. Save the workflow template.

### Section 3: Launching and Observing the Rolling Update

14. From the **Templates** list, click the launch button next to the workflow template.
15. Review the launch dialog and confirm the launch.
16. Watch the **Workflow Visualizer** in the running job view as each node lights up in sequence.
    Observe that the second batch does not start until the first batch completes successfully.
17. Click into individual job template nodes within the running workflow to inspect per-host
    output for that batch.
18. When all nodes complete, verify that the overall workflow status shows success.
19. Confirm the application update result on the fleet by reviewing the final job output or
    any verification step included in the playbook.

## Key Takeaways

- AAP workflows extend job templates with sequencing and conditional logic — critical for
  rolling update patterns where all-at-once deployment is unacceptable for edge fleets
- The Workflow Visualizer provides a real-time view of multi-stage job progression, which is
  more useful for fleet operations than watching raw SSH output
- Rolling update granularity (batch size, serial execution) is typically controlled by the
  playbook or workflow node configuration; the spec leaves the exact mechanism for the
  content author to define during development
- This module covers design spec objective 3; Module 4 shifts from proactive change management
  to reactive, event-driven remediation

## Infrastructure Notes

- The application update playbook is sourced from the Automation Hub collection pre-seeded
  during provisioning; the specific application being updated is defined by the lab author
  during content development
- Workflow node ordering and batch groupings depend on how the inventory was grouped in Module 2;
  students should have a working group structure before attempting this module
