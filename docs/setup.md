| [Home](../README.md) |
|--------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appear, search **VM Lifecycle Management**.
3. Click the **VM Lifecycle Management** solution pack card.
4. Click **Install** on the lower part of the screen to begin the installation.

# Configuration
 
- Install the solution pack and configure connectors mentioned in the [Contents](./contents.md) file. 
- Be aware booting up all the machine may take few minutes
- Please verify and ensure that the new user `atlas numid` is added as a FortiSOAR user in Settings > Users. In a similar way (assigning the same roles and permissions, teams, etc) you can add your own user and assign an email id to be used to submit a request (requestor).
In the current setup, this solution pack will use user `atlas numid` to submit request (requestor)
- Configure the value of the`default_approver_email` variable to the email account that will approve the VM requests.
- Install and Configure a DNS connector setting it up with a public DNS of your choice (e.g. 1.1.1.1)

## Configuring the required connectors
Configure the connectors mentioned in the [Contents](./contents.md) file, keeping the following points in mind:

### FortiGate Firewall Configurations

Install and Configure a FortiGate connector as follows:

1. Open FortiGate GUI  with admin privilages
2. Create an address group: Allowed_LAN_Devices if it doesn’t exist already
3. Create an SNAT policy to allow traffic from Allowed_LAN_Devices to the internet if it doesn’t exist already
4. Create a Web Filter Profile named *FortiSOAR* enabling URL Filter setting
5. Create an Application Control Profile named *FortiSOAR* with default settings
6.Create an API key with admin privileges

### FortiGate Connector Configurations

Install and Configure a FortiGate connector with the following settings:

- Configuration Name: FortiGate.
- Mark as default configuration.  
-  host: `Your FortiGate IP`.  
- API Key: `Add the API Key you have just created`.  
- Port: `FortiGate API communication Port` 
- Web Filter Profile Name: FortiSOAR.  
- Application Control Profile Name: FortiSOAR.  
-  Verify SSL: False.  
 Click Save to save the configuration

### SSH Connector Configurations

SSH Connector comes pre-installed with FortiSOAR and it is required in this solution pack to run commands on the KVM host for provisioning and deprovisioning VMs. Configure the SSH connector for KVM access and ensure that one of its configurations is marked as `Mark as default configuration`.

### SMTP Connector Configurations

SMTP Connector comes pre-installed with FortiSOAR. Configure it keeping the following point in mind and ensure that one of its configurations is marked as `Mark as default configuration`.

>[!Note]
>
> Verify that the default FortiMail configuration should allow relay from an FortiSOAR IP. if it doesn’t, please add it. 
>
  * Install and configure SMTP Connector
  * The default FortiMail config should allow relay from FortiSOAR IP, if it doesn’t, please add it.

### Code Snippet Connector Configurations

Code Snippet comes pre-installed with FortiSOAR.

>[!Note]
>
> Enable Custom Code Execution. Navigate to `Settings > System Configuration > Advanced Development Features`. Under the **Custom Code Execution** section, review the information, including the Risks and Guidelines for Safe Use, then select the **I understand the risks and accept responsibility for enabling Custom Code Execution.** checkbox and click **Submit**.
>

### IMAP Connector Configurations

SMTP Connector comes pre-installed with FortiSOAR. Configure it keeping the following points in mind and ensure that one of its configurations is marked as `Mark as default configuration`.

- Configure your webmail for this configuration for e.g. FortiMail ( This should be your approver's email account)
- Enable data Ingestion and configure it
  * Use Unified Communication : This will record emails in the communication module
  * Save Mapping & Continue
  * Schedule the connector to run every couple of minutes (to speed up test while you are developing the playbooks). Once the testing is done you can adjust the schedule as per your requirement.

#### Fixing IMAP Data Ingestion
  * Head to Automation > Data Ingestion and search for IMAP
  * Click on Playbooks and open IMAP > Ingest playbook
  * Open the Create Record step and set the subject to 
   {{vars.item.headers.Subject}} instead of    
   {{vars.item.headers.subject}}.  
  * Update Email From to    
   {{vars.item.headers.From}}
   * Update Email Recipients (To) To     
   {{vars.item.headers.To}}
  * Sender Domain:    
   {% if vars.item.headers.From %}{{(vars.item.headers.From.split('<')[-1] | replace(">","")).split('@')[-1] | replace(">","")}}{% endif %}
  * Sender Email Address:    
   {% if vars.item.headers.From %}{{vars.item.headers.From.split('<')[-1] | replace(">","")}}{% endif %}.  
  * Return Path:     
  {{ vars.item.headers['Return-Path'] }}
  * Source ID:    
  {{ vars.item.headers['Message-ID'] | join }}
  * Name:    
  {% if vars.item.headers.Subject %} {{vars.item.headers.Subject}} {% else %} Email from {{vars.item.headers.From}} {% endif %}
  * Save and quit the playbook editor
Test with another Dummy email for e.g. atlas@fortielab.com -> fortisoar@fortielab.com to make sure emails are being ingested and parsed properly

### Enable Custom Connectors Upload

To enable uploading of custom connectors, **Custom Code Execution** must be enabled. Navigate to `Settings > System Configuration > Advanced Development Features`. Under the **Custom Code Execution** section, review the information, including the Risks and Guidelines for Safe Use, then select the **I understand the risks and accept responsibility for enabling Custom Code Execution.** checkbox and click **Submit**. 

Once enabled:  

- Install and configure *Google Gemini Connector*
- Install *Playbook Buttons* widget from Content hub.




| [Usage](./usage.md) | [Contents](./contents.md) |
|---------------------|---------------------------|
