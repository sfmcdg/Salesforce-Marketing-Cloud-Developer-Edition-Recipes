#How automation occurs with Salesforce Marketing Cloud

> Salesforce Marketing Cloud Automation Studio allows processes consisting of marketing activities to be triggered to start and be scheduled.

Automation Studio is a Marketing Cloud application that is used to manage multi-step processes. Automations in Automation Studio can be triggered by file changes or a schedule. Some of the automation activities include: 

* **Send email** - used to send emails.
* **Import file** - used to import a file into a data extension or list.
* **File transfer** - used to transfer a file from a specified location. The file transfer activity can also unencrypt or uncompress a file.
* **Data extract** - used to create a file from a data extension.
* **SQL query** - used to run a SQL query.

An automation will generally be used to start a batch process to load a file or send a scheduled email.

In Automation Sudio triggered automations are used to start processes that import files and run subsequent tasks. Scheduled automations will generally be used to run recurring processes. Activities in a scheduled automation can be used to evaluate segments to determine if marketing activities should be run using queries and filtered data extensions.

##Links

* [Automation Studio](https://help.marketingcloud.com/en/documentation/automation_studio/)