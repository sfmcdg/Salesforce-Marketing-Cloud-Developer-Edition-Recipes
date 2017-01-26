#How emails are built with Salesforce Marketing Cloud

Required for an email send the following are required:

* Email content
* Recipients
* Publication list is optional
* Subject line
* Send from user name, classification or sender profile

Emails can be sent as a guided send or as a send activity in Automation Studio.

Emails can be personalised using:

* Personalisation strings
* AMPscript
* Dynamic content
* Guide Template Language

The difference between SSJS and AMPScript is that SSJS is processed by the Salesforce Marketing Cloud servers, SSJS is based on JavaScript and SSJS contains more features that AMPScript.

The difference between Dynamic Content and AMPScript is that Dynamic Content uses business rules with subscriber's attributes to display content areas, whereas AMPScipt uses lookup functions and logic statements to format content dynamically.

Other Marketing Cloud email add-on options include:

* Link Alias tags
* [Impression tracking](https://help.marketingcloud.com/en/documentation/exacttarget/tracking/impression_tracking/) - used to performance of emails that use regions with AMPscript or dynamic content.
* Web Analytics Connector - used to add params to all outgoing links

