#How contact builder is used with Salesforce Marketing Cloud

> Salesforce Marketing Cloud Contact Builder allows the data designer to access data, design data relationships and link data to external sources.

Contact Builder is a data design tool used access data contained in a Salesforce Marketing Cloud account and to design data relationships. 

##Contact Builder Tools

Contact Builder consists of the following tools:

* [**Data designer**](https://help.marketingcloud.com/en/documentation/contact_builder/data_designer/) - is used to create attribute groups which are used to organise data relationships. Data designer allows data extensions to be linked to contacts.
* [**All contacts**](https://help.marketingcloud.com/en/documentation/contact_builder/all_contacts/) - is used to list all contacts in the Marketing Cloud account. The population of contacts can be filtered on recently modified, source and channel. For each individual contact engagement, membership and attribute information is available.
* [**Data sources**](https://help.marketingcloud.com/en/documentation/contact_builder/data_sources/) - is used to describe where the Marketing Cloud account stores and locates contact attributes.
* [**Data extensions**](https://help.marketingcloud.com/en/documentation/contact_builder/data_extensions/) - is used to create, read, update and delete data extensions. Data extensions are the tables used by the Marketing Cloud account to store data. Data extensions are used by the data design tool when organising relationships between objects.
* [**Imports**](https://help.marketingcloud.com/en/documentation/contact_builder/imports/) - is used to define an import definition.
* [**Contact**](https://help.marketingcloud.com/en/documentation/contact_builder/contacts_configuration/) - is used to determine channel send preferences. 

##Data Relationships

When relationships are created in the data design tool the cardinality for the relationship is specified. Options include:

* **One-to-One relationship** - indicates that the data extensions relate to each other on a single primary key. 
* **Populations** - represent a master set of contacts with in a Marketing Cloud account. Examples of populates in the same for a health care provider could include the following three separate populations: patients; doctors; and insurers. Populations link to the contact model using the primary key with a one-to-one relationship. To aviod performance issues do not create more 3 populations in the data model.
* **One-to-Many relationship** - is where the primary key linked to the contact model has are multiple items linked to it in another data extension. An example is multiple orders for a contact.
* **Many-to-Many Relationship ** - is where there are multiple records in the linked data extensions that both contain the same value.

Changes to cardinality change the relationship that data extensions have with one another. When making changes to cardinality review all filtered lists, filters and scheduled sends.


##Links

* [Contact Builder](https://help.marketingcloud.com/en/documentation/contact_builder/)
