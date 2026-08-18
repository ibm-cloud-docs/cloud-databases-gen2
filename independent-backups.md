---

copyright:
  years: 2026
lastupdated: "2026-08-18"

subcollection: cloud-databases-gen2

keywords: independent backups, decoupled backups, backup lifecycle, backup management, cross-region backups, mysql backups

---

{{site.data.keyword.attribute-definition-list}}

# Managing independent backups
{: #independent-backups}

[Gen 2]{: tag-purple}

Independent backups are currently available only for {{site.data.keyword.databases-for-mysql}}.
{: important}

Independent backups represent a fundamental shift in how {{site.data.keyword.databases-for}} Gen 2 manages backup data. Unlike traditional backups that are tightly coupled to your database instance lifecycle, independent backups exist as separate, provisionable service instances with their own lifecycle, allowing you to retain backup data even after the source database instance is deleted. Independent backups are billed as separate service instances. For more information, see [Independent backups billing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-pricing#independent-backups-billing).
{: shortdesc}

## What are independent backups?
{: #what-are-independent-backups}

Independent backups are backup instances that operate independently from your database service instances. Each independent backup is a fully managed service resource with its own:

- Service name and Cloud Resource Name (CRN)
- Lifecycle management through {{site.data.keyword.cloud_notm}} Resource Controller
- Billing and resource tracking
- Access control and permissions

This architecture provides greater flexibility in managing your backup data, enabling use cases such as long-term data retention, compliance requirements, and disaster recovery scenarios where the source database may no longer exist.

## Key differences from coupled backups
{: #independent-vs-coupled}

| Feature | Coupled backups | Independent backups |
|---------|-------------------------|---------------------|
| Lifecycle | Tied to database instance | Independent of database instance |
| Persistence | Deleted when instance deleted | Can be persisted after instance deletion |
| Management | UI only | {{site.data.keyword.cloud_notm}} Resource Controller |
| Visibility | Instance UI only | Database Hub, Resource List, Instance UI |
| Deletion | Automatic only (30 days) | Manual and automatic |
| Cross-region copies | Not supported | Future release |
| Provisioning | Automatic and on-demand | Automatic and on-demand |
| Billing | Included with instance | Separate service billing |
{: caption="Comparison of coupled and independent backups" caption-side="bottom"}

## How independent backups work
{: #how-independent-backups-work}

### Automatic backup creation
{: #automatic-backup-creation}

When you provision a Gen 2 {{site.data.keyword.databases-for}} instance, the system automatically creates independent backup instances for your daily scheduled backups. These backups:

- Are created daily according to your backup schedule
- Persist for 30 days by default
- Are managed automatically by the service
- Appear in your Resource List and Database Hub

### On-demand backup creation
{: #ondemand-backup-creation}

You can create on-demand independent backups at any time using the {{site.data.keyword.cloud_notm}} Resource Controller. These backups:

- Are created immediately upon request
- Follow the same retention policies as automatic backups
- Can be manually deleted before expiration
- Are useful before major changes or migrations

### Backup lifecycle
{: #backup-lifecycle}

Independent backups follow this lifecycle:

1. **Provisioning**: Backup instance is created (automatically or on-demand)
2. **Active**: Backup is available for restore operations
3. **Expiration**: Backup reaches end of retention period (30 days default)
4. **Deletion**: Backup is automatically deleted or manually removed

Unlike coupled backups, independent backups can be manually deleted at any time through the Resource Controller, giving you greater control over your backup data and associated costs.

## Prerequisites
{: #backup-prerequisites}

Before you use independent backups, ensure that service-to-service authorization is configured for the following operations:

- Provisioning a database instance
- Updating a database instance
- Deprovisioning a database instance that is configured with preserve: false
- Provisioning independent backups

When a database instance is configured with preserve: false, its independent backups are also deleted when the database instance is permanently deleted.

For more information, see [Service-to-service authorization](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-iam&interface=ui#s2s-authorization-backups).

## Accessing your backups
{: #accessing-backups}

You can access independent backups in multiple locations:

- **Instance UI**: Go to your database instance's Dashboard and see the **Backups and restore** tab.
- **Database Hub**: View all backups across your account in a centralized location.
- **Resource List**: Independent backups appear as separate service instances.

Gen 2 {{site.data.keyword.databases-for}} backups can only be restored within the same region where they were created.
{: note}

## Viewing independent backups
{: #viewing-independent-backups}

Independent backups can be viewed in multiple locations:

### Database Hub
{: #database-hub-view}
{: ui}

The IBM Cloud console provides a centralized view of all backups across your account:

1. Navigate to the IBM Cloud console and go to **Resource list** > **Databases**.
2. View your database instances and their associated backups.
3. Independent backups appear as separate service instances in your resource list.

This helps you identify backups that may need cleanup or long-term retention.

### Resource List
{: #resource-list-view}
{: ui}

Independent backups appear as separate service instances in your {{site.data.keyword.cloud_notm}} Resource List:

1. Navigate to your [Resource List](https://cloud.ibm.com/resources).
2. Filter by service type to show backup instances.
3. Click on a backup instance to view details and manage its lifecycle.

### Instance backups and Restore tab
{: #instance-view}
{: ui}

In the UI, navigate to the **Backups and restore** tab where you see a table with all available backups for your database, including both coupled backups and independent backups.

The backup types can be either _On-demand_ or _Automatic_. Each backup is listed with its type, when the backup was taken, and whether it's a coupled or independent backup.

Click the backup to reveal information for that specific backup, including its full ID and CRN. A **Restore** button or a pre-formatted CLI command is there for restore options.



## Managing independent backups
{: #managing-independent-backups}

### Configuring the database instance for independent backups
{: #configuring-instance}

You can configure the following features on the database instance:

| Feature |  Independent backups | Configuration |
|---------|---------------------|---------------------|
| Retention duration | Determines when the backups can be deleted. Automatic backups are automatically deleted after the retention duration expires. On-demand backups can be manually deleted after the retention duration expires. |  Set to fixed duration of 30 days and cannot be configured. |
| Preserve backups | Determines whether the backups (both automatic and on-demand) are to be preserved if the database instance is deleted. | Set to false by default. Independent backups do not persist after the database instance is hard deleted. You can enable this option on a database instance, but it cannot be disabled after it is enabled. For {{site.data.keyword.databases-for-mysql}}, preserve is disabled by default and cannot be enabled. |
| Start time | Determines the start time of one hour window during which the automatic backup is initiated on the database instance. Automatic backups are performed daily. | Set to a default value at the time of database instance provisioning and cannot be configured. |
{: caption="Configuration features" caption-side="bottom"}

You can set the allowed configuration in the provision parameters of the database instance.
For example, the following configuration sets the backups to be preserved even after the database is deleted:
{: cli}

```sh
ibmcloud resource service-instance-create \
  <DATABASE_INSTANCE_NAME> \
  <DATABASE_SERVICE_NAME> \
  <DATABASE_SERVICE_PLAN_NAME> \
  <REGION> \
  -g <RESOURCE_GROUP> \
  -p '{
    "dataservices": {
      "backups": {"preserve": true}
    }
  }'
```
{: pre}
{: cli}

### Taking an on-demand backup in the UI
{: #ondemand-backup-ui}
{: ui}

If you plan to make major changes to your instance, like scaling or removing databases, tables, collections, on-demand backups are useful. It can also be useful if you need to back up on a schedule. On-demand backups are kept for 30 days.

To create a manual backup in the UI, go to the **Backups and restore** tab of your instance then click **Create backup**. A message is displayed that a backup is in progress, and an on-demand backup is added to the list of available backups.

Once the backup provisioning is completed, you can see the details of the backup like the Backup CRN, associated database instance and its version, region, status and size.

### Creating an independent backup using CLI
{: #creating-independent-backup-cli}
{: cli}

To create an on-demand independent backup using the {{site.data.keyword.cloud_notm}} CLI:

```sh
ibmcloud resource service-instance-create \
  <BACKUP_INSTANCE_NAME> \
  <BACKUP_SERVICE_NAME> \
  <BACKUP_SERVICE_PLAN_NAME> \
  <REGION> \
  -g <RESOURCE_GROUP> \
  -p '{
    "dataservices": {
      "source_dataservice_crn": "<DATABASE_INSTANCE_CRN>"
    }
  }'
```
{: pre}

Example:

```sh
ibmcloud resource service-instance-create \
  my-mysql-backup-20260429 \
  databases-independent-backups  \
  databases-independent-backups-gen2-standard \
  us-east \
  -g Default \
  -p '{
    "dataservices": {
      "source_dataservice_crn": "crn:v1:bluemix:public:databases-for-mysql:us-east:a/1234567890:abcd-1234-efgh-5678::"
    }
  }'
```
{: pre}

After provisioning completes, you can view backup details, such as the associated database instance and version, region, status, and size, in the **Resource Controller extensions** field of the backup instance.

Following is an example of the output of the command:

```sh
ibmcloud resource service-instance --output JSON crn:v1:staging:public:databases-independent-backups:ca-mon:a/cf8d4161fa0243b9a2a5494cd7ff66b7:4be73b7d-a395-4613-83dd-315a6e573e00:: | jq '.[0].extensions'
{
  "dataservices": {
    "backup": {
      "can_be_deleted_after": "<timestamp after which retention duration expires>",
      "size_gb": <size of the backup in GB>,
      "source_data_service_crn": "<CRN of the database provided at the time of provisioning the backup>",
      "type": "<type of the backup, value is either on_demand or automatic>",
      "version": "major version of the database"
    }
  }
}
```
{: pre}

### Deleting an independent backup
{: #deleting-independent-backup}
{: cli}

To manually delete an independent backup before its expiration:

```sh
ibmcloud resource service-instance-delete <BACKUP_CRN> --force
```
{: pre}

Example:

```sh
ibmcloud resource service-instance-delete e318275d-f860-4e4e-a63b-271fb4400c26 --force
```
{: pre}

Backups use incremental infrastructure-level volume snapshots. As a result, deleting a backup can increase the size of the remaining backups.

Deleting a backup is permanent and cannot be undone. Ensure you no longer need the backup data before deletion.
{: important}

### Restoring from an independent backup
{: #restoring-independent-backup}

Independent backups can be restored to a new database instance even if the source instance no longer exists, providing greater flexibility for disaster recovery and data retention scenarios.
{: tip}

Backups are restored to a new instance. After the new instance finishes provisioning, your data in the backup file is restored into the new instance.

By default, the new instance is auto-sized to the default disk size and same host size as the source instance at the time of the backup from which you are restoring. To adjust the resources that are allocated to the new instance, use the optional fields in the UI, CLI, or API to resize the new instance. Be sure to allocate enough for your data and workload; if the instance is not given enough resources or the backup contains more storage than the default disk size and a disk size is not specified, the restore fails.

Do not delete the backup while the backup is restoring. Before you delete the backup, wait until the new instance is provisioned and the backup is restored. Deleting the database instance also deletes its backups by default.
{: tip}

You have immediate access to the restored database instance, but I/O performance is reduced until hydration completes. Backups cannot be created on the restored instance until hydration is complete. You can track hydration progress by using platform Activity Tracker events. For more information, see [at-events](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-at_events#at_actions_platform).

#### Restoring a backup in the UI
{: #restore-backup-ui}
{: ui}

To restore a backup to a new service instance:

1. Click in the corresponding row to expand the options for the backup that you want to restore.
2. Click **Restore**.
3. On the **Provisioning** page, select from some available options.
    - You provide the name of the new service instance.
    - You can choose the initial resource allocation, or expand the resources on the new instance. Note that if you decrease your resource amount, it may lead to provision failure or your database not functioning properly.
4. Click **Restore backup**. A "restore from backup started" message appears. Clicking **Your new instance is available now** takes you to your _Resources List_.

#### Restoring a backup in the CLI
{: #restore-backup-cli}
{: cli}

The Resource Controller supports provisioning of database instances, and provisioning and restoring are the responsibility of the Resource Controller CLI. Use the [`resource service-instance-create`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command.

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID>-gen2-<PLAN NAME> <REGION> -p  '{"dataservices":{"restore_backup_id":"<BACKUP_CRN>"}}'
```
{: pre}

Example command:

```sh
ibmcloud resource service-instance-create mysql-restore-abc databases-for-mysql databases-for-mysql-gen2-standard us-east -p  '{"dataservices":{"restore_backup_id":"crn:v1:bluemix:public:databases-independent-backups:us-east:a/26b19aex04da4475b6e31205fa93248d:793b4f27-7733-4803-917f-de8e055e2deb::"}}'
```
{: pre}

* Change the value of `instance_name` to the name that you want for your new instance.
* The `service-id` is the type of instance (for example, _databases-for-mysql_).
* The `region` is where you want the new instance to be located, which can be a different region from the source instance.
* The `restore_backup_id` is the backup that you want to restore.

The previous command will restore a backup to a machine of the same configuration and on the same hosting model as your original deployment.

##### Optional parameters in the CLI
{: #restore-cli-optional}
{: cli}

Optional parameters are available through the CLI. Use them if you need to customize resources, change the hosting model, or use a Key Protect key for BYOK encryption on the new instance. See the following example:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID> gen2-<PLAN NAME> <REGION> -p
'{"restore_backup_id":"BACKUP_ID","key_protect_key":"KEY_PROTECT_KEY_CRN", "storage_gb":"DESIRED_DISK_IN_GB", "host_flavor": "<VALUE>"}'
```
{: pre}

The `host_flavor` should be an appropriate-sized host. For more information, see [the list of available values](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui).
{: note}

A pre-formatted command for a specific backup is available in detailed view of the backup on the **Backups and restore** tab of your instance's dashboard.
{: tip}

By default, restoring from a backup provisions an instance with the preferred version of the database type, not the version of the instance you restore from. Gen 2 {{site.data.keyword.databases-for}} currently only support one version per database. Over time, new versions will be released, and when a new version becomes available, you can move to that version with a restore from a backup.

#### Restoring a backup through the API
{: #restore-backup-api}
{: api}

The [Resource Controller API](/apidocs/resource-controller/resource-controller){: external} supports provisioning and restoring database instances. The create request is a `POST` to the [`/resource_instances`](/apidocs/resource-controller/resource-controller#create-resource-instance) endpoint.

```sh
curl -X POST \
  https://resource-controller.cloud.ibm.com/v2/resource_instances \
  -H 'Authorization: Bearer <>' \
  -H 'Content-Type: application/json' \
    -d '{
    "name": "<INSTANCE_NAME>",
    "target": "<REGION>",
    "resource_group": "<YOUR-RESOURCE-GROUP>",
    "resource_plan_id": "<SERVICE-ID>",
    "parameters":{
      "restore_backup_id": "<BACKUP_ID>"
    }
  }'
```
{: pre}

The parameters `name`, `target`, `resource_group`, and `resource_plan_id` are all required, and `restore_backup_id` is the backup that you want to restore.
{: important}

* Change the value of `name` to the name that you want for your new instance.
* The `resource_plan_id` is the type of instance (for example, _databases-for-mysql_).
* The `target` is the region where you want the new instance to be located, which must be a Gen 2 region.
* The `restore_backup_id` is the backup that you want to restore.

The previous command will restore a backup to a machine of the same configuration and on the same hosting model as your original deployment.

##### Optional parameters in the API
{: #restore-api-optional}
{: api}

Optional parameters are available through the Resource Controller API. Use them if you need to customize resources, change the host size, deploy to a specific version, or use a Key Protect key for BYOK encryption on the new instance.

If you need to adjust resources, add any of the optional parameters `key_protect_key`, `storage_gb`, `host_flavor` or `version` and their preferred values to the body of the request.

### Backup encryption
{: #backup-encryption}

Independent backups are encrypted at rest with the same encryption as the database instance. If you use Key Protect to manage your encryption for the database, your backups are encrypted with the same key. For more information, see [Key Protect integration](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-key-protect).

When you restore a backup that was encrypted with a Key Protect key, you can use the same key or a different key. If you use a different key, the new instance is encrypted with the new key.

### Cross-account restore
{: #cross-account-restore}

Independent backups can be restored across IBM Cloud accounts, enabling scenarios such as:
- Restoring production data to a development account for testing
- Migrating databases between organizational units
- Disaster recovery to a separate account

To restore a backup to a different account:

1. The source account must grant the target account access to the backup resource
2. Use the backup CRN when creating the new instance in the target account
3. Ensure the target account has appropriate IAM permissions

For more information about cross-account restore, see [Cross-account restore](#cross-account-restore).

## Business continuity and disaster recovery
{: #independent-backups-bcdr}

Independent backups are a critical component of your business continuity and disaster recovery strategy. Because they persist independently of the source database instance, they provide protection against:

- Accidental database deletion
- Data corruption
- Regional failures (when backups are stored in different regions)

For comprehensive information about business continuity and disaster recovery with {{site.data.keyword.databases-for}}, see:
- [Understanding business continuity and disaster recovery for {{site.data.keyword.databases-for}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr)
- [Understanding high availability and disaster recovery for {{site.data.keyword.databases-for}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-ha-dr)

## Next steps
{: #independent-backups-next-steps}

- Learn about [backup pricing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-pricing#pricing-backup).
- Review [backup FAQs](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-faq#faq-backups).
- Understand [your responsibilities](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-responsibilities-cloud-databases) for managing backups.

## Transition from coupled backups
{: #migration-from-coupled}

The transition from coupled backups to independent backups varies by database service:



### MySQL
{: #transition-mysql}

{{site.data.keyword.databases-for-mysql}} supports only independent backups from general availability. There are no coupled backups and no transition period for MySQL deployments.

## Billing for independent backups
{: #independent-backups-billing}

Independent backups are billed as separate service instances:

- **Free allocation**: You receive free backup storage equal to the total provisioned disk size of your database deployment.
- **Overage charges**: Usage beyond the free allocation is charged additionally.
- **Billing visibility**: Backup costs appear as separate line items in your billing statement.

For detailed pricing information, see [Pricing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-pricing#pricing-backup).

## Security and compliance
{: #independent-backups-security}

Independent backups maintain the same security standards as your database instances:

- **Encryption at rest**: All backups are encrypted using either IBM-managed keys or your own keys via Key Protect.
- **Encryption in transit**: Data is encrypted during backup creation and restore operations.
- **Access control**: IAM policies control who can create, view, and restore backups. For more information, see [Independent backups IAM permissions](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-iam&interface=ui#independent-backups-iam).

## Limitations and restrictions
{: #independent-backups-limitations}

Be aware of the following limitations:

- Bulk operations (bulk copy, bulk delete) are not supported.
- Independent backups cannot be downloaded; use database-specific tools (for example, `mysqldump`) for local backups.
- Backup retention duration is not yet configurable (30 days default).
- You can create upto 50 on-demand backups per database instance.
