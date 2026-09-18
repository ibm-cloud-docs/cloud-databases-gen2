---

copyright:
  years: 2026
lastupdated: "2026-09-18"

subcollection: cloud-databases-gen2

keywords: independent backups, decoupled backups, backup lifecycle, backup management, cross-region backups, mysql backups

---

{{site.data.keyword.attribute-definition-list}}

# Managing independent backups
{: #independent-backups}

[Gen 2]{: tag-purple}

Independent backups are currently available only for {{site.data.keyword.databases-for-mysql}}, {{site.data.keyword.databases-for-postgresql}}, {{site.data.keyword.databases-for-mongodb}}, {{site.data.keyword.databases-for-elasticsearch}}

### Deleting an independent backup by using the CLI
{: #deleting-independent-backup-cli}
{: cli}

To delete an independent backup before its expiration, use the following command:

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

### Deleting an independent backup by using the API
{: #deleting-independent-backup-api}
{: api}

To delete an independent backup before its expiration, use the following command:

```sh
curl -X DELETE \
  https://resource-controller.cloud.ibm.com/v2/resource_instances/${INDEPENDENT_BACKUP_ID} \
  -H 'Authorization: Bearer <>'
```
{: pre}

Example:

```sh
curl -X DELETE \
  https://resource-controller.cloud.ibm.com/v2/resource_instances/793b4f27-7733-4803-917f-de8e055e2deb \
  -H 'Authorization: Bearer <>'
```
{: pre}

## Next steps
{: #independent-backups-next-steps}

- Learn about [backup pricing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-pricing#pricing-backup).
- Review [backup FAQs](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-faq#faq-backups).
- Understand [your responsibilities](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-responsibilities-cloud-databases) for managing backups.

## Transition from coupled backups
{: #migration-from-coupled}

The transition from coupled backups to independent backups varies by database service:

### Databases enabled with independent backups
{: #databases-with-independent-backups}

| Database           | Regions                                                                                  |
|--------------------|------------------------------------------------------------------------------------------|
| PostgreSQL         | `au-syd`, `ca-mon`, `eu-de`, `eu-es`, `in-che`, `in-mum`, `us-east`, `us-south`, `eu-gb` |
| MongoDB Enterprise | `au-syd`, `ca-mon`, `eu-de`, `eu-es`, `in-che`, `in-mum`, `us-east`, `us-south`, `eu-gb` |
| MongoDB Sharding   | `ca-mon`, `in-che`, `in-mum`, `us-east`                                                  |
| Elasticsearch      | `ca-mon`, `in-che`, `in-mum`, `eu-gb`                                                    |

| Redis              | `eu-gb`                                                                                  |
{: caption="Databases enabled with independent backups" caption-side="bottom"}

The databases listed in the table are transitioning from coupled backups to independent backups in the specified regions.

Independent backups will be enabled for applicable databases and regions in a phased approach.

During the 30-day transition period:

- Coupled backups and independent backups coexist.
- All new backups are created as independent backups.
- Existing coupled backups continue to function and are automatically deleted after 30 days.
- The UI displays both backup types.
- No action is required. The transition is handled automatically.
- After the 30-day transition period, only independent backups remain.

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
- On-demand backup on MySQL is not supported.
