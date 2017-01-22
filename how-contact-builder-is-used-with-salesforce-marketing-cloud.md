#How contact builder is used with Salesforce Marketing Cloud

> Salesforce Marketing Cloud Contact Builder allows the data designer to access data, design data relationships and link data to external sources.

Contact Builder is a data design tool used access data contained in a Salesforce Marketing Cloud account and to design data relationships. 

##Examples for how to build attribute groups

###Issue tracker example

In the issue tracker data relationship example, each contact record can have multiple issues. In this simple example, a contact record is linked to many records in the issues table.

####How to implement in contact builder the issue tracker example

1. In data designer create a new attribute group.
2. Create or select the contacts data extension.
3. Link the contacts data extension to customer data object. The relationship between Customers Data and the contacts data extension should be a one-to-one relationship between the `Contact Key` field in the Customers Data object and the PrimaryKey in the contacts data extension.
4. Create or select the issues data extension.
5. Link the issues data extension to the contacts data extension. The relationship between the two data extensions should be a one-to-many relationship between the PrimaryKey on the contacts data extension and the corresponding field on the issues data extension.

##Contact Builder Tools

Contact Builder consists of the following tools:

* [**Data designer**](https://help.marketingcloud.com/en/documentation/contact_builder/data_designer/) - is used to create attribute groups which are used to organise data relationships. Data designer allows data extensions to be linked to contacts.
* [**All contacts**](https://help.marketingcloud.com/en/documentation/contact_builder/all_contacts/) - is used to list all contacts in the Marketing Cloud account. The population of contacts can be filtered on recently modified, source and channel. For each individual contact engagement, membership and attribute information is available.
* [**Data sources**](https://help.marketingcloud.com/en/documentation/contact_builder/data_sources/) - is used to describe where the Marketing Cloud account stores and locates contact attributes. There are three types of data source location consisting of system, synchronized and custom. System data sources are automatically allocated depending on functionality enabled in the Marketing Cloud. The synchronized data sources reflect how the Marketing Cloud account is using the Marketing Cloud Connector. Custom data sources is used to identify where the attributes for values originate.
* [**Data extensions**](https://help.marketingcloud.com/en/documentation/contact_builder/data_extensions/) - is used to create, read, update and delete data extensions. Data extensions are the tables used by the Marketing Cloud account to store data. Data extensions are used by the data design tool when organising relationships between objects.
* [**Imports**](https://help.marketingcloud.com/en/documentation/contact_builder/imports/) - is used to define an import definition.
* [**Contact**](https://help.marketingcloud.com/en/documentation/contact_builder/contacts_configuration/) - is used to determine channel send preferences. 

##Data Relationships

When relationships are created in the data design tool the cardinality for the relationship is specified, options include:

* **One-to-One relationship** - indicates that the data extensions relate to each other on a single primary key. 
* **Populations** - represent a master set of contacts with in a Marketing Cloud account. An example of using populations is a separate population for each patients, doctors and insurers in a health care provider Marketing Cloud account. Populations link to the contact model using the primary key with a one-to-one relationship. To avoid performance issues do not create more 3 populations in the data model.
* **One-to-Many relationship** - is where the primary key is linked to multiple items in another data extension. An example is a customer having multiple orders.
* **Many-to-Many Relationship** - is where there are multiple records in the linked data extensions that both contain the same value.

Changes to cardinality change the relationship that data extensions have with one another. After making changes to cardinality review all filtered lists, filters and scheduled sends.

##Links

* [Contact Builder](https://help.marketingcloud.com/en/documentation/contact_builder/)
