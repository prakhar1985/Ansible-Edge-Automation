# Module 4: Detecting and Remediating a Security Finding

## Brief Overview

Proactive configuration management and scheduled updates cover planned changes, but edge fleets
also face unplanned security events that require immediate automated response. This module
introduces Event-Driven Ansible (EDA), which listens for conditions on managed devices and
triggers remediation playbooks automatically — without operator intervention for each event.
Students will configure an EDA rulebook that detects a simulated security finding on the edge
fleet and observe the automated remediation running through AAP. This closes the device
lifecycle loop that started with onboarding in Module 1.

## Audience and Time

- **Target personas:** Sysadmins and infrastructure engineers
- **Prerequisites:** Modules 1–3 complete — fleet registered, credentials in place, and
  students familiar with AAP job templates; Event-Driven Ansible is a new concept introduced
  in this module
- **Estimated duration:** ~20 min

## Learning Objectives

<!-- Maps to design spec objective 4:
     "Detect and automatically remediate a security finding on edge devices using Event-Driven
      Ansible rulebooks" -->

- Identify the components of an Event-Driven Ansible rulebook (source, condition, action) using
  the provided rulebook for this lab
- Configure and activate the EDA rulebook within the AAP environment to monitor the edge fleet
- Trigger a simulated security finding on an edge device and observe the automated remediation
  job executing in AAP without manual intervention

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Introducing Event-Driven Ansible and the Rulebook | ~5 min |
| 2 | Activating the Rulebook in AAP | ~8 min |
| 3 | Triggering and Observing Automated Remediation | ~7 min |

## Detailed Steps

### Section 1: Introducing Event-Driven Ansible and the Rulebook

1. In the AAP Controller UI, navigate to the Event-Driven Ansible section (exact UI location
   depends on AAP 2.6 navigation; follow the lab environment panel guidance).
2. Locate the pre-provided rulebook for this module in the lab materials or Automation Hub
   content.
3. Review the rulebook structure: identify the **source** (what EDA is listening to), the
   **condition** (what triggers a response), and the **action** (what AAP job or playbook runs
   when the condition is met).
4. Note the specific security finding that the rulebook is designed to detect, as described
   in the lab instructions.

### Section 2: Activating the Rulebook in AAP

5. In the EDA section of the AAP Controller UI, create a new rulebook activation (or equivalent
   EDA activation object in AAP 2.6).
6. Attach the provided rulebook to the activation.
7. Associate the activation with the edge fleet inventory from Module 1 so that EDA knows which
   devices to monitor.
8. Link the remediation job template or playbook that should run when the rulebook condition
   fires. This may be an existing job template from a prior module or a new one defined in
   the lab instructions.
9. Save and activate the rulebook. Confirm that the activation status shows as running or
   listening.

### Section 3: Triggering and Observing Automated Remediation

10. Following the lab instructions, introduce the simulated security finding on one of the edge
    devices. The exact trigger mechanism (for example, a configuration change or a specific
    file/state condition) is defined by the rulebook and will be specified in the lab content.
11. Switch to the **Jobs** view in the AAP Controller UI and watch for a new job to appear
    automatically — this job should have been triggered by EDA, not by a manual launch.
12. Confirm that the job was initiated by the EDA activation (check the job's launch source or
    metadata).
13. Observe the job output as the remediation playbook runs against the affected edge device.
14. Verify that the security finding is remediated: the output should indicate the corrective
    action was applied and the device is returned to the expected state.
15. If time permits, introduce the finding on a second device and observe EDA triggering the
    remediation again — demonstrating that the detection-and-response loop is continuous and
    does not require manual intervention.

## Key Takeaways

- Event-Driven Ansible extends AAP from a tool for planned changes to a platform for automated
  reactive operations — the key differentiator for edge scenarios where operator presence
  cannot be assumed
- Rulebooks encode detection logic (source + condition) and response logic (action) in one
  place, making the remediation policy auditable and version-controlled
- The EDA-to-AAP job integration means remediation uses the same job templates, credentials,
  and inventory already configured in Modules 1–3 — no separate toolchain
- This module covers design spec objective 4 and completes the full device lifecycle arc:
  onboard (M1) → configure (M2) → update (M3) → remediate (M4)

## Infrastructure Notes

- Event-Driven Ansible is included with Red Hat Ansible Automation Platform 2.6; no separate
  installation is required in the lab environment
- The simulated security finding and its trigger mechanism are defined by the lab content
  author during development; this outline does not prescribe the specific finding
- EDA rulebook content is sourced from the Automation Hub collections pre-seeded during
  provisioning
