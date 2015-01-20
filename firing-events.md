# Firing Events

This document provides a step-by-step guide for creating an Event that is used to start an Interaction.

## Workflow

When a customer updates their details in an external system, the `contactEvent` Fuel REST API menthod is used to serialize the event data into a linked Data Extension. A relationship exists between the linked Data Extension and a Customer Data Extension that is used by a Trigger in an Interaction. The Trigger listens for this event and the Contact enters the Interaction (assuming that the Contact Filter Criteria is met). This workflow is summarized in the diagram below.

![Firing Event Workflow](img/fire-event-flow.png "Firing Event Workflow")

## Steps

The following steps detail the procedure for creating and starting the workflow.

1. Create a new Sendable Data Extension in the Email App with the following fields:

  |Field|Type|Length|PrimaryKey|Nullable|Default Value|
  |----|----|----|----|----|----|
  |MemberID|Number||Yes|||
  |FirstName|Text|50||Yes||
  |LastName|Text|50||Yes||
  |EmailAddress|Text|50||Yes||
  |Updated|Boolean|||Yes|False|

Send Relationship 'MemberID' relates to Subscribers on 'Subscriber Key'

  ![Customer Data Extension](img/customer-data-extension.png "Customer Data Extension")

Make a note of the External Key before moving onto the next step.

2. Open Contact Builder and Create a New Attribute Group

3. Link to Data Extension you created in Step 1, creating a Root Relationship with Contact ID linking to MemberID

 ![Link Data Extension](img/link-data-extension.png "Link Data Extension")

4. Create a New Event with a unique Name and Event Key, then select the Attribute Group from Step 2 as the Event Destination.

 ![Create New Event](img/create-new-event.png "Create New Event")

5. Create a Data Extension for the Event Data by selecting 'Create New Data Extension' **while still in the Event** (this is important, as it will automatically create additional required fields).

6. Give the Data Extension a name and External Key

7. Skip past the Data Retention Policy

8. In the Attributes section add the additonal field or fields that you want to add for the Contact when posting the Event Data.

 ![New Data Extension Attributes](img/new-data-extension-attributes.png "New Data Extension Attributes")

9. In the Link Data Extension Section, select the Data Extension from Step 1 from Root Data Section and link MemberID to ContactKey

 ![Link Data Extension](img/link-data-extension-from-event.png "Link Data Extension")

10. Click Create

11. Click Start Event button in the top right corner of the page.

12. Open the Attribute Group from step 2 and you will note that the Attribute Set (or Data Extension) selected from Step 9 has been added as a one-to-many relationship.

 ![Attribute Group Relationship](img/attribute-group-relationship.png "Attribute Group Relationship")

13. Open Journey Builder and create a new Interaction

14. Select a Trigger then select Create Trigger

15. Create an Expression using the 'Updated' attribute and set the condition to 'Is False'\

  ![Configure Trigger](img/configure-trigger.png "Configure Trigger")

16. Choose the Data Extension from Step 1 as the Event Source

17. Give the Trigger a unique name

18. Click Next twice, then click Done

19. Drag Update Contact Data Activity into the 'Immediately' swim lane in the Interaction Canvas

20. Select the Activity and click Configure

21. Select the Data Extension from Step 1 and click Next

22. Set the Updated Attribute to True and click Done

 ![Set Attribute](img/set-attribute.png "Set Attribute")

23. Save the Interaction

24. Activate the Interaction

25. Now we are ready to populate the Data Extension from Step 1 with a record. You will need to use the `requestToken` Fuel Autentication Service method to retrieve an `accessToken` (using the `clientId` and `clientSecret` values from the App you created in AppCenter).

26. Make the following request with the `accessToken` from the previous step and the External Key from the Data Extension you created in Step 1, and use it in the SOAP request envelope below. Save this envelope in a file named 'request.xml' 

  ```
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing" xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
     <soap:Header>
          <fueloauth xmlns="http://exacttarget.com">insert-access-token-here</fueloauth>
     </soap:Header>
     <soap:Body>
        <CreateRequest xmlns="http://exacttarget.com/wsdl/partnerAPI">
        <Options/>
        <Objects xsi:type="DataExtensionObject">
           <CustomerKey>441594C9-78A9-4226-811C-68B474766FC6</CustomerKey>
           <Properties>
              <Property>
                 <Name>MemberID</Name>
                 <Value>1</Value>
              </Property>
              <Property>
                 <Name>FirstName</Name>
                 <Value>Sam</Value>
              </Property>
              <Property>
                 <Name>LastName</Name>
                 <Value>Sample</Value>
              </Property>
              <Property>
                 <Name>EmailAddress</Name>
                 <Value>sam@sample.com</Value>
              </Property>
           </Properties>
        </Objects>
     </CreateRequest>
    </soap:Body> 
  </soap:Envelope>
  ```

27. Make the SOAP request from the previous step using the following cURL command. You may need to update the endpoint to reference the endpoint used by your Marketing Cloud Account (which can be retrieved from the URL in Marketing Cloud).

  ```
  curl -XPOST -H "Content-type: text/xml; charset=utf-8" -H "SOAPAction: Create" -d @request.xml https://webservice.s7.exacttarget.com/Service.asmx
  ```

  You should receive the following response:

  ```
  <?xml version="1.0" encoding="utf-8"?>
  <soap:Envelope
      xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
      xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
      xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
      <soap:Header>
          <wsa:Action>CreateResponse</wsa:Action>
          <wsa:MessageID>urn:uuid:3d9d91af-0bd6-44f8-8562-dbefb730de4e</wsa:MessageID>
          <wsa:RelatesTo>urn:uuid:51aa910f-ff61-442e-a8e0-2015db9440cb</wsa:RelatesTo>
          <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
          <wsse:Security>
              <wsu:Timestamp wsu:Id="Timestamp-1fccc3d8-8a4e-42e8-a01e-e1381cf18d11">
                  <wsu:Created>2015-01-20T19:07:46Z</wsu:Created>
                  <wsu:Expires>2015-01-20T19:12:46Z</wsu:Expires>
              </wsu:Timestamp>
          </wsse:Security>
      </soap:Header>
      <soap:Body>
          <CreateResponse
              xmlns="http://exacttarget.com/wsdl/partnerAPI">
              <Results xsi:type="DataExtensionCreateResult">
                  <StatusCode>OK</StatusCode>
                  <StatusMessage>Created DataExtensionObject</StatusMessage>
                  <OrdinalID>0</OrdinalID>
                  <NewID>0</NewID>
                  <Object xsi:type="DataExtensionObject">
                      <PartnerKey xsi:nil="true" />
                      <ObjectID xsi:nil="true" />
                      <CustomerKey>441594C9-78A9-4226-811C-68B474766FC6</CustomerKey>
                      <Properties>
                          <Property>
                              <Name>MemberID</Name>
                              <Value>1</Value>
                          </Property>
                          <Property>
                              <Name>FirstName</Name>
                              <Value>Sam</Value>
                          </Property>
                          <Property>
                              <Name>LastName</Name>
                              <Value>Sample</Value>
                          </Property>
                          <Property>
                              <Name>EmailAddress</Name>
                              <Value>sam@sample.com</Value>
                          </Property>
                      </Properties>
                  </Object>
              </Results>
              <RequestID>b2a52bcd-2a3f-4518-9cd8-3d3ea0e3e356</RequestID>
              <OverallStatus>OK</OverallStatus>
          </CreateResponse>
      </soap:Body>
  </soap:Envelope>
  ```

  If you view the Data Extension in the Email app, you will see that the record now appears.

28. We are now ready to fire the Event. This will create a new record in the Events Data Extension from step 5 which is linked to the Customer Data Extension, and in turn the Contact will enter the Interaction. Using the same `accessToken` make the following REST API request:

  ```
  HOST: https://www.exacttargetapis.com
  POST /https://www.exacttargetapis.com/contacts/v1/contactEvents
  Content-Type: application/json
  Authorization: Bearer insert-access-token-here

  {
      "contactKey": "1",
      "eventDefinitionKey": "member-update",
      "data": [{
          "key": "sausageClubPreferences",
          "name": "Sausage Club Preferences",
          "id": "sausage-club-preferences",
          "items": [{
              "values": [{
                  "name": "FavoriteSausage",
                  "value": "Frankfurter"
              }]
          }]
      }]
  }
  ```