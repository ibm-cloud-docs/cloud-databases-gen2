---
copyright:
  years: 2026
lastupdated: "2026-11-27"

keywords: independent backups, backup portability, data portability, cloud databases

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.independent-backups}}
{: #data-portability}

[Gen 2]{: tag-purple}

{{site.data.keyword.independent-backups}} preserves database data independently of the lifecycle of the original deployment. To move data outside of {{site.data.keyword.cloud_notm}}, restore an independent backup to a supported database deployment and use database-native export tools to create a portable copy of your data.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and guidance to help you copy and store customer content, including related configuration data, in a location of your choice. 

You're responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- Planning and setting up alternative infrastructure on another cloud provider or an on-premises environment that provides capabilities similar to those of {{site.data.keyword.IBM_notm}} services.
- Porting and adapting application code, deployment automation, and related tooling to run on the target environment.
- Converting exported data and configuration into formats that are supported by the target environment and applications.
- Restoring independent backups to a supported database deployment and using database-native export tools to obtain a portable copy of your data.

For more information about responsibility ownership between {{site.data.keyword.IBM_notm}} and the customer, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.independent-backups}} preserves database data independently of the lifecycle of the original deployment. Independent backups are not a downloadable export format and cannot be exported directly.

To obtain a portable copy of your data:

- Restore the independent backup to a supported database deployment.
- Use the export tools that are provided by the database engine.
- Store or transfer the exported data in the format that is required by your target environment.

Examples of database-native export tools include:

- `pg_dump` for PostgreSQL
- `mysqldump` for MySQL
- `mongodump` for MongoDB

For detailed export procedures and supported export formats, see the documentation for your database service.

## Exported data formats
{: #data-portability-data-formats}

{{site.data.keyword.independent-backups}} stores backup data in a service-managed format that is used to restore supported database deployments.

{{site.data.keyword.independent-backups}} doesn't provide direct access to downloadable backup files or a customer-accessible backup format.

To move data to another cloud provider or on-premises environment, restore the independent backup to a supported database deployment and use the export tools that are provided by the database engine.

Supported export formats depend on the database engine and can include:

- SQL dumps and schema exports for PostgreSQL and MySQL.
- BSON dumps and collection exports for MongoDB.

For database-specific export formats and procedures, see the documentation for your database service.

## Data ownership
{: #data-portability-ownership}

All exported data is considered customer content. Customers retain ownwership of exported data and are responsible for storing, securing, transferring, and managing that data after it is exported from the service. For more information, see the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS){: external}.
