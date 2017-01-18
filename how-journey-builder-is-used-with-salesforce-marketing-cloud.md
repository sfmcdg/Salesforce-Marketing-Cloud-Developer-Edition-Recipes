#How Journey Builder is used with Salesforce Marketing Cloud

> Salesforce Marketing Cloud Journey Builder allows the campaign designer to implement and easily share complex digital marketing requirements. Journey Builder features an easy to use interface that does not require programming.

Journey Builder is a campaign planning tool that allows for the design and automation of responsive multi-channel campaigns that can be used to help guide customers through each step of their journey with the brand. The Salesforce Marketing Cloud Journey Builder user interface enables teams to easy understand how customer journey campaigns are executed. With this ease of use comes the ability for teams to apply an iterative design process where all parts of the campaign are tested. Gone is the campaign code only understood by programmers.

##Journey Builder Customer Scenarios

A campaigns in Journey Builder is described as an interaction. Journey Builder interactions are used to help manage the touch points that a customer has with a brand. To determine a customer touch points consider the sales funnel that a customer works through whilst purchasing.

###1 - Welcome and Nurturing Customer Journeys

Generally this is where the customer is working through recognition of problem, information search and evaluation of alternative products of the sales process. At this time the marketer will want to welcome the customer and differentiate their product. To enable this the marketer will develop a single view of the customer containing preference, segment and behavioral data that is used to communicate personalised and relevant information. The **welcome journey** represents a starting point in the relationship that the marketer will have with the customer. At this stage the customer will have signaled the marketer that they are interested in more information. The customer generally starts the welcome process by joining a membership program, completing a form or causing an update to a record in a CRM. After the customer has been welcomed **lead nurturing journeys** can be conducted to learn more about the customer and to help the customer move onto the purchasing stage.

###2 - Purchase and Offer Customer Journeys

At this point the marketer will want to help the customer make a purchasing decision. If the customer fails to complete the purchase then the marketer can direct the customer back to the lead nurturing customer journey. Offers can be included in content with welcome and lead nurturing customer journeys. Separate seasonal offers can be made to customer using journeys based on customer understandings.

###3 - Post-purchase Customer Journeys

Post-purchase Customer Journeys provides the marketer with opportunities to help the customer to make a repeat purchases.

##Steps to the set-up of a Salesforce Marketing Cloud Journey Builder Interaction

Before starting a Journey Builder interaction data must first be integrated into the Salesforce Marketing Cloud platform. Integration occurs when data is feed into a data extension. This can occur via the import activity, API or Salesforce connector. Contact builder is used to expose data for use with journey builder trigger events. Journey Builder then exposes activities available in the Salesforce Marketing Cloud.

1. **First define a campaign goal** - defining goals is important because they help to communicate campaign objectives and share progress.

2. **Next trigger an event to start the customer journey interaction** - this is done by configuring the interaction to listen for an event. Events include changes to data, date schedules and API requests.

3. **Configure the flow of activities** - in Journey Builder activities are described as a flow of send, wait, data update and custom activities. All decisions are  managed by rules that control how the contact progresses through the journey interaction.

##Journey Builder and Automation Studio Feature Comparison

Both Journey Builder and Automation Studio are campaign automation tools and as such have similarities which allow for the scheduling of activities to communicate with the customer. The main difference is that Journey Builder is a tool that works directly with the contact, whereas Automation Studio is designed to trigger processes that are batched against a collection of records. The following table provides a summary of differences between Journey Builder and Automation Studio.

|  | Journey Builder | Automation Studio |
| -------- | --------------- | ----------------- |
| Built in goal reporting | Yes | No |
| GUI includes: | Configuration and scheduling of activities and contact decision flow logic. | Configuration and scheduling of activities only. |  
| Processing method used to decision activities | In Journey Builder activities and decisions are applied at an individual contact level using the GUI. To decision if an activity should be performed a decision split is used and configured with an easy to use drag and drop filter method. | In Automation Studio activities are applied in a batch mode to all records. To decision if a subset of records should have an activity performed a query, filter and then send against the filter is performed. Queries and therefore filters are configured using SQL. |
| Trigger used to start processing | An event is fired at the data extension to determine if any contacts require processing activities. The fireevent is sent either from automation studio or the API. An API fire event may contain a payload of data that can be used to update the data extension used with the Journey Builder Interaction. | Automations can be triggered to start using a schedule, change of file on a watched location or API. The API used to start an Automation Studio automation is different to the one used with Journey Builder and cannot contain any payload of data.  |

##Links

> Visit [Journey Builder](https://www.salesforce.com/products/marketing-cloud/platform/digital-marketing-optimization/) for information about using Salesforce Marketing Cloud Journey Builder to create journeys across email, mobile, social, advertising and the web.

##Notes:

* A contact in the Salesforce Marketing Cloud represents a person and includes all demographic and behavioral data associated to that person.
* Where event triggers depend on calculations and/or complex relationships data can be pre-processed using a query interaction. Where queries are used data is updated into the data extension (or table) associated with the Journey Builder Interaction. Depending on the requirement Contact Builder can also be used to manage complex data requirements.
