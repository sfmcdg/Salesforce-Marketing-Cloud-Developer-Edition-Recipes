# How conceptual design is implemented in Salesforce Marketing Cloud

As a guide considerations for conceptual design in Marketing Cloud should be business structure, data integration and campaign requirements.

## Data considerations

Data model considerations and options:

* **List model** - use the list model for less than 500,000 subscribers, there is a preference for simplicity, fast data loads are not required and there are a limited number of subscriber attributes. Skill set required when using the list model requires confidence with using GUI and drop and drag for configuration and filters.
* **Data extension model** - use the data extension model for greater than 500,000 subscribers, there are multiple subscriber data sets, fast import speeds are required, SOAP/REST APIs required, triggered sends are required and there is a flexible subscription model. Skill set required when using the data extension model requires confidence with using GUI and drop and drag for configuration and filters, and understanding of data relationships and SQL query language.

Data integration options:

* **File import** - use file import to import files from a location into the Marketing Cloud.
* **API** - use SOAP/REST APIs for real-time integration with external systems. APIs includes methods for loading data, triggering notifications and starting communications.
* **Salesforce connector** - use the connector to integrate the Marketing Cloud with Salesforce.

## Campaign considerations

Campaign automation options:

* **TriggerSend** - use a TriggeredSend to send an email on an API request.
* **Automation Studio** - use automation studio to start workflows of tasks that include sending emails or SMS. Automation studio can be triggered using following methods: schedule, changed file in specified location or API. Automation Studio can also be used import files into lists and data extensions, and to execute SQL queries.
* **Journey Builder** - use Journey Builder to send multi-channel campaigns that step the contact through a series of decisions and activities. Journey Builder can be triggered using API, scheduled automation in Automation Studio or Salesforce connector.

## Contact Builder

Contact Builder is used to provide access, builder relationships and link data to the Marketing Cloud account. Contact builder provides a single view of the customer that is used to drive one-to-one messaging.

## IP Warming

IP warming is a strategy to ramp up usage of the IP address so that it is trusted by ISPs and emails are not blocked. During an IP warming strategy initially in week 1 send emails to engaged subscribers with a limit per each ISP (e.g. yahoo, hotmail, gmail, etc.). In week 2 progressively increase sends per ISP. In week 3 and 4 aim at sending more emails per ISP. Throughout watch performance stats closely and pull back sending if any significant issues arise. Refer to [IP Address Warming Guide](https://help.marketingcloud.com/en/documentation/exacttarget/resources/email_deliverability/ip_address_warming_guide/) for guide to limits and quantities of IP warm up sends for each week.

