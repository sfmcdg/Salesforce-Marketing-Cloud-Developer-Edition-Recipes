#How account configuration works with Salesforce Marketing Cloud

##Salesforce Marketing Cloud Roles

Salesforce Marketing Cloud uses [roles](https://help.marketingcloud.com/en/documentation/marketing_cloud/smc_roles/) to manage how the users can access the to application and features. In summary roles consist of:

* **Marketing Cloud Administrator** - allows a person with this role to assist roles to users and manage Mobile Channels Social Channels, Marketing Cloud Apps and Marketing Cloud Tools. Assign a user to the **Marketing Cloud Administrator** role if they want to be able to have access to all features within the marketing Cloud account.
* **Marketing Cloud Viewer** - allows a person with this role to view cross-channel marketing activity that results in Marketing Cloud. Assign a user to the **Marketing Cloud Viewer** if they want to be able to view, but not change or execute campaigns in the Marketing Cloud.
* **Marketing Cloud Channel Manager** - allows a person with this role to create and execute cross-channel interactive marketing campaigns and administer Social and Mobile Channels. Assign a user to the **Marketing Cloud Channel Manager** role if they want to be able to view and create campaigns. A user in this role will not be able to administer users or change configurations.
* **Marketing Cloud Security Administrator** - allows a person with this role to maintain Watchdog security settings and manage user activity and alerts. Assign a user to the **Marketing Cloud Security Administrator** if they want be able to administer users or change configurations. This user has access to MobileConnect and MobilePush, and limited access to email campaigns, automations, content builder and social pages. 
* **Marketing Cloud Content Editor/Publisher** - allows a person with this role to create and deliver messages through Mobile and Sites Channel Apps. Assign a user to the **Marketing Cloud Content Editor/Publisher** role if they want to be able to create and change content.

##Salesforce Marketing Cloud Business Units

A [business unit](https://help.marketingcloud.com/en/documentation/exacttarget/enterprise/enterprise_20_overview/business_units/) is a feature for helping to manage hierarchical structures and data relationships. Business units can mirror workflow processes, demographic and functional structures within the business. Users can be assigned to business units which can help to resolve branding and regulatory compliance considerations. Content and data can be shared accross business units. Business units are a feature of an Enterprise 2.0 marketing Cloud account.

###Examples of business unit strategies

* **Publication strategy** - an example of a business that uses a publication strategy for business units would be one that is made up of different brands.
* **Demographic strategy** - an example of a business that uses a demographic strategy for business units would be one that operates in different regions or countries.
* **Workflow processes strategy** - an example of a business that uses a Workflow processes strategy for business units would be one that has logical distinctions between business functions.
* **Organisational structure strategy** - an example of a business that uses a organisational structure strategy for business units would be one that has a requirement to map business units to the organisational structure of the business.

##Salesforce Marketing Cloud Reply Mail Management

[RMM (Reply Mail Management)](https://help.marketingcloud.com/en/documentation/exacttarget/admin/reply_mail_management/) allows emails received as replies to campaign sends to be managed. Using RMM Marketing Cloud emails received can automatically be acknowledged and unsubscribe depending on keywords.

When setting up RMM there is a one-time requirement to specify a reply subdomain, make the appropriate DNS changes and configure RMM as required. Optional setup includes a triggered send and sender profile.

##Salesforce Marketing Cloud Sender Authentication Package

[placeholder for what is SAP (Sender Authentication Package) and how it relates to a business unit, include information about link wrapping, landing pages, image URLs]

