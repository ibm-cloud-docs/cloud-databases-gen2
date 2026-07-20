---
copyright:
  years: 2025, 2026
lastupdated: "2026-07-20"

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
| Databases for MongoDB | Non-relational | 3-member |
{: caption="Out of the box configurations per database " caption-side="bottom"}

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



## Scaling per member
{: #scaling-member}

{{site.data.keyword.databases-for}} deployments have minimum and maximum allocation for disk and RAM as shown. Scaling deployments through the [UI](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui),  [API](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ap) and [CLI](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=cli). You can scale database storage up to 4 TB of disk per member, minimum and maximum CPU and RAM combinations vary per region, see [Isolated compute](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui#isolated-compute-sizing-ui).

| Resource | Minimum | Maximum | Scaling granularity |
| ---------- | ----- | ----- | ------- |
| Disk | 5 GB per member | 4 TB per member | 1024 MB per member |
| RAM | 16 GB | 240 GB | Isolated compute – Resource scaling with host sizes |
| CPU | 4 vCPU | 48 vCPU| Isolated compute – Resource scaling with host sizes |
{: caption="Scaling limits" caption-side="bottom"}
