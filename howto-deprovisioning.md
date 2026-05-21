---

copyright:
  years: 2026
lastupdated: "2026-05-21"

subcollection: cloud-databases-gen2

keywords: deprovision cloud databases, databases with terraform, deprovisioning parameters, delete cloud databases, soft delete

---

{{site.data.keyword.attribute-definition-list}}

# Deleting your deployment and removing your data
{: #deprovisioning}

[Gen 2]{: tag-purple}


When an {{site.data.keyword.cloud}} Databases deployment is deleted, it is put in a soft-deleted state for 3 days after which it is removed. Soft-deleted deployments can be recovered by following the steps below.

After the 3-day soft-deletion period has ended, or if a hard deletion is issued, deployments are no longer recoverable.
{: note}

## Deleting your deployment in the user interface
{: #delete-deployment-ui}
{: ui}

To delete your deployment from the Resource list section dashboard of the {{site.data.keyword.cloud}} dashboard, select your deployment. Then, in the overflow menu ![Stacked three dots icon](images/stacked-three-dots.png) click **Delete service** from the drop-down list.

## Restoring a soft-deleted instance using the UI
{: #restore-deployment-ui}
{: ui}

Soft-deleted instances must be restored using the [CLI](/docs/databases-for-mysql?topic=databases-for-mysql-dashboard-backups&interface=cli#restore-backup-cli).

## Deleting your deployment using the CLI
{: #delete-deployment-cli}
{: cli}

By using the CLI, you can delete your existing {{site.data.keyword.cloud}} Databases deployment with the [`ibmcloud resource service-instance-delete`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_service_instance_delete) command:

```sh
ibmcloud resource service-instance-delete <INSTANCE_NAME_OR_CRN>
```
{: .pre}

You can further hard-delete an instance by using `ibmcloud resource reclamations` to list soft-deleted instances, followed by `ibmcloud resource reclamation-delete <RECLAMATION ID>` to hard-delete it.

Instances hard-deleted by `ibmcloud resource reclamation-delete` are unrecoverable and cannot be restored.
{: .important}

## Restoring a soft-deleted instance using the CLI
{: #restore-deployment-cli}
{: cli}

You can use the following command to list the soft-deleted instances that are available for reclamation:

```sh
ibmcloud resource reclamations
```
{: .pre}

Then, use the following command to recover them:

```sh
ibmcloud resource reclamation-restore <RECLAMATION ID>
```
{: .pre}

Restoring an {{site.data.keyword.cloud}} Databases deployment from a soft-deleted state may take several hours.
{: .note}

## Cryptoshredding keys
{: #cryptoshred}



{{site.data.keyword.keymanagementserviceshort}} provides cryptoshredding, which is [deletion](/docs/key-protect?topic=key-protect-delete-keys) of a key that is in use by {{site.data.keyword.cloud}} services, including your {{site.data.keyword.databases-for}} deployments.

Cryptoshredding is a destructive action. When the key is deleted, your data is unrecoverable even from a soft delete state.
{: .important}

## Backups removal
{: #backup-remove}

The behavior of backup deletion depends on the backup type:

### Independent backups
{: #independent-backup-removal}

Independent backups persist after the database instance is deleted and must be deleted separately if desired. To manually delete an independent backup:

```sh
ibmcloud resource service-instance-delete <BACKUP_CRN> --force
```
{: pre}

You can view all independent backups in the [Database Hub](https://cloud.ibm.com/databases/hub) under the **Independent backups** tab to identify backups whose source instance has been deleted.

### Coupled backups (legacy)
{: #coupled-backup-removal}

Coupled backups are automatically deleted when the database instance is deleted. These backups cannot be manually deleted.

For more information about backup types, see [Understanding independent backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-independent-backups).
