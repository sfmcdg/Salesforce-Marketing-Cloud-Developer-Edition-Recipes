# Firing Events

## Contents
* [Introduction](#Introduction)
* [Configuration](#Configuration)
  * [Configuring a Data Extension](#Configuring-a-Data-Extension)
  * [Creating an Attribute Group](#Creating-an-Attribute Group)
  * [Creating an Interaction](#Creating-an-Interaction)
* [Firing an Event using Automation Studio](#Firing-an-Event-using-Automation-Studio)
* [Firing an Event using the Fuel REST API](#Firing-an-Event-using-the-Fuel-REST-API)
  * [Add Event data for existing Contact and fire an Interaction](#Add-Event-data-for-existing-Contact-and-fire-Interaction)
  * [Add Event data, create new Contact and fire an Interaction](#Add-Event-data-create-new-Contact-and-fire-Interaction)
  * [Add new Contact and fire an Interaction](#Add-new-Contact-and-fire-Interaction)
* [Further Information](#Further-Information)

## Introduction<a id="Introduction"></a>

An Interaction starts when an Event is fired. The Event will be heard by a Trigger, which prompts the Interaction to begin. Contacts that meet the Contact Filter Criteria defined by the Trigger will enter into the Interaction.

Events can be fired either by using the contactEvents Fuel REST API method or by creating an Automation using Automation Studio. This document explains the steps for using both procedures.

## Configuration<a id="Configuration"></a>

Before an Event can be fired, the following tasks must be completed:

1. Setup a customer Data Extension
2. Add records to the Data Extension
3. Create an Interaction with Trigger and Events
4. Start the Interaction

In this tutorial we will create a Data Extension for customers and build a simple Interaction to update a field in the Data Extension once the Contact enters the Interaction. The steps to completed these tasks are detailed below.

### Configuring a Data Extension<a id="Configuring-a-Data-Extension"></a>

A Data Extension can either be managed from within the Email app in Marketing Cloud, or from within Contact Builder. Configuring and adding records from Contact Builder provides convenience (as you don't need to open another application) but also provides additional functionality for adding and editing records in the Data Extension.

1. To create a new Data Extension, open Contact Builder from the Data & Analytics menu and select the **Data Extensions** tab. Click **Create** and enter a name for the Data Extension in the Name field. You can optionally complete the other fields in this dialog.

  ![Create New Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/create-new-data-extension.png "Creating a new Data Extension in Contact Builder") *Creating a new Data Extension in Contact Builder*

2. Click the **Next** button twice and in the Attributes step, add the following attributes. These attributes (or Data Extension fields) are for a fictitious membership database.

  |Primary Key|Name|Data Type|Data Sources|Required|Length|Default Value|
  |----|----|----|----|----|----|----|
  |Yes|EmailAddress|Email Address|Unassigned|Yes|254||
  ||MemberID|Number|Unassigned||||
  ||FirstName|Text|Unassigned||50||
  ||LastName|Text|Unassigned||50||
  ||Updated|Boolean|Unassigned|||False|

  ![Adding Attributes to a Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/adding-attributes.png "Adding Attributes to a Data Extension in Contact Builder") *Adding Attributes to a Data Extension in Contact Builder*

3. When you have completed all fields, click **Next** and **OK** to return to the Data Extensions interface. Now add records to the Data Extension by clicking on the Data Extension name and click on the Records tab. Use the **Add Record** button to insert a record into the Data Extension. Complete all fields, leaving the Updated field set to 'False'. Repeat this step to add additional records to the Data Extension.

  ![Adding records to a Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/adding-records-to-data-extension.png "Adding records to a Data Extension in Contact Builder") *Adding records to a Data Extension in Contact Builder*

4. Finally we need to change the Data Extension Type to 'Sendable', as Data Extensions need to be 'Sendable' in order to be used as an Event Source in an Interaction Trigger. Select the **Properties** tab and under the Type selection click the **Edit** button. Click the 'Used For Sending' option, ensure that the 'EmailAddress' field is set to relate to the subscriber on 'Subscriber Key' and click **Save**.

  ![Updating a Data Extension Type](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/edit-data-extension-type.png "Updating a Data Extension Type in Contact Builder") *Updating a Data Extension Type in Contact Builder*

### Creating an Attribute Group<a id="Creating-an-Attribute Group"></a>

Next we will define the relationship between a Contact Record in and the Data Extension that you have just created.

1. Select the Data Designer tab in Contact Builder to open Data Designer and click the **Create Attribute Group** button.

2. Name the Attribute Group and click **Save**.

  ![Naming Attribute Group](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/name-attribute-group.png "Naming an Attribute Group") *Naming an Attribute Group*

3. Link to the Data Extension that you created previously by selecting **Link Data Extensions**. This opens the Link Data Extension dialog. Select the Data Extension you created earlier and link 'Contact Key' to 'Email Address' then set the relationship to a Root relationship by selecting **One** from the menu next to the Data Extension name and select the 'Use as root' option, thenk click **Save**.

  ![Creating a Root Relationship](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/creating-root-relationship.png "Creating a Root Relationship for an Attribute Group") *Creating a Root Relationship for an Attribute Group*

4. You will now see the cardinal relationship that you have created between the Contact Record an the Data Extension. You can preview the link between the Contact Record and Data Extension by moving your cursor over the link icon.

  ![Attribute Group Relationship](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/attribute-group-relationship.png "Relationship of an Attribute Group in Contact Builder") *Relationship of an Attribute Group in Contact Builder*

### Creating an Interaction<a id="Creating-an-Interaction"></a>

Now that the Data Extension and Attribute Group has been created, we will create a new Interaction that uses the Attribute Group as the Event Source, then will update the 'Updated' attribute in the Attribute for a Contact when they move through the Interaction.

1. Open Journey Builder from the Marketing Automation menu and click the **New Interaction** button in the top right corner of the interface to open the new Interaction in the Interaction Canvas.

2. Name the Interaction by selecting the 'Untitled Interaction' field in the top left corner, add a name and click **Done**. 

  ![New Interaction](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/new-interaction.png "New Interaction in the Interaction Canvas") *New Interaction in the Interaction Canvas*

3. Create a new Trigger by clicking on the **Select a Trigger&hellip;** button, click the **Create Trigger** panel and click **Next**.

  ![Create Trigger](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/add-interaction-trigger.png "Adding a Trigger in the Interaction Canvas") *Adding a Trigger in the Interaction Canvas*

4. Create a name for the Trigger in the **Add Name** field.

5. Click the **Choose Data Extension** button and select the Data Extension you created earlier.

6. Give the Trigger a name in the **Add Name** field. 

7. Select the Attribute Group from the Atrributes list and drag the 'Updated' Atrribute to the Expression Editor. Change the expression value to **Is False**.

  ![Configuring an Interaction Trigger](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/configuring-interaction-trigger.png "Configuring an Interaction Trigger in the Interaction Canvas") *Configuring an Interaction Trigger in the Interaction Canvas*

7. Click **Next** twice, then click **Done** to close the Interaction Trigger dialog.

8. Next we are going to add an Update Customer Data Activity so when a Contact enters the Interaction, we will immediately update the 'Updated' field in the Data Extension.

  Drag the **Update Customer Data** Activity from the Activities panel to the 'Day 0' swim lane in the Interaction Canvas, move your cursor over the Activity and click **Configure**.

9. In the Update Contact Data dialog, select the Data Extension that you created earlier and click **Next**.

10. Select the **Updated** Atrribute from the Attribute Set menu and set the value to **True**, then click **Done**.

  ![Setting Attribute Value](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/set-update-value-contact-data.png "Setting an Attribute value for an Update Customer Data Activity") *Setting an Attribute value for an Update Customer Data Activity*

18. Now we are ready to publish the Interaction. Click the **Activate** button in the version panel on the top left corner of the Interface, then click **Activate** in the Activate Interaction dialog. The Interaction will be saved and changed to a 'running' state.

## Firing an Event using Automation Studio<a id="Firing-an-Event-using-Automation-Studio"></a>

Now that the Attribute Group has been created and the Interaction is running, we can fire an Event to start the Interaction. We will use Automation Studio to fire an Event; when records are added to the Data Extension, Interaction Triggers that use the Data Extension as the Event Source will listen for the Event and Contacts that meet the Contact Filter Criteria will enter the Interaction.

1. To create a new Automation in Automation Studio, select **Automation Studio** from the Marketing Automation menu in Marketing Cloud.

2. Click the **Create Automation** button in the top right corner of the Automation Studio Interface, select the **Scheduled** type and click **Ok**.

3. Name the Automation by clicking on the 'Untitled Automation' field in the top left corner, enter a name and click **Done**.

4. Drag a **Fire Event** Activity from the Activities panel onto the Automation Canvas.

  ![Fire Event in Automation Canvas](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/automation-studio-fire-event.png "Adding a Fire Event to the Automation Canvas") *Adding a Fire Event to the Automation Canvas*

5. Click the **Choose&hellip;** button and select the Data Extension you created earlier in the Data Extensions directory, and click **Done**.

6. Save the Automation by clicking the **Save** button in the top right corner of the Automation interface.

7. Now you can fire the Event. Click the **Run Once** button (next to the Save button). The Automation task will start after a few seconds. You can view the progress from the Activity page by selecting the **Activity** tab.

  ![Review Automation Activities](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/automation-activities.png "Review Activities for an Automation in Automation Studio") *Review Activities for an Automation in Automation Studio*

8. Check that the Interaction completed by selecting the **Data Extensions** tab in Contact Builder, select the Data Extension and click on the **Records** tab. You should see that the 'Updated' value for the records has been set to 'True' by the Update Customer Data Activity in the Interaction. It may take a few minutes for the Interaction Trigger to hear the Event, so if the fields are not updated, check again later.

  ![Updated Data Extension Records](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/updated-data-extension-records.png "Data Extension records updated in Contact Builder") *Data Extension records updated in Contact Builder*

## Firing an Event using the Fuel REST API<a id="Firing-an-Event-using-the-Fuel-REST-API"></a>

Next, we will use the contactEvents REST API method to add Event data to a Data Extension and fire an Interaction for a defined Interaction Trigger. 

There are three different scenarios for using this API method:

* Add Event data for existing Contact and fire an Interaction
* Add Event data, create new Contact and fire an Interaction
* Add new Contact and fire an Interaction

The steps to complete each of these scenarios is detailed below.

### Add Event data for existing Contact and fire an Interaction<a id="Add-Event-data-for-existing-Contact-and-fire-Interaction"></a>

An Event comprises of an Event Destination and a linked Data Extension. The Event Destination will be the Attribute Group that we created earlier and we will add serialized Event Data to the linked Data Extension using the contactEvents method.

In this next workflow, we will simulate the behavior when an existing Contact updates their preference data on an external platform, for example on a website. When this Event occurs, the Contact preference data will be serialized into a Data Extension and the Contact will enter an Interaction.

1. The first step is to define the properties for an Event. Events are created from Data Designer in Contact Builder. Open **Contact Builder** from the Data & Analytics menu and from the dropdown menu on the **Create Attribute Group** button, select **Create New Event**.

2. In the Create New Event dialog, add a unique name in the Name field, assign an event key in the Event Key field and then select the Attribute Group you created earlier. This creates a relationship between the Event and Event Destination. Make a note of the event key as this will be used later in the contactEvents method.

  ![Create New Event](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/create-new-event.png "Creating a new Event in Contact Builder") *Creating a new Event in Contact Builder*

3. Click **Create** and the Event will be displayed in the Interface. Next we need to create a new Data Extension to contain the serialized Event Data. Click on the **Create New Data Extension** button. This is the preferred method rather than linking to an exisiting Data Extension, as the Data Extension needs to contain additional fields and these are automatically added to the Data Extension when a new Data Extension is created from the Events interface.

4. In the Create New Data Extension dialog, assign a name to the Data Extension. You can optionally complete the additional fields in this step and change the location of the Data Extension. 

  ![Create New Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/new-data-extension-for-event.png "Creating a new Data Extension for an Event in Contact Builder") *Creating a new Data Extension for an Event in Contact Builder*

5. Click **Next** twice and add an Attribute (or Attributes) to store the member preference data. You will note that three required Attributes have automatically been added to the Data Extension.

  ![Adding Attributes to an Event Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/adding-attributes-for-event.png "Creating Attributes for an Event in Contact Builder") *Creating Attributes for an Event in Contact Builder*

6. Click **Next** and create the relationship between the Contact record and the new Data Extension. In this instance, we will link the two **Contact Key** system generated Attributes.

  ![Creating Event Relationships](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/event-attribute-relationship.png "Creating relationships for an Event in Contact Builder") *Creating relationships for an Event in Contact Builder*

7. Click **Create** and click **OK** in the confirmation dialog. You will now see the relationship between the Contact Record and the linked Data Extension where the Event data will be serialized. 

  ![Event Data Relationships](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/data-relationship-for-event.png "Data relationship for an Event in Contact Builder") *Data relationship for an Event in Contact Builder*

8. You can now start the Event by selecting the **Start Event** button in the top right corner of the interface. Click **Start** in the confirmation dialog.

9. When you start an Event, you will be returned back to the Data Designer interface. From the constellation view, select the Attribute Group that you previously created and click the **View & Edit** button then click **OK** if prompted to confirm changes. You will see that the relationship from the Contact Record has been updated to include the linked Data Extension used by the Event.

  ![Event Data Relationship in an Attribute Group](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/event-data-relationship-in-attribute-group.png "Data relationship of an Event in an Attribute Group") *Data relationship of an Event in an Attribute Group*

10. Before we can fire the Event, we need to add a new record to the Event Destination, as the existing Contacts have already entered the Interaction and will no longer meet the Contact Filter Criteria defined in the Interaction Trigger. Select the **Data Extensions** tab in Contact Builder and then select the first Data Extension you created that is used in the Attribute Group.

11. Click the **Add Record** button and complete the fields. You will note that an eventinstanceid field has automatically been added to the Data Extension. This is used internally, you do not need to add a value to this new field. When you have added a new record click the **Save** button.

  ![Adding a new record](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/adding-new-record-to-data-extension.png "Adding a new record to a Data Extension in Contact Builder") *Adding a new record to a Data Extension in Contact Builder*

12. Now we are almost ready to simulate posting data from an Event for this new record using the contactEvents method from the Fuel REST API. The Event data will be serialized into the linked Data Extension associated with the Contact and the Contact will enter the Interaction. 

   While in the Data Extensions interface, locate the Data Extension that you will serialize the Event data into by opening the Data Extension that you created for the Event data. Copy the External Key, and paste it into a text file for later use.

  ![Copy Data Extension External Key](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/copy-external-key-data-extension.png "Locating the External Key for a Data Extension") *Locating the External Key for a Data Extension*

13. Before we can make the API request, you will need to create an app in App Center with the required permissions (or edit an existing app to include the permissions). Login to App Center at http://appcenter.exacttarget.com and click the **Create New App** button in the top right corner of the page.

14. Click the **API Integration** template.

15. Complete the Name and Package fields

  ![Defining App Properties](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-define.png "Defining app properties in App Center") *Defining app properties in App Center*

16. Click **Next** and select a Marketing Cloud user account that the app will use when making API requests. Unless you have purchased a separate Sandbox Account license, select the Production Account option. The 'Link to Account' button opens a new window for defining Marketing Cloud account credentials. If you have previously created an Account reference, you can select it from the Account menu. 

17. Click **Next** and add the permissions required to use the app. You will need to enable the following permissions:

  |Operation|Functional Area|Feature|Permissions|
  |----|----|----|----|
  |Data|Data Management|Data Extensions|Read, Write|
  |Automation|Marketing Automation|Interactions|Execute, Read, Write|

  ![Defining App Properties](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-define.png "Defining app properties in App Center") *Defining app properties in App Center*

18. Click **Next** to display the Summary page and **Finish** to save the app. Copy the OAuth Client ID and Client Secret on this page and paste into a text file.

  ![Details of an app in App Center](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-details-tutorial.png "Details of an app in App Center") *Details of an app in App Center*

19. Now you can obtain an OAuth token to use in the contactEvents method. Perform a HTTP POST request specifying your client ID and client secret for the app (obtained from App Center) in the payload. An example request is provided below.

  ```
  POST https://auth.exacttargetapis.com/v1/requestToken
  Content-Type: application/json
  {
    "clientId": "gyjzvytv7ukqtfn3x2qdyfsn",
    "clientSecret": "SJbAEenSK2SVBK4d4vBV6NKT"
  }
  ```

  This HTTP POST request returns an `accessToken` which is the OAuth token used for subsequent API requests and an `expiresIn` value indicating the expiration period of the OAuth token in seconds. An example response is provided below.

  ```
  {
    "accessToken": "4ae36paatp4mnwkhanyhajp4",
    "expiresIn": 3600
  }
  ```

20. We will now use the contactEvents API method to serialize the Event data into the Data Extension linked to the Event and fire an Interaction using the Trigger `eventDefinitionKey`.

  This method uses the following key value pairs:

  |Key|Value|
  |----|----|
  |`contactKey`|The Contact Key for the Contact Record (that was created in the Attribute Group relationship)|
  |`contactID`|The Contact ID for the Contact Record (if it was created in the Attribute Group relationship)|
  |`eventDefinitionKey`|String value identifying the Event key, used to map Event data to the linked Data Extension.|
  |`data`|Any related data associated with the event. This data must include the following values:<br />* `key`: The data extension used to receive the data.<br />* `name`: A human-readable identifier for the Data Extension used to receive the data.<br />* `id`: The External Key of the Data Extension used to receive the data.<br />* `items`: Name/value pairs containing information associated with the event|

  Use the `accessToken` value obtained from the Fuel Authentication Service as an Authorization Bearer parameter in the request header below.

  The `eventDefinitionKey` value is the Event key you added in step 2.

  The `ContactKey` value will be the ContactKey of the new record we created in the Event Destination Data Extension earlier.

  The Data Extension used to receive the data is the linked Data Extension for the Event. Add the Data Extension name as the `name` value, external key as `id` value and create a unique `key` value. An example request is provided below.

  ```
  HOST: https://www.exacttargetapis.com
  POST /contacts/v1/contactEvents
  Content-Type: application/json
  Authorization: Bearer insert-accessToken-here

  {
      "contactKey": "susan@sausage.com",
      "eventDefinitionKey": "update-preferences",
      "data": [{
          "key": "MemberPreferences",
          "name": "Member Preferences",
          "id": "6160D1B6-54CB-4CD6-BE17-F5BBD496919A",
          "items": [{
              "values": [{
                  "name": "FavoriteSausage",
                  "value": "frankfurter"
              }]
          }]
      }]
  }
  ```

This request returns the following response

  ```
  {
      insert here once I get this method to actually work
  }
  ```

21. The Event data will be added to the Data Extension linked to the Event and the Contact will enter the Interaction. You can confirm that the Interaction completed by selecting the **Data Extensions** tab in Contact Builder, select the Data Extension and click on the **Records** tab. You should see that the 'Updated' value for the new record has been set to True by the Update Customer Data Activity in the Interaction. Also, the serialized event data should appear in the Data Extension linked to the Event.

### Add Event data, create new Contact and fire an Interaction<a id="Add-Event-data-create-new-Contact-and-fire-Interaction"></a>

Assuming you have already created an Event as detailed in the previous section, the contactEvents method is similar, but this time we are adding records to two Data Extensions; the Data Extension linked to the Event and the Data Extension used as the Event Destination. The additional steps required are detailed below.

1. Locate the External Key of the Data Extension used as the Event Destination &mdash; this is the Data Extension you created in the Configuring a Data Extension section. Select the **Data Extensions** tab in Contact Builder, select the Data Extension and copy the External Key.

2. Create a new data object for the Event Destination Data Extension in the `data` array using the Data Extension name as the `name` value, external key as `id` value and create a unique `key` value. 

  As the Contact does not already exist, the `contactKey` should need to be included in the payload, but you will need to include a matching `ContactKey` name/value pair for the Event data object for it to relate to the Event Destination.

  An example request is provided below.

  ```
  HOST: https://www.exacttargetapis.com
  POST /contacts/v1/contactEvents
  Content-Type: application/json
  Authorization: Bearer insert-accessToken-here

  {
      "eventDefinitionKey": "update-preferences",
      "data": [{
          "key": "MemberPreferences",
          "name": "Member Preferences",
          "id": "6160D1B6-54CB-4CD6-BE17-F5BBD496919A",
          "items": [{
              "values": [{
                  "name": "FavoriteSausage",
                  "value": "frankfurter"
                  },
                  {
                  "name": "ContactKey",
                  "value": "sam@sausage.com"
                  }]
              }]
          },
          {
          "key": "SausageClubMembers",
          "name": "Sausage Club Members",
          "id": "872B2E1B-0368-4457-895F-986EC1A859BC",
          "items": [{
              "values": [{
                  "name": "EmailAddress",
                  "value": "sam@sausage.com"
                  },
                  {
                  "name": "MemberID",
                  "value": 5
                  },
                  {
                  "name": "FirstName",
                  "value": "Sam"
                  },
                  {
                  "name": "LastName",
                  "value": "Sample"
                  }]
          }]
     }]
  }
  ```

This request returns the following response

  ```
  {
      insert here once I get this method to actually work
  }
  ```

3. The Event data will be added to the Data Extension linked to the Event, the Contact will be added to the Event Destination and the Contact will enter the Interaction. You can confirm that the Interaction completed by selecting the **Data Extensions** tab in Contact Builder, select the Data Extension and click on the **Records** tab. You should see that the new record has been inserted into the Data Extension and the 'Updated' value for the new record has been set to True by the Update Customer Data Activity in the Interaction. Also, the serialized event data should appear in the Data Extension linked to the Event.

## Add new Contact and fire an Interaction<a id="Add-new-Contact-and-fire-Interaction"></a>

In this third scenario, we will not add Event data, but instead include add a record to the Event Destination Data Extension and fire the Interaction. 

1. Using the ContactEvents method from the previous request, omit the data object used for the data Event. An example request is provided below.

  ```
  HOST: https://www.exacttargetapis.com
  POST /contacts/v1/contactEvents
  Content-Type: application/json
  Authorization: Bearer insert-accessToken-here

  {
  {
      "eventDefinitionKey": "update-preferences",
      "data": [{
          "key": "SausageClubMembers",
          "name": "Sausage Club Members",
          "id": "872B2E1B-0368-4457-895F-986EC1A859BC",
          "items": [{
              "values": [{
                  "name": "EmailAddress",
                  "value": "saskia@sausage.com"
                  },
                  {
                  "name": "MemberID",
                  "value": 6
                  },
                  {
                  "name": "FirstName",
                  "value": "Saskia"
                  },
                  {
                  "name": "LastName",
                  "value": "Sausage"
                  }]
          }]
     }]
  }
  ```

This request returns the following response

  ```
  {
      insert here once I get this method to actually work
  }
  ```

2. The Contact will be added to the Event Destination and the Contact will enter the Interaction. You can confirm that the Interaction completed by selecting the **Data Extensions** tab in Contact Builder, select the Data Extension and click on the **Records** tab. You should see that the new record has been inserted into the Data Extension and the 'Updated' value for the new record has been set to True by the Update Customer Data Activity in the Interaction.

## Further Information<a id="Further-Information"></a>

For more information on Journey Builder development, refer to:

* [Journey Builder Developer's Guide](https://jbdevelopers.guide)
* [Journey Builder Development on @code](https://code.exacttarget.com/app-development/journey-builder-development/)