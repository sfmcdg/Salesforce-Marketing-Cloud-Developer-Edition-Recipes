#Step by step guide to sending email with journey builder

In this example an email will be sent when a new record is added to the data extension.

##Setup database and relationships

**Contact builder** is used to create the **data extension**. In **contact builder** the **data extension** is linked to the **contact record**.

1. In **contact builder** create a new **attribute group**. For example use _**DemoConceptRelationships**_ as name of attribute group. 
2. Start building your **attribute group** by selecting **create new data extension**.
    1. For **data extension name** and **data extension external key** use _**DemoConceptData**_.
    2. Next then click through to **3 - data extension attributes** and create these fieds:
        1. _**EmailAddress**_ as primary key with required type **email address**. 
        2. _**Firstname**_ as required **text** (use default text length 50).
        3. _**Log**_ as not required type **text** (use default text length 50).
    3. Click through to **4 - link data extension** and join **contact key** to **EmailAddress**.
3. Click on link joining **contact record** and **data extension**, and then:
    1.  Change relationship from **many** to **one**.
    2.  Turn on **use as root**.
4. Next select **contacts configuration** from menu, and then:
    1.  Edit **email** channel.
    2.  In edit section for email channel select **add address**, then select the **EmailAddress** from the **data extension** - in example data extension will be called _**DemoDataConcept**_. When finished save changes.
5. Finally select **data extensions** from menu, then select _**DemoConceptData**_, edit behaviour, select **used for sending** and ensure that _**EmailAddress**_ relates to subscriber on _**Subscriber Key**_.

##Create interaction (program)

**Journey Builder** is used to create the **interaction** that records will be processed through.

Before starting this section setup content for email.

1.  In **journey builder** select **new interaction**. This will create a new interaction where the **trigger** and **events (or tasks)** for the journey are  described. 
2.  Give **interaction** a name. For example use _**DemoConceptInteractionWelcome**_.
3.  The trigger is used to specify the criteria for which records to use. To setup up a trigger:
    1.  Click on **select a trigger**, followed by **create trigger** and click on next.
    2.  In the **configure trigger** section:
        1.  Use _**DemoConceptInsert**_ for the name of **trigger**.
        2.  Select _**DemoConceptData**_ for`attributes.
        3.  Drag and drop _**DemoConceptData.Log**_ into the section for **creating the expression that defines this contact data trigger**. The criteria for **Log** is **IsNull**. The reason for this will become apparent later when we setup **events**. In summary ` .Log = IsNull` is the test that will be used to check if email has already been sent.
        4.  For **event source** select **choose data extension**. In example data extension is _**DemoConceptData**_.
    3. In the **timeline** section drag and drop events for **journey**. _Hint - at this point consider changing flow view to points instead of timeline._
       1.  Use **update contact data** and configure to set attribute  _**DemoConceptData.Log**_ equal to _**WELCOMED**_. This is set so that when **interaction** is run previously inserted records do not receive welcome email.
       2.  Drag and drop **send email** and configure. 
       3.  Change any timers to _**wait 1 minute**_.
       4.  Save and activate. When an **interaction** is activiate it means that it is available to be run.

##Add some data to the database

Next add some data to the _**DemoConceptData**_ **data extension**.

1. In **contact builder** select, view and edit the _**DemoConceptRelationships**_ attribute group.
2. Select **data extensions** from the menu, for example select the _**DemoConceptData**_ data extension, then click on the **records** tab, then select **add records**.
3. Populate only **EmailAddress** , **Name** fields and then **save**.

##Run the interaction (program)

Next use **automation strudio** to run the **interaction** against the **data extension** that was created earlier.

1. In **automation studio** create a **scheduled automation**.
2. Drag and drop **fire event** onto the timeline.
3. Configure **fire event** to use data extension. In example this would be _**DemoConceptData**_.
4. Use **_DemoConceptInteractionWelcomeRun**_ as **name** of automation and save
5. Select **run once** to run automation and wait a couple of moments. Select **activity** to monitor progress. _Hint - screen will not automaticly fresh - use **refresh** button to update progress._
6. What will happen next is that any interactions linked via trigger to data extension will run. To monitor progress:
    1. View records in **data extension** where **log** field should be populated with word _**WELCOMED**_.
    2. View control panel on **journey builder** where number of records in interaction should have increased.
    3. View **trigger emails** in matching **journey builder sends** for interaction. In example this would be _**Journey Builder Sends > DemoConceptInteractionWelcome > Version 1**_ where **status** should be **running** and **completed**, **queued** and/or **errored** should have values.
    4. Also check to see if recipient received email.
    5. To test that only new records receive email repeat **adding data to database** and **running the program**. 

