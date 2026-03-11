---

copyright:
  years: 2026
lastupdated: "2026-03-06"

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Shared responsibilities for {{site.data.keyword.databases-for}}
{: #responsibilities-cloud-databases}

[Gen 2]{: tag-purple}


Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cloud}} {{site.data.keyword.databases-for}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the client and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.databases-for}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and notices](/docs/overview/terms-of-use?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops-responsibilities}

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|--------|-----------------------|-----------------------|
|Monitoring| {{site.data.keyword.databases-for}} is responsible for hosting monitoring and health services. | The Client is responsible for integrating with the [{{site.data.keyword.monitoringfull}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-monitoring), [{{site.data.keyword.atracker_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-at_events), or [{{site.data.keyword.logs_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-logging). |
|High availability| {{site.data.keyword.databases-for}} is responsible for deploying databases across availability zones in a multizone region (MZR), or across hosts in a single-campus multizone region, and storing backups in {{site.data.keyword.block_storage_is_short}} instances for Gen 2 {{site.data.keyword.databases-for}}. {{site.data.keyword.databases-for}} provides replication, fail-over features, and infrastructure maintenance or updates. High availability varies based on each database type, refer to database-specific documentation for details. | The Client is responsible for designing application logic to retry connections caused by temporary connection failures (during regular database maintenance and updates).|
|Database performance | {{site.data.keyword.databases-for}} is responsible for hosting and maintaining database infrastructure. | The Client is responsible for the data model and performance, including tuning the data model, queries, and scaling the database as necessary for application needs. |
|Operating System | {{site.data.keyword.databases-for}} is responsible for hosting and maintaining database Operating System infrastructure. | The Client is not responsible for, nor has access to, Operating System level activities. |
{: caption="Responsibilities for incident and operations" caption-side="top"}

## Change management
{: #change-management-responsibilities}

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Scaling| {{site.data.keyword.databases-for}} is responsible for scaling infrastructure to meet client requests. | The Client is responsible for choosing, monitoring, and scaling disk, memory, and CPU core allocation for their deployments by using the UI or API. If a database deployment runs out of disk space, it might go down and must be restored from backup. |
|Version management | {{site.data.keyword.databases-for}} is responsible for maintaining minor versions and patches as described in the [version lifecycle policy](/docs/cloud-databases?topic=cloud-databases-versioning-policy). {{site.data.keyword.databases-for}} is also responsible for providing availability and tools for database major version upgrades. | The Client is responsible for running major database version upgrades. The Client is also responsible for monitoring for EOL announcements and moving off EOL versions before the end of support date that is announced by {{site.data.keyword.databases-for}} also described in the version lifecycle policy.|
{: caption="Responsibilities for change management" caption-side="top"}

## Security and regulation compliance
{: #security-responsibilities}

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Encryption| {{site.data.keyword.databases-for}} is responsible for the encryption of data on disk, in motion, and in backups. | The Client is responsible for choosing and managing appropriate additional security features. If using Key Protect and Bring Your Own Key (BYOK), the client is responsible for managing Key Protect authorizations and keys. |
|Security| {{site.data.keyword.databases-for}} is responsible for ensuring the security of data on disk and data in motion within our infrastructure. | The Client is responsible for managing {{site.data.keyword.cloud_notm}} passwords via service credentials and ensuring that they are stored properly. The Client is also responsible for configuring appropriate network security or isolation (for example, context-based restrictions). |
|Compliance| {{site.data.keyword.databases-for}} is responsible for ensuring adherence, auditing, and certification of compliances listed at the [IBM Cloud compliance page](https://www.ibm.com/cloud/compliance). | The Client is responsible for the storing, processing, and transmission of their data. More information on these specific responsibilities can be found in each of the {{site.data.keyword.databases-for}} offerings' specific Security Compliance documentation. |
{: caption="Responsibilities for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery-responsibilities}

PITR is not currently available for Gen 2 {{site.data.keyword.databases-for}} instances.
{: note}

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Backups and restore| {{site.data.keyword.databases-for}} is responsible for automatic daily backups, as well as monitoring the state of client backups.| The Client is responsible for restoration, timeliness, validity of backups, and alerting of failed backups via [{{site.data.keyword.atracker_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-at_events). For more information, see [Managing Cloud Databases backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui).|
|Read-only replicas (_{{site.data.keyword.databases-for-postgresql}} and {{site.data.keyword.databases-for-mysql}} ONLY_)| {{site.data.keyword.databases-for-postgresql}} and {{site.data.keyword.databases-for-mysql}} are responsible for providing the capability of deploying read-only replicas across regions (except for replicating data into or outside of `eu-de`). | The Client is responsible for provisioning, configuring, monitoring, and promoting read-only replicas. |
{: caption="Responsibilities for disaster recovery" caption-side="top"}
