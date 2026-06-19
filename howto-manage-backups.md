---

copyright:
  years: 2026
lastupdated: "2026-06-19"

keywords: backups, new deployment, source deployment, backup, back up, ondemand backup, on-demand backup, on-demand back up, instance

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Managing Gen 2 {{site.data.keyword.databases-for}} backups
{: #dashboard-backups}

[Gen 2]{: tag-purple}







Deleting a backup is permanent and cannot be undone. Ensure you no longer need the backup data before deletion.
{: important}

- Daily backup scheduling is not configurable.
- The backup inherits the same encryption as the database.
- Backups are restorable across accounts, but only through the API and only if the user that is running the restore has access to both the source and destination accounts.
- {{site.data.keyword.databases-for}} backups are not downloadable. If you need a local backup, use the appropriate software. For example, [pg_dump](https://www.postgresql.org/docs/9.6/static/backup-dump.html){: .external} is an effective tool for managing PostgreSQL backups.



### Taking an on-demand backup in the UI
{: #ondemand-backup-ui}
{: ui}

If you plan to make major changes to your instance, like scaling or removing databases, tables, collections, on-demand backups are useful. It can also be useful if you need to back up on a schedule. On-demand backups are kept for 30 days.

Instances come with backup storage equal to their total disk space at no cost. If your backup storage usage is greater than total disk space, each gigabyte is charged at an overage of $0.095/month. Backups are compressed, so even if you use on-demand backups, most instances do not exceed the allotted credit.
{: .tip}

To create a manual backup in the UI, go to the _Backups and restore_ tab of your instance then click **Create backup**. A message is displayed that a backup is in progress, and an on-demand backup is added to the list of available backups.

## Restoring a backup
{: #restore-backup}

Backups are restored to a new instance. After the new instance finishes provisioning, your data in the backup file is restored into the new instance.

By default, the new instance is auto-sized to the default disk size and same host size as the source instance at the time of the backup from which you are restoring. To adjust the resources that are allocated to the new instance, use the optional fields in the UI, CLI, or API to resize the new instance. Be sure to allocate enough for your data and workload; if the instance is not given enough resources or the backup contains more storage than the default disk size and a disk size is not specified, the restore fails.

Do not delete the source instance while the backup is restoring. Before you delete the old instance, wait until the new instance is provisioned and the backup is restored. Deleting an instance also deletes its backups.
{: .tip}

### Restoring a backup in the UI
{: #restore-backup-ui}
{: ui}

To restore a backup to a new service instance,

1. Click in the corresponding row to expand the options for the backup that you want to restore.
2. Click **Restore**.
3. On the **Provisioning** page, select from some available options.
    - You provide the name of the new service instance.
    - You can choose the initial resource allocation, either to expand or shrink the resources on the new instance. Note that if you decrease your resource amount, it may lead to provision failure or your database not functioning properly.
4. Click **Restore backup**. A "restore from backup started" message appears. Clicking **Your new instance is available now** takes you to your _Resources List_.

### Restoring a backup in the CLI
{: #restore-backup-cli}
{: cli}



The Resource Controller supports provisioning of database instances, and provisioning and restoring are the responsibility of the Resource Controller CLI. Use the [`resource service-instance-create`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_create) command.

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID>-gen2-<PLAN NAME> <REGION> -p  '{"dataservices":{"restore_backup_id":"<BACKUP_CRN>"}}'
```
{: .pre}

Example command

```sh
ibmcloud resource service-instance-create postgresql-restore-abc databases-for-postgresql databases-for-postgresql-gen2-standard ca-mon -p  '{"dataservices":{"restore_backup_id":"crn:v1:bluemix:public:databases-for-postgresql:ca-mon:a/26b19aex04da4475b6e31205fa93248d:a1e247d8-01c2-3bbe-a5e6-fdb5eb872d2f:backup:f689275f-7da9-4e90-9055-70b02c575492"}}'
```
{: .pre}

* Change the value of `instance_name` to the name that you want for your new instance.
* The `service-id` is the type of instance, such as _databases-for-postgresql_ or _databases-for-mongodb_.
* The `region` is where you want the new instance to be located, which can be a different region from the source instance.
* The `restore_backup_id` is the backup that you want to restore.

The previous command will restore a backup to a machine of the same configuration and on the same [hosting model](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli) as your original deployment.

#### Optional parameters
{: #restore-cli}
{: cli}

Optional parameters are available through the CLI. Use them if you need to customize resources, change the hosting model, or use a Key Protect key for BYOK encryption on the new instance. See the following example:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE-ID> gen2-<PLAN NAME> <REGION> -p
'{"restore_backup_id":"BACKUP_ID","key_protect_key":"KEY_PROTECT_KEY_CRN", "storage_gb":"DESIRED_DISK_IN_GB", "host_flavor": "<VALUE>"}'
```
{: .pre}

The `host_flavor` should be an appropriate-sized host. For more information, see [the list of available values](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui).
{: note}

A pre-formatted command for a specific backup is available in detailed view of the backup on the _Backups and restore_ tab of your instance's dashboard.
{: .tip}

By default, restoring from a backup provisions an instance with the preferred version of the database type, rather than the version of the source instance. Gen 2 {{site.data.keyword.databases-for}} currently support only one version per database. Over time, new versions are released. When a new version becomes available, you can move to that version by restoring from a backup.



### Restoring a backup through the API
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
{: .pre}



The parameters `name`, `target`, `resource_group`, and `resource_plan_id` are all required, and `restore_backup_id` is the backup that you want to restore.
{: important}

* Change the value of `name` to the name that you want for your new instance.
* The `resource_plan_id` is the type of instance, such as _databases-for-postgresql_ or _messages-for-rabbitmq_.
* The `target` is the region where you want the new instance to be located, which must be a Gen 2 region.
* The `restore_backup_id` is the backup that you want to restore.

The previous command will restore a backup to a machine of the same configuration and on the same [hosting model](/docs/databases-for-mongodb?topic=databases-for-mongodb-hosting-models&interface=cli) as your original deployment.

#### Optional parameters in the API
{: #restore-api}
{: api}

Optional parameters are available through the Resource Controller API. Use them if you need to customize resources, change the host size, deploy to a specific version, or use a Key Protect key for BYOK encryption on the new instance.

If you need to adjust resources, add any of the optional parameters `key_protect_key`, `storage_gb`, `host_flavor` or `version` and their preferred values to the body of the request. See the following example:

```sh
curl -X POST \
  https://resource-controller.cloud.ibm.com/v2/resource_instances \
  -H 'Authorization: Bearer <>' \
  -H 'Content-Type: application/json' \
```



## Business continuity and disaster recovery
{: #backup-locations}

{{site.data.keyword.databases-for}} provides mechanisms to protect your data and restore service functions. For more information (including [Backup Storage Regions](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr&interface=ui#bc-dr-single-region-backups){: external}), see [Understanding business continuity and disaster recovery for {{site.data.keyword.databases-for}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr){: external}.
