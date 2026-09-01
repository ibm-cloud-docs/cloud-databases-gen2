---
copyright:
  years: 2025, 2026
lastupdated: "2026-09-01"

keywords: gen 2, pricing

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for Gen 2 {{site.data.keyword.databases-for}}
{: #pricing}

[Gen 2]{: tag-purple}


The charge for an {{site.data.keyword.databases-for}} instance is determined by the following five factors:

- Database: PostgreSQL, MongoDB
- Quantity of vCPU allocated per database instance member
- GB of RAM allocated per database instance member
- GB of disk storage allocated per database instance member
- Backup size and retention

| Database | Database type | Default configuration|
| --- | --- | --- |
| Databases for PostgreSQL | Relational | 2-member |
| Databases for MySQL | Relational | 2-member |
| Databases for MongoDB | Non-relational | 3-member |
| Databases for Redis | Non-relational (Key-value) | 2-member |
| Databases for Elasticsearch | Non-relational (Search and Analytics) | 3-member |
| Databases for RabbitMQ | Messaging | 3-member |
{: caption="Out of the box configurations per database" caption-side="bottom"}

Each database instance consists of two or three members, depending on the database type, with each member holding a copy of the data to provide resiliency and high availability. Gen 2 {{site.data.keyword.databases-for}} instances are only available with [Isolated compute](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui) hosting. Isolated compute offers a choice of standard vCPU x RAM resource profiles that are hosted on single-tenant compute instances for maximum workload isolation and security. Disk storage capacity per member is specified independently of the vCPU x RAM profile selected. Gen 2 deployments depend on regional availability, for more information, see [Isolated Compute sizing](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui#isolated-compute-sizing-ui).

## Compute profile options
{: #pricing-profile-options}

Gen 2 offers two types of compute profiles designed to meet different workload requirements, with consistent vCPU:RAM ratios across both options and storage configured independently:

- **Fixed profiles**: Predefined vCPU and RAM combinations that run on the newest available CPU generation, delivering the highest level of consistent and predictable performance.

   - Designed for workloads where performance consistency is critical
   - No variation in underlying CPU generation
   - Optimized for deterministic, production-grade environments

- **Flex profiles**: Predefined vCPU and RAM profiles designed to run across available CPU generations, with dynamic placement optimized for cost.

   - Aligned to a standard baseline level of CPU performance
   - May run on different hardware generations over time
   - Priced at a lower price point while maintaining predictable behavior

### Fixed profiles
{: #pricing-fixed-profiles}

| Host size | vCPU x RAM |
| --- | --- |
| 4x20 | 4 vCPU x 20 GB RAM |
| 8x40 | 8 vCPU x 40 GB RAM |
| 16x80 | 16 vCPU x 80 GB RAM |
| 32x160 | 32 vCPU x 160 GB RAM |
| 48x240 | 48 vCPU x 240 GB RAM |
{: caption="Fixed profile selections" caption-side="bottom"}

### Flex profiles
{: #pricing-flex-profiles}

| Host size | vCPU x RAM |
| --- | --- |
| 4x16 | 4 vCPU x 16 GB RAM |
| 8x32 | 8 vCPU x 32 GB RAM |
| 16x64 | 16 vCPU x 64 GB RAM |
| 32x128 | 32 vCPU x 128 GB RAM |
{: caption="Flex profile selections" caption-side="bottom"}

The total cost of your {{site.data.keyword.databases-for}} deployment will consist of the the cost of each vCPU x RAM profile, disk storage in GB and backup storage (for all members), prorated hourly.
{: note}

### Disk storage
{: #pricing-storage}

Disk storage is provisioned per member and billed based on the total allocated capacity (GB) across all members in a deployment.
{{site.data.keyword.databases-for}} uses IBM Cloud VPC Block Storage as the underlying storage layer. Storage capacity can be configured independently of the selected compute profile, allowing customers to scale storage based on workload requirements.

The available storage performance profile is determined by the region in which the service is deployed. Most regions support the latest generation of storage capabilities (SSD Defined Performance (`sdp`)), which provides more flexible and consistent performance characteristics. In Chennai - Airtel (`in-che`), Mumbai - Airtel (`in-mum`), Montreal (`ca-mon`), Frankfurt (`eu-de`), and Washington DC (`us-east`) regions, storage is delivered using standard profiles with predefined performance levels at 5 IOPS/GB. As a result, both storage performance characteristics and pricing varies by region, reflecting differences in the underlying storage infrastructure.

For customers with specific performance or compliance requirements, it is recommended to validate regional capabilities during deployment planning.

## Using the pricing calculator
{: #pricing-calc}

For pricing estimation, use the **Add to estimate** button on the provisioning page of each service. Input your total consumption across each data members into the calculator. This is equal to the number of members because your data is replicated to all members. For example, a 2-member {{site.data.keyword.databases-for}} deployment with 5 GB of disk on a 4 vCPU x 20 GB RAM profile would have a total bill for 10 GB of disk and the total cost of 2 members.

## Backups pricing for Gen 2 instances
{: #pricing-backup}

Gen 2 {{site.data.keyword.databases-for}} uses independent backups with a snapshot-based model. Pricing is aligned to the size of your provisioned database storage. Snapshots are block-level incremental copies, so you are billed based on how much data has changed since the last snapshot, not just the total size of your database.

By default, all Gen 2 {{site.data.keyword.databases-for}} provides a daily backup that is stored for 30 days. These backups, and any on-demand backups you make, all count toward the free allocation.

### Independent backups billing
{: #independent-backups-billing}

Independent backups are billed as separate service instances:

- Each backup instance appears as a separate line item in your billing statement.
- Free allocation applies per database deployment (not per backup).

- Manual deletion of backups stops billing immediately.

For more information about independent backups, see [Understanding independent backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-independent-backups).

## Backup storage
{: #pricing-storage}

### Free allocation
{: #pricing-storage-free}

- You receive free backup storage equal to the total provisioned disk size of your deployment.
- This includes both automated daily backups and manual (on-demand) snapshots.

To help manage variability in monthly charges, especially during failover events or update events, the free backup storage {{site.data.keyword.databases-for}} with every instance is for each member. This buffer ensures that when a failover or cluster update occurs, resulting in a switch in the database primary, it does not result in unexpected costs. In the rare case where there’s no update or failover activity during a given month, your usage may fall below the free allocation, and you'll be charged less accordingly. This approach gives you predictable pricing while still accounting for the realities of high availability.

- Example: If a 3-member {{site.data.keyword.databases-for}} deployment is provisioned with 100 GB of disk per member, you get 300 GB of backup storage included at no cost.

### Overage charges
{: #pricing-storage-overage}

- Overage is billed monthly and applies when your snapshot storage exceeds the included allocation.
- Total snapshot storage = (Initial single member snapshot * number of members) + (Daily change × 29 days).
- Any usage beyond the free allocation is charged at $0.095 per GB per month.

### Worked example, for a 3-member {{site.data.keyword.databases-for}} deployment with 100 GB of data per member
{: #pricing-example}

- Day 1: A full snapshot is taken from the current primary. This consumes 100 GB of snapshot storage.

This models the worst case scenario where the full snapshot is equal to the file system. In practice, especially for new databases (which will grow over time), the snapshot size is often smaller, reducing your backup bill.
{: note}

- Day 2-16: You write 10 GB of new data per day. Snapshots are incremental and only store changes. Over 15 days, this adds 150 GB, bringing total snapshot usage to 100 GB + 150 GB = 250 GB.
- Day 17: A failover occurs, and one secondary member becomes the new primary. A full snapshot is taken from this new primary, consuming another 100 GB. This uses up the remaining free allocation and brings total snapshot usage to 350 GB.
- Day 18-30: You continue writing 10 GB per day, adding 130 GB over 13 days.
- Total snapshot = 100 GB (initial) + 150 GB (incremental) + 100 GB (failover snapshot) + 130 GB (post-failover incremental) = 480 GB.
- Free allocation = 100 GB x 3 members = 300 GB.
- Overage = 480 GB - 300 GB  = 180 GB.
- Monthly charge = (480 GB - 300 GB) X $0.095 = $17.1.

### Pricing independent backups
{: #pricing-independent-backups}

The free backup storage allocation is equal to the total provisioned disk capacity of your deployment. The allocation is applied to backups created earlier in the month until the free allocation is exhausted. After the free allocation is exhausted, all additional backup storage is billed.

For example, if a three-member {{site.data.keyword.databases-for}} deployment is provisioned with 100 GB of disk capacity per member, you receive 300 GB of backup storage at no additional cost. The free allocation is applied to backups as follows:

Backup 1 is **80 GB**. The entire backup is covered by the free allocation, so the total charge is **$0.00**. The remaining free allocation is **220 GB**.
Backup 2 is **80 GB**. The entire backup is covered by the free allocation, so the total charge is **$0.00**. The remaining free allocation is **140 GB**.
Backup 3 is **80 GB**. The entire backup is covered by the free allocation, so the total charge is **$0.00**. The remaining free allocation is **60 GB**.
Backup 4 is **80 GB**. The remaining free allocation of **20 GB** is applied to the backup. The billable storage is **60 GB** (80 GB - 20 GB), resulting in a charge of **60 GB × $0.095 = $5.70**. The remaining free allocation is **0 GB**.
Backup 5 is **80 GB**. No free allocation remains. The entire backup is billable, resulting in a charge of **80 GB × $0.095 = $7.60**.
Backup 6 is **80 GB**. No free allocation remains. The entire backup is billable, resulting in a charge of **80 GB × $0.095 = $7.60**.

The free allocation applies only while the database instance is active. If the instance is disabled, any existing backups continue to exist but are fully billable and do not qualify for the free allocation. If backups remain after the database instance is deleted, those backups are also fully billable and do not qualify for the free allocation.

The monthly free allocation is calculated based on the total provisioned disk size at the time the first backup is created and does not change if the disk size is scaled later in the month. This allocation applies only to backups created in that same month and does not apply to backups from previous months.
{: note}

## Scaling per member
{: #scaling-member}

{{site.data.keyword.databases-for}} deployments have minimum and maximum allocation for disk and RAM as shown. Scaling deployments through the [UI](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui),  [API](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ap) and [CLI](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=cli). You can scale database storage up to 4 TB of disk per member, minimum and maximum CPU and RAM combinations vary per region, see [Isolated compute](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui#isolated-compute-sizing-ui).

| Resource | Minimum | Maximum | Scaling granularity |
| ---------- | ----- | ----- | ------- |
| Disk | 5 GB per member | 4 TB per member | 1024 MB per member |
| RAM | 16 GB | 240 GB | Isolated compute – Resource scaling with host sizes |
| CPU | 4 vCPU | 48 vCPU| Isolated compute – Resource scaling with host sizes |
{: caption="Scaling limits" caption-side="bottom"}

## Billing metrics reference
{: #pricing-metrics}
The following billing metrics are used to calculate charges for Gen 2 {{site.data.keyword.databases-for}} deployments.

| Component | Description |
| --- | --- |
| Compute | Defines the CPU and memory resources allocated to each database member. Available in a range of predefined host sizes, for example **HOST_FOUR_SIXTEEN_FLEX** provides **4 vCPUs and 16 GB RAM** per member. |
| Storage | Persistent database storage backed by IBM Cloud VPC Block Storage. Storage is provisioned using the **5 IOPS/GB performance tier** and billed based on allocated capacity using **GIGABYTE_HOUR_DISK_GEN2**. |
| Backups | Automated backups used for recovery and point-in-time restore. Backup storage is billed separately using **GIGABYTE_MONTH_BACKUP_GEN2**. |
{: caption="Core deployment components and billing dimensions" caption-side="bottom"}
