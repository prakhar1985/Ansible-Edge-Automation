# Module 1: Device Onboarding and Inventory Registration

## Brief Overview

Edge devices cannot be managed until they are known to the controller. This module addresses the first
step of the device lifecycle: making the five RHEL 9 edge VMs visible to Ansible Automation Platform 2.6.
Students will configure device credentials and build a dynamic inventory so that subsequent modules can
target the fleet by name and group. This module establishes the working environment that every later
exercise depends on.

## Audience and Time

- **Target personas:** Sysadmins and infrastructure engineers
- **Prerequisites:** General knowledge of AAP UI navigation; no prior module required (this is the first)
- **Estimated duration:** ~20 min

## Learning Objectives

<!-- Maps to design spec objective 1:
     "Register remote edge devices with Ansible Automation Platform using dynamic inventory
      and device credentials" -->

- Explore the pre-deployed AAP 2.6 Controller environment to locate pre-created organization
  stubs and credential types
- Create machine credentials for the edge device fleet within the AAP Controller UI
- Build a dynamic inventory that covers all five RHEL 9 edge VMs and verify that each device
  is reachable from the controller

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Orienting to the AAP Environment | ~5 min |
| 2 | Creating Device Credentials | ~7 min |
| 3 | Building and Verifying the Inventory | ~8 min |

## Detailed Steps

### Section 1: Orienting to the AAP Environment

1. Open a browser and navigate to the AAP Controller URL provided in the lab environment panel.
2. Log in with the student credentials shown in the environment panel.
3. Observe the pre-created organization stub in the left-hand navigation under **Organizations**.
   Note the name — all subsequent work will be done inside this organization.
4. Navigate to **Credentials** and review the credential types that are pre-created.
   Identify the machine credential type that will be used for the edge devices.
5. Navigate to **Inventories** and confirm that no inventory yet exists for the edge fleet.

### Section 2: Creating Device Credentials

6. In the AAP Controller UI, go to **Credentials** and click **Add**.
7. Select the pre-created machine credential type for edge devices.
8. Fill in the credential fields using the device access information provided in the lab
   environment panel (hostname access method, username, and key or password as applicable).
9. Assign the credential to the pre-created organization.
10. Save the credential and confirm it appears in the credential list.

### Section 3: Building and Verifying the Inventory

11. Navigate to **Inventories** and click **Add** to create a new inventory.
12. Name the inventory and assign it to the pre-created organization.
13. Save the inventory, then open its **Hosts** tab.
14. Add each of the five edge VM hostnames (provided in the lab environment panel) as individual
    hosts in the inventory.
15. Associate the device credential created in Section 2 with the inventory.
16. Use the **Launch ad hoc command** or equivalent inventory sync check to confirm that all five
    hosts are reachable. Observe that each host returns a successful ping or connection result.
17. Verify that all five devices show a green/connected status in the inventory host list before
    proceeding.

## Key Takeaways

- AAP 2.6 uses credentials and inventories as the two foundational objects for reaching managed hosts
- Pre-seeded organization stubs and credential types reduce setup time; students complete the
  device-specific configuration themselves
- A verified inventory is a prerequisite for every subsequent module — if a host is unreachable
  here, later job templates will fail
- This module covers design spec objective 1 in full; the remaining three modules build on the
  registered fleet

## Infrastructure Notes

- AAP Controller and Automation Hub are pre-deployed on a dedicated RHEL 9 host; students do not
  install or configure the control plane
- Edge VM hostnames and access credentials are injected into the lab environment panel by the
  provisioning automation
- Students interact exclusively through the AAP Controller UI; no direct SSH to edge VMs
