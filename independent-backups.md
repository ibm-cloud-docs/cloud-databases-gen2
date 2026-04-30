---

copyright:
  years: 2026
lastupdated: "2026-04-30"

subcollection: cloud-databases-gen2

keywords: independent backups, decoupled backups, backup lifecycle, backup management, cross-region backups

---

{{site.data.keyword.attribute-definition-list}}

# Understanding Independent Backups
{: #independent-backups}

[Gen 2]{: tag-purple}

Independent Backups represent a fundamental shift in how {{site.data.keyword.databases-for}} Gen 2 manages backup data. Unlike traditional backups that are tightly coupled to your database instance lifecycle, Independent Backups exist as separate, provisionable service instances with their own lifecycle, allowing you to retain backup data even after the source database instance is deleted.
{: shortdesc}

## What are Independent Backups?
{: #what-are-independent-backups}

Independent Backups (formerly known as "Decoupled Backups") are backup instances that operate independently from your database service instances. Each Independent Backup is a fully managed service resource with its own:

- Service name and Cloud Resource Name (CRN)
- Lifecycle management through {{site.data.keyword.cloud_notm}} Resource Controller
- Billing and resource tracking
- Access control and permissions

This architecture provides greater flexibility in managing your backup data, enabling use cases such as long-term data retention, compliance requirements, and disaster recovery scenarios where the source database may no longer exist.

## Key differences from coupled backups
{: #independent-vs-coupled}

| Feature | Coupled Backups (Legacy) | Independent Backups |
|---------|-------------------------|---------------------|
| Lifecycle | Tied to database instance | Independent of database instance |
| Persistence | Deleted when instance deleted | Persist after instance deletion |
| Management | Database-specific APIs | {{site.data.keyword.cloud_notm}} Resource Controller |
| Visibility | Instance UI only | Database Hub, Resource List, Instance UI |
| Deletion | Automatic only (30 days) | Manual and automatic |
| Cross-region copies | Not supported | Supported (Q2 2026) |
| Provisioning | Automatic only | Automatic and on-demand |
| Billing | Included with instance | Separate service billing |
{: caption="Comparison of coupled and independent backups" caption-side="bottom"}

## How Independent Backups work
{: #how-independent-backups-work}

### Automatic backup creation
{: #automatic-backup-creation}

When you provision a Gen 2 {{site.data.keyword.databases-for}} instance, the system automatically creates Independent Backup instances for your daily scheduled backups. These backups:

- Are created daily according to your backup schedule
- Persist for 30 days by default
- Are managed automatically by the service
- Appear in your Resource List and Database Hub

### On-demand backup creation
{: #ondemand-backup-creation}

You can create on-demand Independent Backups at any time using the {{site.data.keyword.cloud_notm}} Resource Controller. These backups:

- Are created immediately upon request
- Follow the same retention policies as automatic backups
- Can be manually deleted before expiration
- Are useful before major changes or migrations

### Backup lifecycle
{: #backup-lifecycle}

Independent Backups follow this lifecycle:

1. **Provisioning**: Backup instance is created (automatically or on-demand)
2. **Active**: Backup is available for restore operations
3. **Expiration**: Backup reaches end of retention period (30 days default)
4. **Deletion**: Backup is automatically deleted or manually removed

Unlike coupled backups, Independent Backups can be manually deleted at any time through the Resource Controller, giving you greater control over your backup data and associated costs.

## Viewing Independent Backups
{: #viewing-independent-backups}

Independent Backups can be viewed in multiple locations:

### Database Hub
{: #database-hub-view}

The Database Hub provides a centralized view of all backups across your account:

- **Backups tab**: Shows backups whose source database instance still exists
- **Independent Backups tab**: Shows backups whose source database instance has been deleted

This separation helps you quickly identify orphaned backups that may need attention or cleanup.

### Resource List
{: #resource-list-view}

Independent Backups appear as separate service instances in your {{site.data.keyword.cloud_notm}} Resource List, allowing you to:

- View backup details and metadata
- Manage backup lifecycle
- Track backup costs
- Apply resource tags and labels

### Instance Backups and Restore tab
{: #instance-view}

Within your database instance UI, the Backups and Restore tab shows all backups (both coupled and independent) associated with that specific instance.

## Managing Independent Backups
{: #managing-independent-backups}

### Creating an Independent Backup
{: #creating-independent-backup}

To create an on-demand Independent Backup using the CLI:

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
  my-postgres-backup-20260429 \
  databases-for-postgresql-backup \
  standard \
  us-east \
  -g Default \
  -p '{
    "dataservices": {
      "source_dataservice_crn": "crn:v1:bluemix:public:databases-for-postgresql:us-east:a/1234567890:abcd-1234-efgh-5678::"
    }
  }'
```
{: pre}

### Deleting an Independent Backup
{: #deleting-independent-backup}

To manually delete an Independent Backup before its expiration:

```sh
ibmcloud resource service-instance-delete <BACKUP_CRN> --force
```
{: pre}

Example:

```sh
ibmcloud resource service-instance-delete e318275d-f860-4e4e-a63b-271fb4400c26 --force
```
{: pre}

Deleting a backup is permanent and cannot be undone. Ensure you no longer need the backup data before deletion.
{: important}

### Restoring from an Independent Backup
{: #restoring-independent-backup}

Independent Backups can be restored to a new database instance even if the source instance no longer exists. For detailed restore instructions, see [Restoring a backup](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups#restore-backup).

## Cross-region backup copies
{: #cross-region-copies}

Starting in Q2 2026, you can create copies of Independent Backups in different {{site.data.keyword.cloud_notm}} regions for enhanced disaster recovery and compliance requirements.

### Creating a cross-region copy
{: #creating-cross-region-copy}

To copy an Independent Backup to a different region:

```sh
ibmcloud resource service-instance-create \
  <BACKUP_COPY_NAME> \
  <BACKUP_SERVICE_NAME> \
  <BACKUP_SERVICE_PLAN_NAME> \
  <TARGET_REGION> \
  -g <RESOURCE_GROUP> \
  -p '{
    "dataservices": {
      "source_backup_crn": "<SOURCE_BACKUP_CRN>",
      "encryption": {
        "disk": "<KEY_PROTECT_KEY_CRN>"
      }
    }
  }'
```
{: pre}

### Cross-region copy considerations
{: #cross-region-considerations}

- Copies can only be created in allowed Gen 2 regions
- Each copy is billed as a separate backup instance
- You can specify a different encryption key for the target region
- Bulk copying is not supported; copies must be created individually
- Automatic cross-region replication can be configured at the database instance level

## Migration from coupled backups
{: #migration-from-coupled}

{{site.data.keyword.databases-for}} is transitioning from coupled backups to Independent Backups. During the migration period:

### Coexistence period
{: #coexistence-period}

For 30 days after the Independent Backups feature launch, both backup types will coexist:

- **Existing coupled backups**: Continue to function as before and will be automatically deleted after 30 days
- **New Independent Backups**: All new backups are created as Independent Backups
- **UI support**: The UI displays both backup types during this transition

### What you need to do
{: #migration-actions}

1. **Review your backups**: Check the Database Hub to see all your backups
2. **Update automation**: If you have scripts or automation that manage backups, update them to use Resource Controller commands
3. **Plan for cleanup**: After 30 days, all coupled backups will be automatically deleted
4. **Test restores**: Verify that you can restore from Independent Backups

No action is required for automatic backups; the system handles the transition automatically.
{: note}

## Billing for Independent Backups
{: #independent-backups-billing}

Independent Backups are billed as separate service instances:

- **Free allocation**: You receive free backup storage equal to the total provisioned disk size of your database deployment
- **Overage charges**: Usage beyond the free allocation is charged at $0.095 per GB per month
- **Cross-region copies**: Each copy in a different region is billed separately based on its size
- **Billing visibility**: Backup costs appear as separate line items in your billing statement

For detailed pricing information, see [Pricing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-pricing#pricing-backup).

## Security and compliance
{: #security-compliance}

Independent Backups maintain the same security standards as your database instances:

- **Encryption at rest**: All backups are encrypted using either IBM-managed keys or your own keys via Key Protect or Hyper Protect Crypto Services
- **Encryption in transit**: Data is encrypted during backup creation and restore operations
- **Access control**: IAM policies control who can create, view, and restore backups
- **Audit logging**: All backup operations are logged to {{site.data.keyword.atracker_full_notm}}

## Limitations and restrictions
{: #limitations}

Be aware of the following limitations:

- Bulk operations (bulk copy, bulk delete) are not supported
- Cross-region copies can only be created in allowed Gen 2 regions
- Independent Backups cannot be downloaded; use database-specific tools (e.g., `pg_dump`) for local backups
- Backup retention policies are not yet configurable (30 days default)
- CLI and Terraform support is available; UI support is in development

## Next steps
{: #next-steps}

- [Managing {{site.data.keyword.databases-for}} backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups)
- [Understanding business continuity and disaster recovery](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr)
- [Backups FAQ](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-faq-backups)
