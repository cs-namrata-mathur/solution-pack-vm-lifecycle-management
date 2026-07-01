| [Home](../README.md) |
|----------------------|

# Contents

The **VM Lifecycle Management** solution pack contains the following resources.

## Connectors

|**Name**|**Description**|
| :- | :- |
| Active Directory | An Active Directory Connector in FortiSOAR is an integration that enables FortiSOAR to communicate with Microsoft Active Directory and allows to automate user and group tasks|
| DNS | It allows integration with a DNS server to automate DNS lookups |
| Fortinet FortiGate | It facilitates automated interactions, with a Fortinet FortiGate firewall using FortiSOAR playbooks.
| Fortinet FortiMail | This connector automates operations over FortiMail email security gateway that monitors email messages on behalf of an organization to identify messages that contain malicious content, including spam, malware and phishing attempts. |
| Google Gemini | This connector facilitates automated interactions, with a Google Gemini server using FortiSOAR playbooks. 
| IMAP | Using this connector we can set up multiple email accounts and fetch emails from different email accounts.
| SMTP |It is used to send emails from SOAR playbooks using the Simple Mail Transfer Protocol (SMTP). |
| SSH | It enables secure remote access to Linux, Unix, and network devices over the SSH (Secure Shell) protocol.|
| VirusTotal | This connector performs automated operations, such as scanning and analyzing suspicious files and URLs and retrieving reports from VirusTotal for files, IP addresses, and domains.|


## Module Schema

|**Name**|**Description**|
| :- | :- |
| VM Instances | To store the VM instance attributes (name, type, status etc.) |
| Network Interfaces | Representing the VM interface record (IP Address, mask, gateway etc.) |



## Roles

|**Name**|**Description**|
| :- | :- |
| Full App Permissions | Existing FortiSOAR Role to merge newly created modules.



## Playbook Collection
| 02 - VM Lifecycle Management |
| :----------------------------------------------- |


| Playbook Name                              | Description                                                                                                                                                                   |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| > AD User Enrichment.json| Enrich user with Active Directory data.   |
| > Get Public FortiSOAR URL.json| Set Server_FQHN global variable.   |
| > KVM > Destroy VM Instance.json| Destroy individual VM defined with params.   |
| > KVM > Provision VM Instances.json| Create VM Instances.   |
| > Manage VM Instance Request.json| Process VM instances requests and approvals.   |
| > Post Destruction Cleanup.json| Cleanup Internet access, network interface etc.    |
| > Proxmox > Destroy VM Instance.json| Destroy individual VM defined with params.   |
| > Proxmox > Provision VM Instances.json| Provision VM on Proxmox.   |
| > Run Provisioning_Deprovisioning Playbook.json| Wrapper to run playbooks dynamically based on the target hypervisor.   |
| > Select Best Hypervisor.json| Pick which hypervisor to use based on available resources.   |
| Allow Internet Access on Fortigate.json| If Approved VM is allowed to access internet.   |
| Destroy Expired VM Instances.json| Iterate over existing VM instances and destroy expired ones.   |
| Parse VM Requests Emails.json| Parse emails with VM requests.   |
| Remove Internet Access on FortiGate.json| Remove access for destroyed VMs.   |
| Request VM Instance.json| Request virtual machine deployment and manage approval process.   |

>**Warning:** We recommend that you clone these playbooks before customizing to avoid loss of information while modifying the solution pack.

## User 

A new user *atlas numid* is added as a part of this solution pack, which will act as a VM requestor.

| [Installation](./setup.md#installation) | [Configuration](./setup.md#configuration) | [Usage](./usage.md) |
|-----------------------------------------|-------------------------------------------|---------------------|