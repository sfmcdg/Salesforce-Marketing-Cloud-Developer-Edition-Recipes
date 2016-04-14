#Working notes for doing setup of Salesforce Marketing Cloud V5 data connector

These are working notes for doing setup of Salesforce Marketing Cloud V5 data connector.

Notes compiled January 2016. Notes do not include setup of Marketing Cloud for Salesforce user email sends.

Before starting support request needs to be put in to provision Marketing Cloud.

##Background

Data is fundamental to Salesforce Marketing Cloud. Data starts the customer journey and data informs the customer journey. Data is used for sending emails and SMSs.
Data can be integrated from files, API or a services. Options: 

**Files** - to integrate data from a file first put file on configured location and then use the file import activity to put data in the Marketing Cloud.

**API* - to integrate data from API use API direct. An example of this is to make a soap API request.

**Services** - to integrate data from a service select app and configure as required.

The Salesforce V5 Connector is a data integration service.

Following is step by step description for how to setup the V5 connector.

##Overview of process

For overview refer to installing V5 connector video https://www.youtube.com/watch?v=jJg0sYGat0M

##Step 1 - prerequisites

Ensure no older versions of connector previously installed.

Best done with most recent version of chrome, firefox or internet explorer.

##Step 2 - Add tracking user to Salesforce

In video refer to https://youtu.be/jJg0sYGat0M?t=2m50 - in summary:

* Login To Salesforce as admin
* In Salesforce navigate to Setup > New user
* Add/specify details as required (hint for name use tracking-MID)

##Step 3 - Preconfiguration > Getting Started > Installing the Marketing Cloud Connector

In video refer to https://youtu.be/jJg0sYGat0M?t=4m32s or in docs refer to https://help.exacttarget.com/de-DE/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/preconfiguration/ in summary:

* Login to Salesforce as admin

Navigate to https://help.exacttarget.com/cs-CZ/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/

Use link to install e.g. https://login.salesforce.com/packaging/installPackage.apexp?p0=04ti0000000t01a - important note, make sure most recent link in docs is used.

Install as admin only with default settings.

Wait for confirmation email from Salesforce.
Use following to see if Marketing Cloud app is installed https://ap1.salesforce.com/0A3?setupid=ImportedPackage

##Step 4 - IP Addresses for Inclusion on Whitelists

In video refer to https://youtu.be/jJg0sYGat0M?t=6m - this can be done whilst waiting for step 1 to complete. For IPs refer to https://help.exacttarget.com/en/documentation/exacttarget/resources/exacttarget_ip_addresses_for_inclusion_on_whitelists/

To determine what instance you're on (e.g. S1, S4, S6 or S7), see accessing the Salesforce Marketing Cloud Application (refer to instance name in Marketing Cloud URL). In summary:

Login SF admin

In SF navigate to Adminster > Security Controls > Network Access and click new
Add/specify IP as required

##Step 5 - Preconfiguration > Getting Started > Applying Admin Permissions

In video refer to https://youtu.be/jJg0sYGat0M?t=7m30s - In docs refer to https://help.exacttarget.com/de-DE/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/preconfiguration/ - For this follow step by step guide in documentation. Remember to apply change to tracking user

##Step 6 - Setup MC API user

In docs refer to https://help.exacttarget.com/en/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/first_time_configuration__connection_mc_admin/

##Step 7 - Setup MC to SF data integration

In docs refer to https://help.exacttarget.com/en/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/first_time_configuration__connection_mc_admin/ and https://help.exacttarget.com/en/documentation/integrated_products__crm_and_web_analytic_solutions/marketing_cloud_connector_v5/connecting_the_clouds/integrating_data_into_your_account_with_data_stream