# Firing Events

An Interaction starts when an Event is fired. The Event will be heard by a Trigger, which prompts the Interaction to begin. Contacts that meet the Contact Filter Criteria defined by the Trigger will enter into the Interaction.

Events can be fired either by using the contactEvents Fuel REST API method or by creating an Automation using Automation Studio. This document explains the steps for using both procedures.

## Configuration

Before an Event can be fired, the following tasks must be completed:

1. Setup a customer Data Extension
2. Add records to the Data Extension
3. Create an Interaction with Trigger and Events
4. Start the Interaction

In this tutorial we will create a Data Extension for customers and build a simple Interaction to update a field in the Data Extension once the Contact enters the Interaction. The steps to completed these tasks are detailed below.

## Configuring a Data Extension

A Data Extension can either be managed from within the Email app in Marketing Cloud, or from within Contact Builder. Configuring and adding records from Contact Builder provides convenience (as you don't need to open another application) but also provides additional functionality for adding and editing records in the Data Extension.

1. To create a new Data Extension, open Contact Builder from the Data & Analytics menu and select the **Data Extensions** tab. Click **Create** and enter a name for the Data Extension in the Name field. You can optionally complete the other fields in this dialog.

  ![Create New Data Extension](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/create-new-data-extension.png "Creating a new Data Extension in Contact Builder") *Creating a new Data Extension in Contact Builder*

2. Click the **Next** button twice and in the Attributes step, add the following attributes. These attributes (or Data Extension fields) are for a fictitious membership database.

  |PrimaryKey|Name|Data Type|Data Sources|Required|Length|Default Value|
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

## Creating an Attribute Group

Next we will define the relationship between a Contact Record in and the Data Extension that you have just created.

1. Select the Data Designer tab in Contact Builder to open Data Designer and click the **Create Attribute Group** button.

2. Name the Attribute Group and click **Save**.

  ![Naming Attribute Group](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/name-attribute-group.png "Naming an Attribute Group") *Naming an Attribute Group*

3. Link to the Data Extension that you created previously by selecting **Link Data Extensions**. This opens the Link Data Extension dialog. Select the Data Extension you created earlier and link 'Contact Key' to 'Email Address' then set the relationship to a Root relationship by selecting **One** from the menu next to the Data Extension name and select the 'Use as root' option, thenk click **Save**.

  ![Creating a Root Relationship](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/creating-root-relationship.png "Creating a Root Relationship for an Attribute Group") *Creating a Root Relationship for an Attribute Group*

4. You will now see the cardinal relationship that you have created between the Contact Record an the Data Extension. You can preview the link between the Contact Record and Data Extension by moving your cursor over the link icon.

  ![Attribute Group Relationship](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/attribute-group-relationship.png "Relationship of an Attribute Group in Contact Builder") *Relationship of an Attribute Group in Contact Builder*

## Creating an Interaction

Now that the Data Extension and Attribute Group has been created, we will create a new Interaction that uses the Attribute Group as the Event Source, then will update the 'Updated' attribute in the Attribute for a Contact when they move through the Interaction.

1. Open Journey Builder from the Marketing Automation menu and click the **New Interaction** button in the top right corner of the interface to open the new Interaction in the Interaction Canvas.

2. Name the Interaction by selecting the 'Untitled Interaction' field in the top left corner, add a name and click **Done**. 

  ![New Interaction](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/new-interaction.png "New Interaction in the Interaction Canvas") *New Interaction in the Interaction Canvas*

3. Create a new Trigger by clicking on **Select a Trigger...** button, click the **Create Trigger** and click **Next**.

  ![Create Trigger](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/add-interaction-trigger.png "Adding a Trigger in the Interaction Canvas") *Adding a Trigger in the Interaction Canvas*

4. Create a name for the Trigger in the **Add Name** field.

5. Click **Choose Data Extension** and select the Data Extension you created earlier.

6. Give the Trigger a name in the **Add Name** field. 

7. Select the Attribute Group from the Atrributes list and drag the 'Updated' Atrribute to the Expression Editor. Change the value to **Is False**.

  ![Configuring an Interaction Trigger](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/configuring-interaction-trigger.png "Configuring an Interaction Trigger in the Interaction Canvas") *Configuring an Interaction Trigger in the Interaction Canvas*

7. Click **Next** twice, then click **Done** to close the Interaction Trigger dialog.

8. Next we are going to add an Update Customer Data Activity so when a Contact enters the Interaction, we will immediately update the 'Updated' field in the Data Extension.

  Drag the **Update Customer Data** Activity from the Activities panel to the 'Day 0' swim lane in the Interaction Canvas, move your cursor over the Activity and click **Configure**.

9. In the Update Contact Data dialog, select the Data Extension that you created earlier and click **Next**.

10. Select the **Updated** Atrribute from the Attribute Set menu and set the value to **True**, then click **Done**.

  ![Setting Attribute Value](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/set-update-value-contact-data.png "Setting an Attribute value for an Update Customer Data Activity") *Setting an Attribute value for an Update Customer Data Activity*

18. Now we are ready to publish the Interaction. Click the **Activate** button in the version panel on the top left corner of the Interface, then click **Activate** in the Activate Interaction dialog. The Interaction will be saved and changed to a 'running' state.

## Firing an Event using Automation Studio

Now that the Attribute Group has been created and the Interaction is running, we can fire an Event to start the Interaction. We will use Automation Studio to fire an Event; when records are added to the Data Extension, Interaction Triggers that use the Data Extension as the Event Source will listen for the Event and Contacts that meet the Contact Filter Criteria will enter the Interaction.

1. To create a new Automation in Automation Studio, select **Automation Studio** from the **Marketing Automation** menu in Marketing Cloud.

2. Click the **Create Automation** button in the top right corner of the Automation Studio Interface, select the **Scheduled** type and click **Ok**.

3. Name the Automation by clicking on the 'Untitled Automation' field in the top left corner, enter a name and click **Done**.

4. Drag a **Fire Event** Activity from the Activities panel onto the Automation Canvas.

  ![Fire Event in Automation Canvas](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/automation-studio-fire-event.png "Adding a Fire Event to the Automation Canvas") *Adding a Fire Event to the Automation Canvas*

5. Click the **Choose&hellip;** button and select the Data Extension you created earlier in the Data Extensions directory, and click **Done**.

6. Save the Automation by clicking the **Save** button in the top right corner of the Automation interface.

7. Now you can fire the Event. Click the **Run Once** button (next to the Save button). The Automation task will start after a few seconds. You can view the progress from the Activity page by selecting the **Activity** tab.

  ![Review Automation Activities](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/automation-activities.png "Review Activities for an Automation in Automation Studio") *Review Activities for an Automation in Automation Studio*

8. Check that the Interaction completed by selecting the **Data Extensions** tab in Contact Builder, select the Data Extension and click on the **Records** tab. You should see that the 'Updated' value for the records has been set to True by the Update Customer Data Activity in the Interaction. It may take a few minutes for the Interaction Trigger to hear the Event, so if the fields are not updated, check again later.

  ![Updated Data Extension Records](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/updated-data-extension-records.png "Data Extension records updated in Contact Builder") *Data Extension records updated in Contact Builder*

## Firing an Event using the Fuel REST API

Next, we will use the contactEvents REST API method to add Event data to a Data Extension and fire an Interaction for a defined Interaction Trigger. 

An Event comprises of an Event Destination and a linked Data Extension. The Event Destination will be the Attribute Group that we created earlier and we will add serialized Event Data to the linked Data Extension using the contactEvents method.

In this next workflow, we will simulate the behavior when a Contact updates their preference data on an external platform, for example on a website. When this Event occurs, the Contact preference data will be serialized into a Data Extension and the Contact will enter an Interaction.

1. The first step is to define the properties for an Event. Events are created from Data Designer in Contact Builder. Open **Contact Builder** from the Data & Analytics menu and from the dropdown menu on the **Create Attribute Group** button, select **Create New Event**.

2. In the Create New Event dialog, add a unique name in the Name field, assign an event key in the Event Key field and then select the Attribute Group you created earlier. This creates a relationship between the Event and Event Destination.

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

9. When you start an Event, you will be returned back to the Data Designer interface. From the constellation view, select the Attribute Group that you previously created and... [done to here]

