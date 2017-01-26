#How Marketing Cloud Connect works with Salesforce Marketing Cloud

For Marketing Cloud Connect prerequisites refer to account and user prerequisites in [Prerequisites & Critical Concepts](https://help.marketingcloud.com/en/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/prerequisites__critical_concepts/), in summary:

* **Use a supported Salesforce.com edition with the v5 connector** - includes:  Unlimited, Enterprise, performance and person Accounts. Professional Edition is supported by the v2 connector. Government Cloud requires a custom script to set up a custom domain which must be scheduled 30 days in advance of planned installation. CipherCloud is not supported by Marketing Cloud Connect.
* **Use a supported Salesforce Marketing Cloud account** - includes:  Agency or Agency Client Editions: Core Edition, Advanced Edition, Lock and Publish, Enterprise 2.0 Edition, or Reseller Edition. 
* **Enable Salesforce integration for your Salesforce Marketing Cloud account** - this requires support from Salesforce Marketing Cloud to enable Salesforce Marketing Cloud Connect in the Marketing Cloud account.
* **Administrator credentials/permissions* - obtain administrator credentials for logging in to Salesforce.com and the Salesforce Marketing Cloud.
* **4 custom tabs in Salesforce** - ensure four (4) custom tabs are available in Salesforce.
* **List of integration users** - compile a list of integration users.
* **Create a report in Salesforce** - create a report that defines an intended send to list. Sending to reports requires either a Contact ID or Lead ID.
* **Create a test email in Marketing Cloud - validate email to ensure that it passes validation.
* **Use recent Chrome or Firefox** - setup is best done with most recent version of Chrome or Firefox.
* **Default Sender Profiles, Delivery Profiles and Send Classification** - ensure that all Default Sender Profiles, Delivery Profiles and Send Classifications have not been deleted or renamed.
* **Users must have license for Marketing Cloud and license for Sales or Service Clouds with required permissions.

##Sending Email

* **Sending an email from Sales or Service Cloud** - to send an email in Sales or Service Cloud:
  1. Click on the Marketing Cloud tab.
  2. Click find in the email row to access Salesforce Marketing Cloud emails.
  3. Click My Emails or Shared Items to view a list of existing Salesforce Marketing Cloud emails.
  4. Proceed to config email to be sent.
* **Sending an email from Marketing Cloud using Send Email in Interactions** - to send an email:
  1. Create a Salesforce Send Email in Interactions.
  2. Select email content.
  3. In recipients select Salesforce reports, Salesforce campaigns, Salesforce Data Extensions, or Salesforce Shared Data Extensions.
  4. Complete remaining fields as required.
  5. Save.
  6. Select the Salesforce Send from the grid and click Send.
* **Sending an email from Marketing Cloud using Guided Send** - to send an email proceed as usual and in recipients select Salesforce Shared Data Extensions.
* **Sending an email from Marketing Cloud using Automation Studio** - create a data filter based on the Salesforce data Extension and then use the filtered data extension in the send activity.

To segment Service Cloud data in Marketing Cloud create a data filter from the Salesforce data extension and then use the drop and drag filter to setup required segmentation.

Links

* [#Working notes for doing setup of Salesforce Marketing Cloud V5 data connector](working-nodes-for-setup-of-salesforce-marketingcloud-v5-connector.md)

