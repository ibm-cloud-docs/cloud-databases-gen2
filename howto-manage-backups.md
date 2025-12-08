---

copyright:
  years: 2025
lastupdated: "2025-12-08"

subcollection: cloud-databases-gen2

keywords: backups, new deployment, source deployment, backup, back up, ondemand backup, on-demand backup, on-demand back up, instance

---

{{site.data.keyword.attribute-definition-list}}

# Managing Gen 2 {{site.data.keyword.databases-for}} backups
{: #dashboard-backups}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

An automatically scheduled backup is taken of your database every day. You can also trigger on-demand backups at any time. Backups are encrypted either with an automatic key or your own key if you use Bring Your Own Key (BYOK).  If BYOK is set up for a Gen 2 {{site.data.keyword.databases-for}} instance, the backups will be created using the key. You can restore a backup to a new instance of {{site.data.keyword.databases-for}}.

To access backups for {{site.data.keyword.databases-for}}, go to your database instance's Dashboard, and see the *Backups and restore* tab.

Gen 2 {{site.data.keyword.databases-for}} backups can only be restored within the same region where they were created.
{: .note}

Here is some additional general information about backups:

- Automatic backups are performed daily and kept with a simple retention schedule of 30 days.
- Backups cannot be deleted.
- If you delete your instance, its backups are deleted automatically.
- Daily backup scheduling is not configurable.
- Backup storage is encrypted. To manage the encryption keys, see [Key Protect integration](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-key-protect&interface=ui#key-byok). Otherwise, backups are encrypted with a key that is automatically generated for your instance.
- Backups are restorable across accounts, but only through the API and only if the user that is running the restore has access to both the source and destination accounts.
- {{site.data.keyword.databases-for}} backups are not downloadable. If you need a local backup, use the appropriate software. For example, [pg_dump](https://www.postgresql.org/docs/9.6/static/backup-dump.html){: .external} is an effective tool for managing PostgreSQL backups.

For information on taking an on-demand backup, see [Managing Gen 2 backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui).

## Backups in the UI
{: #backup-ui}
{: ui}

In the UI, navigate to the *Backups and restore* tab where you see a table with all available backups for your database.

The backup types can be either _On-demand_ or _Automatic_. Each backup is listed with its type and when the backup was taken.

Click the backup to reveal information for that specific backup, including its full ID. A **Restore** button or a pre-formatted CLI command is there for restore options.

## Backups in the CLI
{: #backup-ui-cli}
{: cli}

You can access the list of backups and individual backup information from the {{site.data.keyword.databases-for}} CLI plug-in and the {{site.data.keyword.databases-for}} API.

Use the [`cdb deployment-backups-list`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-reference) command to view the list of all available backups for your instance. To get details about a specific backup, use the [`cdb backup-show`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-reference) command.

For example, to view the backups for an instance named "example-instance", use the following command:

```sh
ibmcloud cdb deployment-backups-list <INSTANCE_NAME_OR_CRN>
```
{: .pre}

To see the details of one of the backups from the list, take the ID from the `ID` field of the `deployment-backups-list` response and use it with the `backup-show` command:

```sh
ibmcloud cdb backup-show crn:v1:staging:public:cloud-databases:us-south:a/6284014dd5b487c87a716f48aeeaf99f:3b4537bf-a585-4594-8262-2b1e24e2701e:backup:a3364821-d061-413f-a0df-6ba0e2951566
```
{: .pre}

## Backups in the {{site.data.keyword.databases-for}} API
{: #backup-ui-api}
{: api}

For backups information in the {{site.data.keyword.databases-for}} API, use the [`/deployments/{id}/backups`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api) endpoint to list the instance's backups. To get information about a specific backup, use the [`/backups/{backup_id}`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api) endpoint.

### Taking an on-demand backup in the UI
{: #ondemand-backup-ui}
{: ui}

If you plan to make major changes to your instance, like scaling or removing databases, tables, collections, on-demand backups are useful. It can also be useful if you need to back up on a schedule. On-demand backups are kept for 30 days.

Instances come with backup storage equal to their total disk space at no cost. If your backup storage usage is greater than total disk space, each gigabyte is charged at an overage of $0.03/month. Backups are compressed, so even if you use on-demand backups, most instances do not exceed the allotted credit.
{: .tip}

To create a manual backup in the UI, go to the _Backups and restore_ tab of your instance then click **Create backup**. A message is displayed that a backup is in progress, and an on-demand backup is added to the list of available backups.

### Taking an on-demand backup in the CLI
{: #ondemand-backup-cli}
{: cli}

If you plan to make major changes to your instance, like scaling or removing databases, tables, collections, on-demand backups are useful. It can also be useful if you need to back up on a schedule. On-demand backups are kept for 30 days.

Instances come with backup storage equal to their total disk space at no cost. If your backup storage usage is greater than total disk space, each gigabyte is charged at an overage of $0.03/month. Backups are compressed, so even if you use on-demand backups, most instances do not exceed the allotted credit.
{: .tip}

In the CLI, an on-demand backup is triggered with the [`cdb deployment-backup-now`](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#deployment-backup-now) command.

```sh
ibmcloud cdb deployment-backup-now <INSTANCE_NAME_OR_CRN>
```
{: .pre}

### Taking an on-demand backup in the API
{: #ondemand-backup-api}
{: api}

If you plan to make major changes to your instance, like scaling or removing databases, tables, collections, on-demand backups are useful. It can also be useful if you need to back up on a schedule. On-demand backups are kept for 30 days.

Instances come with backup storage equal to their total disk space at no cost. If your backup storage usage is greater than total disk space, each gigabyte is charged at an overage of $0.03/month. Backups are compressed, so even if you use on-demand backups, most instances do not exceed the allotted credit.
{: .tip}

In the API, sending a POST to the [`/deployments/{id}/backups`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api) endpoint triggers an on-demand backup.

## Restoring a backup
{: #restore-backup}

Backups are restored to a new instance. After the new instance finishes provisioning, your data in the backup file is restored into the new instance.

By default, the new instance is auto-sized to the same disk and memory allocation as the source instance at the time of the backup from which you are restoring. To adjust the resources that are allocated to the new instance, use the optional fields in the UI, CLI, or API to resize the new instance. Be sure to allocate enough for your data and workload; if the instance is not given enough resources, the restore fails.

Do not delete the source instance while the backup is restoring. Before you delete the old instance, wait until the new instance is provisioned and the backup is restored. Deleting an instance also deletes its backups.
{: .tip}

### Restoring a backup in the UI
{: #restore-backup-ui}
{: ui}

To restore a backup to a new service instance,

1. Click in the corresponding row to expand the options for the backup that you want to restore.
2. Click **Restore**.
3. On the **Provisioning** page, select from some available options.
    - The new instance is automatically named `<name>-restore-[timestamp]`, but you can rename it.
    - You can choose the initial resource allocation, either to expand or shrink the resources on the new instance. Note that if you decrease your resource amount, it may lead to provision failure or your database not functioning properly.
4. Click **Restore backup**. A "restore from backup started" message appears. Clicking **Your new instance is available now** takes you to your _Resources List_.

### Restoring a backup in the CLI
{: #restore-backup-cli}
{: cli}

The Resource Controller supports provisioning of database instances, and provisioning and restoring are the responsibility of the Resource Controller CLI. Use the [`resource service-instance-create`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command.

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID> standard <REGION> -p '{"backup_id":"BACKUP_ID"}'
```
{: .pre}

* Change the value of `instance_name` to the name that you want for your new instance.
* The `service-id` is the type of instance, such as _databases-for-postgresql_ or _messages-for-rabbitmq_.
* The `region` is where you want the new instance to be located, which can be a different region from the source instance. Cross-region restores are supported, except for restoring to or from `eu-de` by using another region.
* `backup_id` is the backup that you want to restore.

The previous command will restore a backup to a machine of the same configuration and on the same [hosting model](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli) as your original deployment.

#### Optional parameters
{: #hosting-model-cli}
{: cli}

Optional parameters are available through the CLI. Use them if you need to customize resources, change the hosting model, or use a Key Protect key for BYOK encryption on the new instance. See the following example:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID> standard <REGION> -p
'{"backup_id":"BACKUP_ID","key_protect_key":"KEY_PROTECT_KEY_CRN", "members_disk_allocation_mb":"DESIRED_DISK_IN_MB", "members_host_flavor": "<VALUE>", "members_memory_allocation_mb":"DESIRED_MEMORY_IN_MB", "members_cpu_allocation_count":"NUMBER_OF_CORES"}'
```
{: .pre}

The `members_host_flavor` value can be either "multitenant" or an appropriate-sized Isolated Compute host (see [the list of available values](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli#hosting-models-iso-compute-sizing-cli)). Only specify `members_memory_allocation_mb` or `members_cpu_allocation_count` if you use "multitenant" hosting.
{: note}

A pre-formatted command for a specific backup is available in detailed view of the backup on the _Backups and restore_ tab of your instance's dashboard.
{: .tip}

By default, restoring from a backup provisions an instance with the preferred version of the database type, not the version of the instance you restore from. You can specify a version by adding the version in the parameters object, as in the following example.

```sh
`ibmcloud resource service-instance-create <INSTANCE_NAME> databases-for-mysql standard us-south -p '{"backup_id":"<BACKUP_ID>", "version": "<VERSION>"}'
```

To see a list of versions available, run `ibmcloud cdb deployables`.

### Restoring a backup through the API
{: #restore-backup-api}
{: api}

The [Resource Controller API](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api){: external} supports provisioning and restoring database instances. The create request is a `POST` to the [`/resource_instances`](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api) endpoint.

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
      "backup_id": "<BACKUP_ID>"
    }
  }'
```
{: .pre}

The parameters `name`, `target`, `resource_group`, and `resource_plan_id` are all required, and `backup_id` is the backup that you want to restore.
{: important}

* Change the value of `name` to the name that you want for your new instance.
* The `resource_plan_id` is the type of instance, such as _databases-for-postgresql_ or _messages-for-rabbitmq_.
* The `target` is the region where you want the new instance to be located, which can be a different region from the source instance. Cross-region restores are supported, except for restoring into or out of the `eu-de` region.
* `backup_id` is the backup that you want to restore.

The above command will restore a backup to a machine of the same configuration and on the same [hosting model](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli) as your original deployment.

#### Optional parameters
{: #hosting-model-api}
{: api}

Optional parameters are available through the API. Use them if you need to customize resources, change the hosting model, deploy to a specific version, or use a Key Protect key for BYOK encryption on the new instance.

If you need to adjust resources, add any of the optional parameters `key_protect_key`, `members_disk_allocation_mb`, `members_host_flavor`,  `members_memory_allocation_mb`, `members_cpu_allocation_count`, or `version` and their preferred values to the body of the request. See the following example:

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
      "backup_id": "<BACKUP_ID>",
      "members_host_flavor": "<members_host_flavor_value>",
      "version": "<VERSION_NUMBER>"
    }
  }'
```
{: .pre}

The `members_host_flavor` value can be either "multitenant" or an appropriate-sized Isolated Compute host (see [the list of available values](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli#hosting-models-iso-compute-sizing-cli)). Only specify `members_memory_allocation_mb` or `members_cpu_allocation_count` if you use "multitenant" hosting.
{: note}

By default, restoring from a backup provisions an instance with the preferred version of the database type, not the version of the instance you restore from. You can specify a version by adding a `version` value in the parameters object.
{: note}

### Restoring a backup through Terraform
{: #restore-backup-tf}
{: terraform}

Use Terraform to restore to a backup from an older version to a new version.

1. Set your `backup_id`. For more information, see [`backup_id`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#backup_id){: external}.
1. Set your `version` in the version attribute. For more information, see [`version`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database#version){: external}.

The code looks like:

```tf
resource "ibm_database" "<your-instance>" {
  name                                 = "<your_database_name>"
  service                              = "<service>"
  plan                                 = "<plan>"
  location                             = "<region>"
  version                              = "<version>"
  backup_id                            = "<backup_id>"
}
```
{: codeblock}

For more information, see the [{{site.data.keyword.databases-for}} Terraform Registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/database_backups){: external}.

## Backups and restoration
{: #backup-restoration}

* {{site.data.keyword.databases-for}} are not responsible for restoration, timeliness, or validity of said backups.
* Actions that you take as a user can compromise the integrity of backups, such as under-allocating memory and disk. Users can monitor that backups are successful by using the API, and periodically restore a backup to ensure validity and integrity. Users can retrieve the most recent-scheduled backup details from the [{{site.data.keyword.databases-for}} CLI plug-in](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-reference) and the [{{site.data.keyword.databases-for}} API](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api).
* As a managed service, {{site.data.keyword.databases-for}} monitors the state of your backups and can attempt to remediate when possible. If you encounter issues from which you cannot recover, contact support for more help.

## Backup locations
{: #backup-locations}

Gen 2 Backups are only in the region of the instance.

## Business continuity and disaster recovery
{: #backup-locations}

{{site.data.keyword.databases-for}} provides mechanisms to protect your data and restore service functions. For more information (including [Backup Storage Regions](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr&interface=ui#bc-dr-single-region-backups){: external}), see [Understanding business continuity and disaster recovery for {{site.data.keyword.databases-for}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr){: external}.



## Backups FAQ
{: #backup-faq-reference}

For frequently asked questions about backups, see the [Backups FAQ](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-faq-backups){: external}.
