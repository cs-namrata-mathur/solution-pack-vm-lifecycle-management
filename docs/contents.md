| [Home](../README.md) |
|----------------------|

# Contents

The **VM Lifecycle Management** solution pack includes the following resources to automate and manage the lifecycle of virtual machines (VMs).

## Roles

|**Role**|**Description**|
| :- | :- |
| Full App Permissions | Existing FortiSOAR role that grants access to the modules installed by this solution pack.

## System Views

N/A

>[!Note]
>
>To add VM Lifecycle Management to the FortiSOAR left navigation menu, click **Settings** > **Navigation**, select **VM Lifecycle Management** and then click **Add To Menu**. The **VM Lifecycle Management** menu provides access to the **Network Interfaces** and **VM Instances** modules.
>

## Users

|**User**|**Description**|
| :- | :- |
| atlas numid | A new user `atlas numid` account created by the solution pack acts as the default VM requestor.

## Module Schema

|**Module Schema**|**Description**|
| :- | :- |
| VM Instances | Represents a record that stores VM instance attributes, including the name, type, and status. |
| Network Interfaces | Represents a record of the VM interface that stores network interface information, including the IP address, subnet mask, gateway, and related network settings. |

## Playbook Collection
| 02 - VM Lifecycle Management |
| :----------------------------------------------- |


| **Playbook Name**                              | **Description**                                                                                                                                                                   |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| > AD User Enrichment.json| Enriches a user with information from Active Directory.   |
| > Get Public FortiSOAR URL.json| Sets the `Server_FQHN` global variable.   |
| > KVM > Destroy VM Instance.json| Destroy an individual KVM virtual machine based on the specified parameters.   |
| > KVM > Provision VM Instances.json| Creates a virtual machine instance on a KVM hypervisor.   |
| > Manage VM Instance Request.json| Processes VM instances requests and approvals.   |
| > Post Destruction Cleanup.json| Cleans up network interfaces, Internet access, and related resources after a VM is deleted.    |
| > Proxmox > Destroy VM Instance.json| Destroy an individual Proxmox virtual machine based on the specified parameters.  |
| > Proxmox > Provision VM Instances.json| Creates a virtual machine instance on Proxmox.   |
| > Run Provisioning_Deprovisioning Playbook.json| Runs the appropriate provisioning or deprovisioning playbook dynamically based on the target hypervisor.   |
| > Select Best Hypervisor.json| Selects the optimal hypervisor based on available resources.   |
| Allow Internet Access on Fortigate.json| Includes a decision flow, which if approved, grants Internet access to approved virtual machines.   |
| Destroy Expired VM Instances.json| Iterates over existing VM instances and destroys expired ones.   |
| Parse VM Requests Emails.json| Parses emails with VM requests.   |
| Remove Internet Access on FortiGate.json| Removes Internet access for for destroyed VMs.   |
| Request VM Instance.json| Submits a virtual machine provisioning request and manages the approval workflow.   |

>[!Important]
>
>Clone the provided playbooks before making customizations. This prevents custom changes from being overwritten when the solution pack is upgraded.
>


## Connectors

|**Connector**|**Description**|
| :- | :- |
| Active Directory | Enables FortiSOAR to communicate with Microsoft Active Directory and automate user and group management tasks. |
| DNS | Integrates with DNS servers to automate DNS lookups. |
| Fortinet FortiGate | Enables FortiSOAR playbooks to automate interactions with Fortinet FortiGate firewalls.
| Fortinet FortiMail | Automates interactions with Fortinet FortiMail to process and manage email security operations, including spam, malware, and phishing detection. |
| Google Gemini | Enables FortiSOAR playbooks to automate interactions with Google Gemini. 
| IMAP |Retrieves email messages from one or more IMAP mailboxes for automated processing.
| SMTP |Sends email messages from FortiSOAR playbooks using the Simple Mail Transfer Protocol (SMTP). |
| SSH | Enables secure remote access to Linux, UNIX, and network devices over the Secure Shell (SSH) protocol.|
| Proxmox | Automates workflows that integrate with the open-source Proxmox Virtual Environment (Proxmox VE). |

## Picklists

- VM Status
- VM Type

## Module Views

- VM Instances - Detail, List, Form
- Network Interfaces - Detail, List, Form

## Playbook Blocks

- Dynamic Manager and Device List

## Global Variables

- infrastructure_team_email
- Server_fqhn
- Current_Date


| [Installation](./setup.md#installation) | [Configuration](./setup.md#configuration) | [Usage](./usage.md) |
|-----------------------------------------|-------------------------------------------|---------------------|