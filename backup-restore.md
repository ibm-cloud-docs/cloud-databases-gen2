---

copyright:
  years: 2026
lastupdated: "2026-06-19"

subcollection: cloud-databases-gen2

keywords: backup, snapshot

---

{{site.data.keyword.attribute-definition-list}}

# Comparison of Gen 1 and Gen 2 backups
{: #comparison-backups}

[Gen 2]{: tag-purple}


Backups with Gen 1 instances and backups (snapshots) with Gen 2 instances differ in both scope and mechanism. Traditional backups (Gen 1) operate at the file level, capturing database files and write-ahead logs (WAL). This method relies on deep integration with the database engine to ensure transactional consistency and data integrity. In contrast, Gen 2 uses infrastructure-level snapshots, leveraging IBM VPC's block storage and file share capabilities. These snapshots create near-instant volume-level copies that are fast, scalable, and minimally impact performance, even for large datasets. Similar to Gen 1 backups, every instance has scheduled backups that are automatically run daily during backup windows. You can view a list of backups for your instances and trigger on-demand backups and it is possible to restore backups into new instances.

Gen 2 offers two types of backups: coupled backups (for most services) and independent backups (currently available only for {{site.data.keyword.databases-for-postgresql}}, {{site.data.keyword.databases-for-mongodb}}, and {{site.data.keyword.databases-for-mysql}}). Independent backups are separate service instances that persist after database deletion, while coupled backups are tied to the database instance lifecycle.

Gen 2 instances cannot be used to restore a Gen 1 instance because the volume snapshot restoration process requires complete block-level images rather than individual database files.

## Key feature differences between Gen 1 and Gen 2
{: #differences}

| Differentiator | Gen 1 | Gen 2 |
|----------------|-------|-------|
| Mechanism | File-level backups: Backups are file-level backups performed by copying individual database files and WAL segments, with checksums calculated for every file in the backup and rechecked during restore or verify operations. The backup mechanism works at the product application level, requiring deep integration with the database engine to ensure transactional consistency and data integrity. | Infrastructure-level backups: Backups leverage infrastructure-level volume snapshots that capture the entire storage state at the block-level, significantly reducing backup windows from hours to minutes even for multi-terabyte databases. This approach provides near-instantaneous backup creation regardless of database size. |
| Performance | Affects database process performance by consuming CPU and memory resource. | Backups operate independently from the database process, thus not affecting the databases’ CPU and RAM consumption. |
| Access to restores | Delayed access to restores. Backups require complete file restoration before database startup. No access during the restoration window. | Immediate access to restores with decreased IO performance until hydration completes. [Restoring a volume from snapshot](/docs/vpc?topic=vpc-snapshots-vpc-restore&amp;interface=ui#snapshots-vpc-restore). |
| Recovery Time Objective (RTO) | Slower RTO. Restoring access to the data scales almost linearly as data volume grows and that can take hours for large databases. | Fast RTO: Restoring access to data takes only minutes and is independent of data volume. However, I/O performance may temporarily degrade during the restore process, with the impact scaling based on data size. |
| Recovery Point Objective (RPO) | Scheduled at fixed intervals creating potential data loss windows. | Can be taken frequently with minimal performance impact. |
| Point-in-time recovery (PITR)| Yes | Future release. |
{: caption="Key feature differences between Gen 1 and Gen 2" caption-side="bottom"}

## Independent backups features
{: #independent-backups-features}

Gen 2 introduces independent backups for {{site.data.keyword.databases-for-postgresql}}, {{site.data.keyword.databases-for-mongodb}}, and {{site.data.keyword.databases-for-mysql}}, which provide additional capabilities beyond traditional coupled backups:

| Feature | Gen 1 | Gen 2 (Coupled) | Gen 2 (Independent) |
|---------|-------|-----------------|---------------------|
| Lifecycle | Coupled to instance | Coupled to instance | Independent of instance |
| Account level views | Not supported | Not supported | Database Hub with centralized view |
| Backup deletion | Automatic only | Automatic only | Manual and automatic |
| Backup locality | Fixed | Region-locked | Region-locked, future release to support backup copy |
| Persistence | Deleted with instance | Deleted with instance | Persists after instance deletion |
| Management | Database APIs | Database APIs | Resource Controller |
{: caption="Independent backups feature comparison" caption-side="bottom"}

Independent backups are currently available only for {{site.data.keyword.databases-for-postgresql}}, {{site.data.keyword.databases-for-mongodb}}, and {{site.data.keyword.databases-for-mysql}}. All other Gen 2 services use coupled backups.
{: important}

For more information about independent backups, see [Understanding independent backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-independent-backups).


## Managing Gen 2 backups
{: #managing-backups}

To find out how to manage your Gen 2 backups:

- For {{site.data.keyword.databases-for-postgresql}}, {{site.data.keyword.databases-for-mongodb}}, and {{site.data.keyword.databases-for-mysql}}, see [Managing independent backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-independent-backups).
- For all other Gen 2 services, see [Managing backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups).
