#Getting started AMPScript developer notes

> According to [Marketing Could, What is AMPScript](http://help.exacttarget.com/AMPscript/) - "AMPscript is a scripting language that you can embed within HTML emails, text emails, landing pages, and SMS messages."

AMPScript is processed on the server by the Marketing Cloud system. What this means is that by the time a document is sent to the client it has already had any AMPScript rendered. For this discussion a document is any Marketing Could HTML/text email, landing page or SMS message.

##AMPScript functions allows documents to:

* use relational data stored in data extensions
* have logic to control rendering
* apply formatting to variables

##How to use AMPScript

For the AMPscript script function block wrap AMPScript function with opening `%%[` and closing `]%%`` delimiters, for example `%%[script]%%`.

For inline AMPscript (or function calls outside or the AMPscript script function block) wrap the AMPScript function with opening `%%=` and closing `=%%`` delimiters, for example `%%=function=%%`.

An example of an inline AMPscript function is returning a value, for example `%%[ LOWERCASE(Name) ]%%`.

##AMPscript Language Elements

AMPscript has the following language elements:

* Constants
* Attributes and data extensions
* Keywords
* Conditional logic
* Output
* Comments
* Functions
  * Data modification functions
  * DateTime functions
  * HTTP functions
  * Microsite and landing page functions
  * Mobile variables/functions
  * Social functions
  * Utilities functions
  * API functions

###Constants

Constants are fixed numeric, string or boolean values.

###Attributes and Data Extensions

Attributes and data extensions are values referenced from functions and objects. Values are enclosed in square brackets, for example `[Data Extension Attribute Name]`.

###Keywords

Keywords are variables declared, initialized, and modified within a script.

Keywords are prefixed with the @ symbol, for example `@Name`.

Keywords are declared using the `[VAR]` and `[SET]` syntax, for example:

```
%%[
VAR @Name
SET @Name = "Sam Sample"
]%%
@Name
```

###Conditional logic

Conditional logic is used to control to flow of the script.

Conditional logic consists of:

* `IF` syntax which is used to evaluate a condition, keywords include  `[IF]`, `[ELSEIF]`, `[ELSE]` and `[ENDIF]`.
* `FOR` syntax which is used to process through a loop, keywords include `[FOR]` and `[NEXT]`.

###Output

Output renders code inside a code block, for example `%%[Output(Now())]%%`.

###Comments

Comments are ignored by AMPScript and contain a readable annotations that can help to make code easier to understand, for example `%%[ /* Insert Comment Here */ ]%%`.

###Functions

####Data Modification Functions

There are 2 types of data modification functions. These are used for send time support and landing page support. These functions allow insert, update, upsert (update/insert), and delete actions to be performed at the subscriber level. Data modification functionality include:

* Send time support data modification function includes only the [InsertDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertDE) function.
* Landing page support data modification function includes the [InsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertData), [UpdateData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpdateData), [UpsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpsertData) and [DeleteData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#DeleteData) functions.

For a discussion of all data extention functions refer to [Data Extension AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/). In sumary functions include:

* [ClaimRow](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#ClaimRow) and [ClaimRowValue](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#ClaimRowValue) are used to return values and data extension records.
* [DataExtensionRowCount](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#dataextensionrowcount) is used to return the number of rows in a data extension.
* [DeleteData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#DeleteData) and [DeleteDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#DeleteDE) are used in different contexts to delete rows from a data extension.
* [ExecuteFilter](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#ExecuteFilter) and [ExecuteFilterOrderedRows](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#ExecuteFilterOrderedRows) are used to executes a predefined data filter and return a resultset from a data extension.
* [InsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertData) and [InsertDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertDE) are used in different context to insert rows into a data extension.
* [Lookup](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#Lookup), [LookupOrderedRows](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#LookupOrderedRows), [LookupOrderedRowsCS](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#LookupOrderedRows), [LookupRows](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#LookupRows) and [LookupRowsCS](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#LookupRowsCS) functions return result sets from data extensions.
* [UpdateData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpdateData), [UpdateDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpdateDE), [UpsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpsertData) and [UpsertDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#UpsertDE) are used in different contexts to update/upsert a data extension.

#####Examples showing AMPscript data functions

* [Example showing how to work with lookup tables (data extension) and selecting fields using IF ELSE logic](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/getting_started_with_ampscript/ampscript_201/)
* [Example showing how to loop through and conditionally format lookup table (data extension) results](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/getting_started_with_ampscript/ampscript_401/)

####DateTime functions

Refer to [DateTime AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/) for a complete list of DateTime functions. In summary functions include:

* [DateAdd](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#DateAdd) function is used to do calculation on a date.
* [DateDiff](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#DateDiff) function is used to find the difference between 2 dates.
* [DateParse](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#DateParse) function is used to convert a string to a date.
* [DatePart](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#DatePart) function is used to extract a specified part from a date.
* [LocalDateToSystemDate](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#LocalDateToSystemDate) function is used to convert the local date to the system date.
* [Now](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#Now) function is used to return the current date and time.
* [SystemDateToLocalDate](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/datetime_ampscript_functions/#SystemDateToLocalDate) function is used to convert the system date to the user's local time.

####HTTP functions

Refer to [HTTP AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/) for a complete list of HTTP functions. In summary functions include:

* [HTTPGet](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#HTTPGet) function is used to return content from a specified URL.
* [HTTPPost](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#httppost) and [HTTPPost2](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#httppost2) functions are used to post content to a specified URL.
* [HTTPRequestHeader](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#HTTPRequestHeader) function is used to retrieve a specified header from a HTTP request.
* [IsCHTMLBrowser](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#IsCHTMLBrowser) function is used to indicate if the passed-in user agent value represents a CHTML browser.
* [RedirectTo](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#RedirectTo) function is used allow a client to specify the target of a link be a complete URL stored in an attribute, DE (data extension) field, or variable. 
* [URLEncode](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#URLEncode) function is used to return a fully encoded URL.
* [WrapLongURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#WrapLongURL) function is used to return a wrapped URL that can be used in your send to ensure compatibility with Outlook 2007. For use where URL exceeds 975 characters.

#####Example showing AMPscript HTTPGet HTTP function used in email content

Following is example email content showing AMPscript HTTPGet HTTP function. Data extension used for example contains sendable email. To test copy this code block into email contents and preview.

```
%%[

/* Example email content showing AMPscript HTTPGet HTTP function. Data extension used for example contains sendable email. */

Var @content
Set @content = HTTPGet("http://www.example.com/")
]%%

<table>
 <tr><th>FUNCTION</th><th>RESULT</th></tr>
 <tr><td><a href="http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/http_ampscript_functions/#HTTPGet">HTTPGet</a> function applied to <code>http://www.example.com</code></td><td>%%=v(@content)=%%</td></tr>
</tr>
</table>

```

####Microsite and landing page functions

Refer to [Microsite and Landing Page AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/) for complete list of microsite and landing page functions. In summary functions include:

* [AuthenticatedEmployeeID](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedEmployeeID), [AuthenticatedEmployeeNotificationAddress](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedEmployeeNotificationAddress), [AuthenticatedEmployeeUserName](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedEmployeeUserName), [AuthenticatedEnterpriseID](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedEnterpriseID), [AuthenticatedMemberID](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedMemberID) and [AuthenticatedMemberName](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#AuthenticatedMemberName) functions are used to return information about the authenticated landing page user.
* [CloudPagesURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#cloudpagesURL) function provides a way for users to reference a CloudPages URL in an account from an email message. Use this function within an email to pass information via a URL in an encrypted query string.
* [DeleteData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#DeleteData) function deletes rows from a data extension.
* [InsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertData) function inserts rows into a data extension.
* [IsNullDefault](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#IsNullDefault) function is used to return a default value if test is null.
* [LiveContentMicrositeURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#LiveContentMicrositeURL) function provides a way to return a microsite URL by referencing a coupon name that is being hosted on a microsite.
* [MicrositeURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#MicrositeURL) function provides a way for Enterprise 2.0 users to reference a landing page URL in the top-level business unit in an Enterprise 2.0 account from an email message in any child business unit within the same Enterprise 2.0 account. Use this function within an email to pass information via a URL in an encrypted query string.
* [QueryParameter](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#QueryParameter) function returns the value from a query string based the key.
* [Redirect](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#Redirect) function redirects the recipient's browser to the specified URL.
* [RequestParameter](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/microsite_and_landing_page_ampscript_functions/#RequestParameter) function returns the value of a parameter passed into the query string of a landing page URL or passed via a form post.

#####Example showing AMPscript InsertData function used in microsite or landing page content

Following is example of microsite or landing page content showing AMPscript InsertData function. Target data extension used for example requires nameofEvent and timeofEvent fields. To test copy this code block into microsite or landing page content and preview.

```
%%[

/* Example microsite or landing page content showing AMPscript InsertData function. Target data extension used for example requires nameofEvent and timeofEvent fields. */

InsertData("ampscripresult", "nameofEvent", "OPEN", "timeofEvent", NOW())

]%%
```

####Mobile variables/functions

Refer to [AMPscript Variables for Use with Mobile Messages](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/ampscript_variables_for_use_with_mobile_messages/) for complete list of mobile variables/functions. In summary variables/functions include:

* MMS_CONTENT_URL(O1) - use this function to return the URL of incoming MMS content used in a mobile message.
* MSG(O1) - use this function to return the specified MO keyword used in a mobile message conversation.
* NOUN(O1) - use this function to return the specified noun used in a mobile message.

####Social functions

Refer to [Social AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/social_ampscript_functions/) for complete list of social functions. In summary functions include:

* [GetPublishedSocialContent](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/social_ampscript_functions/#GetPublishedSocialContent) function returns content to be shared on a social network as specified by the region ID.
* [GetSocialPublishURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/social_ampscript_functions/#GetSocialPublishURL) function retrieves the URL of a social network from a lookup table and creates a link to that social network for use with content to be shared from an email.
* [GetSocialPublishURLByName](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/social_ampscript_functions/#GetSocialPublishURLByName) function returns the URL to the publish content page, including a site name, country code, a region ID, and optional pairs of parameter information, such as ShareThis publisher ID information.

####Utilities functions

Refer to [Utilities AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/utilities_ampscript_functions/) for complete list of utility functions. In summary utility functions all include functions that to do calculations, encoding/decoding, logical tests and string formatting/manipulation.

#####Example showing some AMPscript utilities functions functions used in email content

Following is example email content showing some of the AMPscript utilities functions. Data extension used for example contains sendable email and name fields. To test copy this code block into email contents and preview.

```

%%[

/* Example email content showing some of the AMPscript utilities functions. Data extension used for example contains sendable email and name fields. To test copy this code block into email contents and preview.*/

/* Note that for a field to be displayed in content it first must be assigned to an AMPScript variable. */

Var @subscriber_name
Set @subscriber_name = name

]%%

<table>
 <tr><th>FUNCTION</th><th>RESULT</th></tr>
 <tr><td><a href="http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/utilities_ampscript_functions/#Add">Add</a> function applied <code>1 + 2</code></td><td>%%=ADD(1,2)=%%</td></tr>
 <tr><td>No function applied to <code>@subscriber_name</code> field</td><td>%%=v(@subscriber_name)=%%</td></tr>
 <tr><td><a href="http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/utilities_ampscript_functions/#Lowercase">LowerCase</a> function applied to <code>@subscriber_name</code> field</td><td>%%=LOWERCASE(@subscriber_name)=%%</td></tr>
 <tr><td><a href="http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/utilities_ampscript_functions/#ProperCase">ProperCase</a> function applied to <code>@subscriber_name</code> field</td><td>%%=PROPERCASE(@subscriber_name)=%%</td></tr>
 <tr><td><a href="http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/utilities_ampscript_functions/#Uppercase">UpperCase</a> function applied to <code>@subscriber_name</code> field</td><td>%%=UPPERCASE(@subscriber_name)=%%</td></tr>
</table>


```

####API AMPscript functions

[API AMPscript functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/) allow AMPscript to work with [objects in the Marketing Cloud API](https://help.exacttarget.com/en/technical_library/web_service_guide/objects/). The Marketing Cloud API objects allow various functionallity of the Marketing Cloud to be controlled programmaticly. Example use cases include sending emails and creating data extensions.

Refer to [API AMPscript functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/) for complete list of API AMPscript functions. These functions do not work in emails at the time of send. In these function map to method and properties used with objects. In summary functions include:

* [AddObjectArrayItem](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#AddObjectArrayItem) used to add item to array.
* [CreateObject](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#CreateObject) used to service API object.
* [Field](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#Field) use to return field from object
* [InvokeCreate](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokeCreate) used to invoke the create method on the API object.
* [InvokeDelete](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokeDelete) used to invoke the delete method on the API object.
* [InvokeExecute](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokeExecute) used to invoke the execute method on the API object.
* [InvokePerform](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokePerform) used to invoke the perform method on the API object.
* [InvokeRetrieve](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokeRetrieve) used to invoke the retrieve method on the API object.
* [InvokeUpdate](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#InvokeUpdate) used to invoke the update method on the API object.
* [RaiseError](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#RaiseError) use to handle errors.
* [SetObjectProperty](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/api_ampscript_functions/#SetObjectProperty) used to set a value in the API object.

#####Example showing API AMPscript function to insert a record into a data extension.

Following is example showing how to insert a record into a data extension using an API AMPscript function. In example values will be inserted into the nameofEvent and timeofEvent fields of TargetDE data extension. Note that AMPScript also provides [InsertData](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertData) and [InsertDE](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/data_extension_ampscript_functions/#InsertDE) for inserting data into a data extension.


```
%%[

/* Create data extension object */
Set @de = CreateObject("DataExtensionObject")
SetObjectProperty(@de,"CustomerKey","TargetDE")

/* Create first field to insert into record */
Set @deProperty_1 = CreateObject("APIProperty")
SetObjectProperty(@deProperty_1,"Name","nameofEvent")
SetObjectProperty(@deProperty_1,"Value","OPEN")

/* Create second field to insert into record */
Set @deProperty_2 = CreateObject("APIProperty")
SetObjectProperty(@deProperty_2,"Name","timeofEvent")
SetObjectProperty(@deProperty_2,"Value",NOW())

/* Add fields to record */
Set @deProperties = CreateObject("APIProperty")
AddObjectArrayItem(@de,"Properties",@deProperty_1)
AddObjectArrayItem(@de,"Properties",@deProperty_2)

/* Insert record into data extension object */
Set @StatCode = InvokeCreate(@de, @StatMessage, @ErrorCode)

/* In production do error check on @StatCode to test success */ 

]%%
```

#####Links to examples showing API AMPscript functions

* [Creating a Data Extension Using AMPscript and the Web Service API](https://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/using_ampscript_with_the_web_service_api/creating_a_data_extension_using_ampscript_and_the_web_service_api/)

##Helpful AMPScript links and resources

###AMPScript must reads:

>Suggested must reads for releasing potential of AMPScript functions.

* [What is AMPScript](http://help.exacttarget.com/AMPscript/) - overview plus links
* [AMPscript Syntax Guide](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/) - webpage contains syntax and alphabetical list of AMPscript functions

###Interesting AMPScript reads:

>Suggested reads for advanced functionallity.

* [Content AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/) allow for functionallity to work with: [AttachedFile](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#AttachFile) for email attachments, [BarCodeURL](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#BarCodeURL) for working with barcodes, [BeginImpressionRegion](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#BeginImpressionRegion), [EndImpressionRegion](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#EndImpressionRegion) for working with impression regions, [BuildOptionList](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#BuildOptionList) for option lists, content creation from delimetered/XML data with [BuildRowSetFromString](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#BuildRowSetFromString) and [BuildRowSetFromXML](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#BuildRowSetFromXML) functions, SMS with CreateSmsConversation and EndSmsConversation functions, [GetPortfolioItem](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#GetPortfolioItem) and [Image](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#Image) functions for working with portfolios, [TransformXML](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#TransformXML) for transforming XML items in portfolio and [WAT and WATP](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/content_ampscript_functions/#WAT) functions for web analytics tracking options. Some of these require additional features enabled in the Marketing Cloud account.
* [Contacts AMPscript Functions](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/contacts_ampscript_functions/) takes information sent from mobile devices to Salesforce Marketing Cloud applications and processes it accordingly. Contacts AMPscript functions cannot be used in email messages or SMS messages outside of the MobileConnect app. The contacts AMPscript function is [UpsertContact](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/contacts_ampscript_functions/#UpsertContacts). Function can be used to update a contact from a landing page or from an SMS message.

###AMPScript guides for:

* [Microsoft Dynamics CRM](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/ampscript_functions_for_use_with_microsoft_dynamics_crm/)
* [Salesforce.com](http://help.exacttarget.com/en/documentation/exacttarget/content/ampscript/ampscript_syntax_guide/ampscript_functions_for_use_with_salesforcecom/)

