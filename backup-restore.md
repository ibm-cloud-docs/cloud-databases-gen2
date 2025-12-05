---

copyright:
  years: 2025
lastupdated: "2025-12-05"

subcollection: cloud-databases-gen2

keywords: backup, snapshot

---

{{site.data.keyword.attribute-definition-list}}

# Comparison of Gen 1 and Gen 2 backups
{: #comparison-backups}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

Backups with Gen 1 instances and backups (snapshots) with Gen 2 instances differ in both scope and mechanism. Traditional backups (Gen 1) operate at the file level, capturing database files and write-ahead logs (WAL). This method relies on deep integration with the database engine to ensure transactional consistency and data integrity. In contrast, Gen 2 uses infrastructure-level snapshots, leveraging IBM VPC’s block storage capabilities. These snapshots create near-instant volume-level copies that are fast, scalable, and minimally impact performance, even for large datasets. Similar to Gen 1 backups, every instance has scheduled backups that are automatically run daily during backup windows. You can view a list of backups for your instances and trigger on-demand backups and it is possible to restore backups into new instances. Backups are automatically deleted after 30 days.

Gen 1 backups can be used to restore a Gen 2 instance. Gen 2 instances cannot be used to restore a Gen 1 instance because the volume snapshot restoration process requires complete block-level images rather than individual database files.

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
| Cross-region restore | Supported| Not supported as a built-in capability. Gen 2 instances can only be restored in regions they were created in, therefore the backup must be manually copied or automatically configured to copy to the target Gen 2 region or before any restore operation can be performed there. This is due to how backups are managed and stored at the infrastructure and storage-layer level, which is region specific. |
{: caption="Key feature differences between Gen 1 and Gen 2" caption-side="bottom"}



## Managing Gen 2 backups
{: #managing-backups}

To find out how to manage your Gen 2 backup, visit [Managing {{site.data.keyword.databases-for}} backups](//docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui).
