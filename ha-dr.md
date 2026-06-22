---

copyright:
  years: 2026
lastupdated: "2026-06-22"

subcollection: cloud-databases-gen2

keywords: HA for cloud-databases, DR for cloud-databases, high availability for cloud-databases, disaster recovery for cloud-databases, failover for cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability
{: #ha-dr}

[Gen 2]{: tag-purple}


This document reflects general availability for Gen 2 {{site.data.keyword.databases-for}}, which are progressively rolling out across new regions. You can track regional availability [here](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2).
{: .note}

## Regions
{: #regions-ha}

{{site.data.keyword.databases-for}} instances are deployed in either a multi-zone region (MZR), or a single-campus multizone region. Each instance is deployed in a highly available configuration; that is, data is replicated by each database onto one or more servers, making the data highly available during normal operations.

- In [MZRs](/docs/overview?topic=overview-locations#table-mzr), database members are distributed across different data centers, or zones.
- In [single-campus multizone regions](/docs/overview?topic=overview-locations#single-campus-mzr), database members are distributed across different hosts.

If a single-campus multizone region failure in an MZR or a hardware failure in any region occurs, your data is still accessible as it is replicated onto other fully functioning database servers. Such issues are addressed by {{site.data.keyword.cloud}} Specialists in place.

For more information on how your specific database replicates data among each of its members, see your {{site.data.keyword.databases-for}} documentation.

## Backups
{: #backups-ha}

- In addition to the high-availability configuration, for deployments in {{site.data.keyword.cloud}} multi-zone regions, your data is snapshotted and backed up daily by the {{site.data.keyword.databases-for}} platform and stored in [the same region as VPC Block Storage Snapshots](/docs/vpc?topic=vpc-snapshots-vpc-create&interface=ui).
- For most {{site.data.keyword.cloud}} single-campus multizone regions, your data is backed up locally in single-campus multizone region VPC Block Storage Snapshots.

Independent backups are currently available for {{site.data.keyword.databases-for-mongodb}}, {{site.data.keyword.databases-for-postgresql}}, and {{site.data.keyword.databases-for-mysql}} only. For more information about independent backups, see [Understanding independent backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-independent-backups).
{: note}

If a complete region failure occurs, the database servers in the region might not be accessible, but the backup data remains available. You can initiate a restore from these backups into an available region from the service management console. For more information, see the [{{site.data.keyword.databases-for}} backups documentation](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui).

It is your responsibility to [create a new service instance](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-gen2-offerings&interface=ui) in which to restore when the {{site.data.keyword.databases-for}} platform is restored. You are also responsible for testing the validity and restore time of your backups. For more information, see the [Disaster recovery section](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-bc-dr) in the *Shared responsibilities for Cloud Databases* page.

## Application-level high availability
{: #application-ha}

Applications that communicate over networks and cloud services are subject to transient connection failures. You want to design your applications to retry connections when errors are caused by a temporary loss in connectivity to your deployment or to {{site.data.keyword.cloud_notm}}.

Because {{site.data.keyword.databases-for}} is a managed service, regular updates and database maintenance occur as part of normal operations. Such maintenance can occasionally cause short intervals where your database is disabled.

Your applications must be designed to handle temporary interruptions to the database, implement error handling for failed database commands, and implement retry logic to recover from a temporary interruption.

Several minutes of database unavailability or connection interruptions are not expected. Open a [support ticket](https://cloud.ibm.com/unifiedsupport/cases/add) with details if you have time periods longer than a minute with no connectivity so we can investigate.

If you have deployments in more than one region, you must provision {{site.data.keyword.monitoringlong}} and enable platform metrics in each region. For more information, see [{{site.data.keyword.monitoringlong_notm}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-monitoring) integration.

## SLAs
{: #sla}

- See [How IBM Cloud ensures high availability and disaster recovery](/docs/resiliency?topic=resiliency-ha-redundancy) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}.
- All {{site.data.keyword.cloud}} Gen 2 Databases general availability (GA) offerings conform to the {{site.data.keyword.cloud}} [Service Level Agreement](/docs/overview?topic=overview-slas) (SLA) terms.
- For more information, see the [Responsibilities for Cloud Databases](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-responsibilities-cloud-databases) page.
