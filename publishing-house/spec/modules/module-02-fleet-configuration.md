# Module 2: Pushing Configuration to the Fleet

## Brief Overview

With the edge fleet registered in AAP, students can now drive coordinated, repeatable configuration
changes across all five devices from a single control point. This module focuses on organizing the
inventory into groups, authoring a job template, and running it to push a fleet-wide configuration
change. It directly demonstrates the value of centralized fleet orchestration over device-by-device
SSH workflows. Students leave with a working job template they can reuse in Module 3.

## Audience and Time

- **Target personas:** Sysadmins and infrastructure engineers
- **Prerequisites:** Module 1 complete — all five edge VMs registered in AAP inventory and verified
  reachable
- **Estimated duration:** ~25 min

## Learning Objectives

<!-- Maps to design spec objective 2:
     "Deploy fleet-wide configuration changes to RHEL for Edge devices using AAP job templates
      and inventory groups" -->

- Organize the edge device inventory into meaningful groups using the AAP Controller UI
- Configure an AAP job template that targets an inventory group and uses a playbook from
  Automation Hub
- Run the job template to apply a configuration change fleet-wide and observe per-host results
  in the AAP job output

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Organizing the Fleet with Inventory Groups | ~7 min |
| 2 | Configuring a Job Template | ~10 min |
| 3 | Running the Fleet Configuration Job | ~8 min |

## Detailed Steps

### Section 1: Organizing the Fleet with Inventory Groups

1. Open the AAP Controller UI and navigate to **Inventories**, then open the inventory created
   in Module 1.
2. Go to the **Groups** tab and click **Add** to create a new group.
3. Name the group to reflect the edge device role (for example, based on the kiosk scenario
   described in the lab environment).
4. Add all five edge VM hosts to the group.
5. Confirm the group membership by reviewing the group's **Hosts** tab — all five devices should
   appear.

### Section 2: Configuring a Job Template

6. Navigate to **Templates** in the AAP Controller UI and click **Add > Add job template**.
7. Name the job template to reflect its purpose (fleet configuration).
8. Set **Inventory** to the inventory created in Module 1 and scope it to the group created in
   Section 1.
9. Browse **Projects** or use the Automation Hub integration to locate the configuration playbook
   provided for this lab. The required collection is pre-seeded in Automation Hub.
10. Set **Playbook** to the fleet configuration playbook specified in the lab instructions.
11. Under **Credentials**, attach the device credential created in Module 1.
12. Review the remaining default settings and save the job template.

### Section 3: Running the Fleet Configuration Job

13. From the **Templates** list, click the launch button next to the job template.
14. Review the launch dialog (no survey or extra variables expected for this template) and confirm
    the launch.
15. Observe the job output page as AAP runs the playbook in parallel across the fleet.
    Note how each host's task results appear in the output stream.
16. When the job completes, verify the final status shows all five hosts succeeded (green).
17. Inspect the **Details** tab of the completed job to review the inventory group targeted,
    the playbook used, and the credential applied.
18. Note what configuration change was made on the edge devices, as indicated by the playbook
    output — this state is the baseline for Module 3.

## Key Takeaways

- Inventory groups let operators target logical subsets of the fleet without maintaining
  separate inventories
- AAP job templates encode the inventory, credential, and playbook into a single reusable
  unit — replacing ad-hoc ssh loops
- The Automation Hub pre-seeded with collections means students configure templates, not package
  management; the control plane handles collection resolution
- This module covers design spec objective 2; the job template pattern established here is
  extended in Module 3 with AAP workflows

## Infrastructure Notes

- The playbook used in this module is provided via the Automation Hub collection pre-seeded
  during provisioning; its specific content is defined by the lab author during development
- All five edge VMs must be reachable (Module 1 verified) before this module's job template
  will succeed
