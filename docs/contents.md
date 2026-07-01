| [Home](../README.md) |
|----------------------|

# Contents

The **VM Lifecycle Management** solution pack contains the following resources.

## Connectors

|**Name**|
| :- |
| Active Directory | 
| DNS |
| Fortinet FortiGate |
| Fortinet FortiMail |
| Google Gemini |
| IMAP |
| SMTP |
| SSH |
| VirusTotal |


## Module Schema

|**Name**|**Description**|
| :- | :- |
| VM Instances | To store the VM instance attributes (name, type, status…etc) |
| Network Interfaces | Representing the VM interface record (IP Address, mask, gateway…etc) |



## Roles

|**Name**|**Description**|
| :- | :- |
| Full App Permissions | Existing FortiSOAR Role to merge newly created modules.



## Playbook Collection

|**Playbook Collection Name**|**Description**|
| :- 
| > AD User Enrichment.json| 
| > Get Public FortiSOAR URL.json| 
| > KVM > Destroy VM Instance.json| 
| > KVM > Provision VM Instances.json| 
| > Manage VM Instance Request.json| 
| > Post Destruction Cleanup.json| 
| > Proxmox > Destroy VM Instance.json| 
| > Proxmox > Provision VM Instances.json| 
| > Run Provisioning_Deprovisioning Playbook.json| 
| > Select Best Hypervisor.json| 
| Allow Internet Access on Fortigate.json| 
| Destroy Expired VM Instances.json| 
| Parse VM Requests Emails.json| 
| Remove Internet Access on FortiGate.json| 
| Request VM Instance.json| 

>**Warning:** We recommend that you clone these playbooks before customizing to avoid loss of information while modifying the solution pack.

## User 

A new user *atlas numid* is added as a part of this solution pack, which will act as a VM requestor.

| [Installation](./setup.md#installation) | [Configuration](./setup.md#configuration) | [Usage](./usage.md) |
|-----------------------------------------|-------------------------------------------|---------------------|