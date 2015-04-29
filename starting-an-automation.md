# Starting an Automation

This document describes how to Start an Automation (in Automation Studio) using the Fuel SOAP API. This is equivalent to using the 'Run Once' button in Automation Studio to start an Automation.

This is a two step process. Please refer to the procedural information provided below.

## Request

The example SOAP envelopes below can be tested by saving as a 'request.xml' file and  using [cURL](http://curl.haxx.se/) to make the request. Here is a sample request:

    curl -XPOST -H "Content-type: text/xml; charset=utf-8" -H "SOAPAction: Retrieve" -d @request.xml https://webservice.s7.exacttarget.com/Service.asmx

You will need to change the following:

1. Update the SOAP Action verb to reflect the action that you are using (the required actions are indicated in **bold** below)
2. Update the SOAP Endpoint URL to the [respective endpoint](http://help.exacttarget.com/en/technical_library/web_service_guide/getting_started_developers_and_the_exacttarget_api/#section_7) used with your account.

## Authentication

The SOAP request envelopes provided in the below examples use legacy username/password authentication for convenience (note that the user will need to be an API User in the account). It is suggested that you consider using App Center to [create an App and generate an OAuth ClientID and ClientSecret](https://code.exacttarget.com/apis-sdks/soap-api/using-app-center-to-get-an-api-key.html). Then use the Fuel Authentication Service to [acquire an OAuth access token](https://code.exacttarget.com/apis-sdks/soap-api/using-the-api-key-to-authenticate-api-calls.html). If you are using OAuth, you can replace the `header` element in the request envelopes below with:

    <soapenv:Header>
       <fueloauth xmlns="http://exacttarget.com">insertAccessToken</fueloauth>
    </soapenv:Header>

## Retrieve Automation ObjectID

Before you can perform an Automation, you will need to use the following SOAP request envelope to **Retrieve** the associated `ObjectID` for an Automation. Note that the ObjectID is different from the Automation External Key.

Obviously, if you are programatically starting a specific Automation (or Automations) on a recurring basis, then you will only need to retrieve the `ObjectID` once as it won't change.

    <?xml version="1.0" encoding="utf-8"?>
    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
       <soapenv:Header>
          <wsse:Security soapenv:mustUnderstand="1" xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
             <wsse:UsernameToken wsu:Id="UsernameToken-32259181" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
                <wsse:Username>username</wsse:Username>
                <wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">password</wsse:Password>
             </wsse:UsernameToken>
          </wsse:Security>
       </soapenv:Header>
       <soapenv:Body>
            <RetrieveRequestMsg xmlns="http://exacttarget.com/wsdl/partnerAPI">
                <RetrieveRequest>
                    <ObjectType>Automation</ObjectType>
                    <Properties>ProgramID</Properties>
                    <Properties>Name</Properties>
                    <Filter xsi:type="SimpleFilterPart">
                        <Property>Name</Property>
                        <SimpleOperator>equals</SimpleOperator>
                        <Value>TheNameOfYourAutomation</Value>
                    </Filter>
                </RetrieveRequest>
            </RetrieveRequestMsg>
       </soapenv:Body>
    </soapenv:Envelope>

This request will return the following response:

    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope
        xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
        xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
        xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
        <soap:Header>
            <wsa:Action>RetrieveResponse</wsa:Action>
            <wsa:MessageID>urn:uuid:35ba39d5-e6e8-4578-aa65-1a422ea012fa</wsa:MessageID>
            <wsa:RelatesTo>urn:uuid:06f26b12-f91a-4a0f-b4db-2a9b7123c78b</wsa:RelatesTo>
            <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
            <wsse:Security>
                <wsu:Timestamp wsu:Id="Timestamp-2b86c1f4-0d47-49d4-aa9b-b9bb37c5df55">
                    <wsu:Created>2015-04-29T09:59:05Z</wsu:Created>
                    <wsu:Expires>2015-04-29T10:04:05Z</wsu:Expires>
                </wsu:Timestamp>
            </wsse:Security>
        </soap:Header>
        <soap:Body>
            <RetrieveResponseMsg
                xmlns="http://exacttarget.com/wsdl/partnerAPI">
                <OverallStatus>OK</OverallStatus>
                <RequestID>a8635a6a-f597-4b7c-9bec-9fd03ecf6967</RequestID>
                <Results xsi:type="Automation">
                    <PartnerKey xsi:nil="true" />
                    <ObjectID>10a343aa-d95b-4f6e-a90d-95f5850eb32b</ObjectID>
                    <Name>TheNameOfYourAutomation</Name>
                </Results>
            </RetrieveResponseMsg>
        </soap:Body>
    </soap:Envelope>

> Note that even though you requested `ProgramID`, and `ObjectID` value was returned.

## Start Automation

Once you have the `ObjectID` value for the Automation, you can use this value in the following SOAP request to start an Automation using **Perform** as the SOAP Action verb and the `ObjectID` value retrieved from the previous request:

    <?xml version="1.0" encoding="utf-8"?>
    <soapenv:Envelope
        xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <soapenv:Header>
            <wsse:Security soapenv:mustUnderstand="1"
                xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
                <wsse:UsernameToken wsu:Id="UsernameToken-32259181"
                    xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
                    <wsse:Username>username</wsse:Username>
                    <wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">password</wsse:Password>
                </wsse:UsernameToken>
            </wsse:Security>
        </soapenv:Header>
        <soapenv:Body>
            <PerformRequestMsg xmlns="http://exacttarget.com/wsdl/partnerAPI">
                <Action>start</Action>
                <Definitions>
                    <Definition xsi:type="Automation">
                        <ObjectID>10a343aa-d95b-4f6e-a90d-95f5850eb32b</ObjectID>
                    </Definition>
                </Definitions>
            </PerformRequestMsg>
        </soapenv:Body>
    </soapenv:Envelope>

This request will return the following response:

    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope
        xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
        xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
        xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
        <soap:Header>
            <wsa:Action>PerformResponse</wsa:Action>
            <wsa:MessageID>urn:uuid:57167880-baf7-4954-90bc-366340f56d12</wsa:MessageID>
            <wsa:RelatesTo>urn:uuid:0c4a84b1-ffb5-46d1-9261-2b56f63a55ac</wsa:RelatesTo>
            <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
            <wsse:Security>
                <wsu:Timestamp wsu:Id="Timestamp-75fa23b0-04cb-4ef5-ac83-2e3e43f0534e">
                    <wsu:Created>2015-04-29T10:29:48Z</wsu:Created>
                    <wsu:Expires>2015-04-29T10:34:48Z</wsu:Expires>
                </wsu:Timestamp>
            </wsse:Security>
        </soap:Header>
        <soap:Body>
            <PerformResponseMsg
                xmlns="http://exacttarget.com/wsdl/partnerAPI">
                <Results>
                    <Result>
                        <StatusCode>OK</StatusCode>
                        <StatusMessage>Performed Activity</StatusMessage>
                        <Object xsi:type="Automation">
                            <PartnerKey xsi:nil="true" />
                            <ObjectID>ad650395-30ce-43e2-bcdf-100f229d8c6f</ObjectID>
                            <CustomerKey>7ff66d3b-348e-8711-bdc3-00f2c8316b50</CustomerKey>
                            <IsPlatformObject>false</IsPlatformObject>
                            <Name />
                            <Description />
                            <IsActive>true</IsActive>
                        </Object>
                    </Result>
                </Results>
                <OverallStatus>OK</OverallStatus>
                <OverallStatusMessage />
                <RequestID>626b2173-f13d-4614-b828-587cfc8e2270</RequestID>
            </PerformResponseMsg>
        </soap:Body>
    </soap:Envelope>
