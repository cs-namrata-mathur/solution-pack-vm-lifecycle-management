| [Home](../README.md) |
|--------------------------------------------|

# Usage

The `VM Lifecycle Management` Solution Pack handles VM life cycle on Proxmox, KVM and potentially other hypervisors using FortiSOAR. It is ideal for those interested in leveraging FortiSOAR for IT operations automation, specifically VM lifecycle management.

# Objectives
- *Single Hypervisor Support *

1. FortiSOAR should handle new VM deployment requests (limited to: Debian)
2. Requests can be raised via email. GenAI is used to extract request details and pre-populate the request form automatically with default values.
3. Requests can also be raised via FortiSOAR UI request form
4. Requests is approved by the requestor’s manager or the Cloud-Ops team
5. The created VM along with its attributes is stored on FortiSOAR as a VM Instance record
6. Optional internet access is supported with FortiGate Firewall integration
7. FortiSOAR handles VM Instance decommissions when the expiry date is reached and allow users to destroy the VM on demand
8. The VM Instance record status on FortiSOAR is updated to “Destroyed” and the associated IP address freed up and removed from the firewall configuration
(./res/usage/high-level-flow)

*Requesting a VM Instance*
- `Parse VM Requests Emails` playbook is triggered when a VM request email is fetched (via IMAP) and will create a *VM Instance* record in FortiSOAR
(./res/usage/sample-mail-request)
- It extracts key request attributes with Google Gemini and provides them to `Request VM Instance` playbook, that will create *Network Interface* record for the VM.
- A pre-populated form will be sent to requestor to fill the required information.
(./res/usage/VM-request-form)
- Playbook `> Manage VM Instance Request` will be triggered, once *VM Instance* record is created , which will validate requestor credentials over Active Directory. If it is a valid requestor, his/her Manager's will be prompt for approval of VM request over the email.
(./res/usage/Manager-approval)
- Once the approval is received, provisioning of VM will be taken care by playbook `> Run Provisioning/Deprovisioning Playbook`
This playbook will select best Hypervisor (by calculating available resources) and will provide output if resources are available.
Once Hypervisor is selected, based on Hypervisor a playbook will be chosen dynamically to provision the VM over selected Hypervisor for e.g. if KVM is selected , the playbook chosen will be `> KVM > Provision VM Instances`
VM will be provisioned over Hypervisor using commands (SSH connector) and a requestor will be notified over the email
(./res/usage/Success-VM-provision)
- You can verify your VM over FortiSOAR Console that shows VM details and over KVM as well.
(./res/usage/VM-Instance)
Over KVM:
(./res/usage/KVM)

*Destroying a VM Instance*
- Choose a VM instance that you want to decommission by selecting *Destroy Instance* playbook for e.g. `> KVM > Destroy VM Instance`
(./res/usage/destroy-instance)
- Requested VM will be destroyed using commands (SSH Connector)
- Upon successful decommission, a FortiSOAR VM Instance record will be marked as *Destroyed*
(./res/usage/Destroy-status)
- If internet access was provided for VM during/after provisioning , it will be removed during Post Destruction Cleanup activities.
- Network Interface record will be removed which was linked to destroyed VM

