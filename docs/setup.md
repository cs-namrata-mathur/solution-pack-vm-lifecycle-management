| [Home](../README.md) |
|--------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appear, search **VM Lifecycle Management**.
3. Click the **VM Lifecycle Management** solution pack card.
4. Click **Install** on the lower part of the screen to begin the installation.

# Configuration

Complete the following tasks before using this solution pack.

## Prerequisites
 
- Install the solution pack and configure connectors listed in the [Contents](./contents.md) file. 
- Wait for all virtual machines to start. This process can take upto several minutes.
- Verify that the `atlas numid` user exists in **Settings > Users**. <br />This solution pack uses the `atlas numid` account as the default requestor. If you want to use a different requestor account, create a new user with the same roles, permissions, and team assignments as `atlas numid`, then specify the appropriate email address.
- Set the`default_approver_email` variable to the email address that will approve virtual machine requests.
- Install and Configure a DNS connector to use a public DNS server, such as `1.1.1.1`.

## Configure Required Connectors

Configure the connectors listed in the [Contents](./contents.md) file. For connectors that require additional configuration, review and apply the requirements in this section during setup.

### FortiGate Firewall Configurations

Before configuring the Fortinet FortiGate connector, complete the following tasks in the FortiGate GUI:

1. Sign in to the FortiGate GUI using an administrator account.
2. Verify that the `Allowed_LAN_Devices` address group exists. Create it if necessary.
3. Verify that an SNAT policy exists to allow traffic from `Allowed_LAN_Devices` to the internet. Create the policy if necessary.
4. Create a web filter profile named **FortiSOAR** and enable **URL Filter**.
5. Create an application control profile named **FortiSOAR** using the default settings.
6. Generate an API key with administrator privileges.

### FortiGate Connector Configurations

Add a FortiGate connector configuration with the following settings.

|**Setting**|**Value**|
| :- | :- |
| Configuration Name | `FortiGate` |
| Mark as default configuration | Enabled |
| Host | Your FortiGate IP address |
| API Key | API key generated earlier |
| Port | FortiGate API communication port |
| Web Filter Profile Name | `FortiSOAR` |
| Application Control Profile Name | `FortiSOAR` |
| Verify SSL | `False` |

 Click **Save** to save the configuration

### SSH Connector Configurations

The SSH connector is installed with FortiSOAR.

Configure the connector to connect to the KVM host used for VM provisioning and deprovisioning. Ensure that one of its configurations is marked as `Mark as default configuration`.

### SMTP Connector Configurations

The SSH connector is installed with FortiSOAR.

Configure the connector and ensure that one of its configurations is marked as `Mark as default configuration`.

>[!Note]
>
> Verify that the default FortiMail configuration allows SMTP relay from the FortiSOAR IP address. If relay is not allowed, update the FortiMail configuration before continuing. 
>

### Code Snippet Connector Configurations

The Code Snippet connector is installed with FortiSOAR.

Before using this connector, enable **Custom Code Execution**:

1. Navigate to **Settings > System Configuration > Advanced Development Features**.
2. Under **Custom Code Execution**, review the risks and usage guidelines.
3. Select **I understand the risks and accept responsibility for enabling Custom Code Execution.**
4. Click **Submit**.


### IMAP Connector Configurations

The IMAP connector is installed with FortiSOAR. Configure it as follows:

1. Configure the connector to use the mailbox that receives VM approval emails (for example, a FortiMail mailbox used by the approver).
2. Select the **Mark as default configuration** checkbox.
2. Once configured and Health Check is Available, click **Configure Data Ingestion**.
3. In the **Fetch Data** screen, select **Use Unified Communication** to record emails in the Communications module, and continue to configure data ingestion.
4. In the **Scheduling** screen, schedule the connector to run every few minutes during testing. After testing is complete, adjust the schedule to meet your production requirements, and then Click **Save Settings & Continue**.
6. In the **Summary** screen, click **Done** to complete the data ingestion and exit the Data Ingestion Wizard.


#### Update the IMAP Data Ingestion Playbook

1. Navigate to **Automation > Data Ingestion**.
2. Search for **IMAP**.
3. In the **Actions** column, click **Playbooks** to open the IMAP ingestion playbooks.
4. Click the **IMAP > Ingest** playbook, and open the **Create Record** step.
5. Update the following fields:
    - Subject to 
   `{{vars.item.headers.Subject}}` instead of    
   `{{vars.item.headers.subject}}`  
    - Update Email From to    
   `{{vars.item.headers.From}}`
    - Update Email Recipients (To) To     
   `{{vars.item.headers.To}}`
    - Sender Domain:    
   `{% if vars.item.headers.From %}{{(vars.item.headers.From.split('<')[-1] \| replace(">","")).split('@')[-1] \| replace(">","")}}{% endif %}`
    - Sender Email Address:    
   `{% if vars.item.headers.From %}{{vars.item.headers.From.split('<')[-1] \| replace(">","")}}{% endif %}`  
    - Return Path:     
  `{{ vars.item.headers['Return-Path'] }}`
    - Source ID:    
  `{{ vars.item.headers['Message-ID'] | join }}`
    - Name:    
  `{% if vars.item.headers.Subject %} {{vars.item.headers.Subject}} {% else %} Email from {{vars.item.headers.From}} {% endif %}`
6. Once all the changes are made, click **Save** to save the Create Record step.
7. Click **Save Playbook** and exit the playbook editor.

To verify the configuration, send a test email (for example, `atlas@fortielab.com` to `fortisoar@fortielab.com`) and confirm that the email is ingested and parsed correctly.

### Enable Custom Connectors Upload

Uploading custom connectors requires **Custom Code Execution** to be enabled.

If you have not already enabled this feature, then navigate to **Settings > System Configuration > Advanced Development Features**. Under the **Custom Code Execution** section, review the information, including the Risks and Guidelines for Safe Use, then select the **I understand the risks and accept responsibility for enabling Custom Code Execution.** checkbox and click **Submit**. 

After enabling Custom Code Execution:  

- Install and configure the **Google Gemini Connector**.
- Install the **Playbook Buttons** widget from the Content Hub.




| [Usage](./usage.md) | [Contents](./contents.md) |
|---------------------|---------------------------|
