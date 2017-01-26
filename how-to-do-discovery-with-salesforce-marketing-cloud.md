#How to do discovery with Salesforce Marketing Cloud

Configuration in Salesforce Marketing Cloud is flexible and can be adapted to map closely to business and campaign requirements. When making recommendations a key consideration is user expertise and experience with the platform.

Generally when doing discovery there will be 2 phases of information gathering, these are:

***Core configuration** - examples of core configuration items include: business unit requirement gathering; primary domain that will be used for sends; description for how the subscriber will be modeled; and how will data be integrated.
***Campaign configuration** - examples of campaign configuration items include: campaign content and data workflows.

Data model considerations and options:

***List model** - use the list model for less than 500,000 subscribers, there is a preference for simplicity, fast data loads are not required and there are a limited number of subscriber attributes. Skill set required when using the list model requires confidence with using GUI and drop and drag for configuration and filters.
***Data extension model** - use the data extension model for greater than 500,000 subscribers, there are multiple subscriber data sets, fast import speeds are required, SOAP/REST APIs required, triggered sends are required and there is a flexible subscription model. Skill set required when using the data extension model requires confidence with using GUI and drop and drag for configuration and filters, and understanding of data relationships and SQL query language.

Data integration options:

***File import** - use file import to import files from a location into the Marketing Cloud.
***API** - use SOAP/REST APIs for real-time integration with external systems. APIs includes methods for loading data, triggering notifications and starting communications.
***Salesforce connector** - use the connector to integrate the Marketing Cloud with Salesforce.

Campaign automation options:

***TriggerSend** - use a TriggeredSend to send an email on a API request.
***Automation Studio** - use automation studio to start workflows of tasks that include sending emails or SMS. Automation studio can be triggered using following methods: schedule, changed file in specified location or API.
***Journey Builder** - use Journey Builder to send multi-channel campaigns that step the contact through a series of decisions and activities. Journey Builder can be triggered using API, scheduled automation in Automation Studio or Salesforce connector.

