#How reporting works with Salesforce Marketing Cloud

> Salesforce Marketing Cloud reporting allow for the marketer to view, access and use reporting data in campaigns.

Reporting options within Salesforce Marketing Cloud include:

* [**Reports**](https://help.marketingcloud.com/en/documentation/reports/getting_started_with_reports/) - used with GUI to generate various send reports.
* [**Data views**](https://help.marketingcloud.com/en/documentation/exacttarget/interactions/activities/query_activity/) - used with queries to update data extensions with subscriber reporting data.
* [**Tracking Extract**](https://help.marketingcloud.com/en/documentation/automation_studio/using_automation_studio_activities/use_a_data_extract_activity/extract_types_reference/) - option in the [Data Extract Activity](https://help.marketingcloud.com/en/documentation/automation_studio/using_automation_studio_activities/use_a_data_extract_activity/) that can be used to export a reporting data file.
* [**Send logging**](https://help.marketingcloud.com/en/documentation/exacttarget/subscribers/send_logging/) - used to log run-time data about sends to a data extension. The send log is an option that needs to enabled in the Marketing Cloud account before use. To create a send log data extension select the `send log` option from templates when creating the send log data extension. The send log data extension can log fields on the data extension used with the send. To log fields ensure that there is a copy of the sendable data extension field required for logging on the send log data extension. This is useful for adding custom fields that are specific to the Marketing Cloud account to a single log of sent data. The send log data extension can be used with queries to help create custom reports.
