---
copyright:
  years: 2025
lastupdated: "2025-10-23"

keywords: gen 2, pricing

subcollection: cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# Pricing for Gen 2 Databases
{: #pricing}

The charge for an {{site.data.keyword.databases-for}} instance is determined by the following four factors:

- Database type: PostgreSQL, MongoDB
- Quantity of vCPU allocated per database instance member
- GB of RAM allocated per database instance member
- GB of disk storage allocated per database instance member

Each database instance consists of two or three members, depending on the database type, with each member holding a copy of the data to provide resiliency and high availability. {{site.data.keyword.databases-for}} instances are only available with [Isolated compute](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui) hosting. Isolated compute offers a choice of six standard vCPU x RAM resource profiles that are hosted on single-tenant compute instances for maximum workload isolation and security. Disk storage capacity per member is specified independently of the vCPU x RAM profile selected. Gen 2 deployments start with 4 vCPU x 16 GB RAM profiles as the smallest and 48 vCPU x 240 GB RAM as the largest profiles, depending on [regional availability](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui#isolated-compute-sizing-ui).

| Host size | vCPU x RAM | Best for |
| --- | --- | --- |
| 4x16 | 4 vCPU x 16 GB RAM | Getting started |
| 8x32 | 8 vCPU x 32 GB RAM | |
| 8x64 | 8 vCPU x 64 GB RAM | Memory intensive usage |
| 16x64 | 16 vCPU x 64 GB RAM | |
| 32x128 | 32 vCPU x 128 GB RAM | |
| 30x240 | 30 vCPU x 240 GB RAM | Memory intensive usage |
{: caption="Isolated compute UI selections" caption-side="bottom"}

The total cost of your {{site.data.keyword.databases-for}} deployment will consist of the the cost of each vCPU x RAM profile, disk storage in GB and backup storage (for all members), prorated hourly. 
{: note}

## Using the pricing calculator
{: #pricing-calc}

For pricing estimation, use the **Add to estimate** button on the catalog page of each service. Input your total consumption across each data members into the calculator. This is equal to the number of members because your data is replicated to all members. For example, a 2 member PostgreSQL deployment with 5 GB of disk on a 4 vCPU x 20 GB RAM profile would have a total bill for 10 GB of disk and the total cost of 2 members. 

## Backups pricing for Gen 2 instances
{: #pricing-backup}

Gen 2 {{site.data.keyword.databases-for}} uses a snapshot based backup model, with pricing aligned to the size of your provisioned database storage. Snapshots differ from native backups in that they are block-level incremental copies, therefore you are billed based on how much data has changed since the last snapshot, not just the total size of your database. 

By default, all Gen 2 {{site.data.keyword.databases-for}} provides a daily backup that is stored for 30 days. These backups, and any on-demand backups you make, all count toward the above allocation.

## Backup storage
{: #pricing-storage}

### Free allocation
{: #pricing-storage-free}

- You receive free backup storage equal to the total provisioned disk size of your deployment.
- This includes both automated daily backups and manual (on-demand) snapshots.

To help manage variability in monthly charges, especially during failover events or update events, the free backup storage {{site.data.keyword.databases-for}} with every instance is for each member. This buffer ensures that when a failover or cluster update occurs, resulting in a switch in the database primary, it does not result in unexpected costs. In the rare case where there’s no update or failover activity during a given month, your usage may fall below the free allocation, and you'll be charged less accordingly. This approach gives you predictable pricing while still accounting for the realities of high availability.

- Example: If a 2-member {{site.data.keyword.databases-for-postgresql}} deployment is provisioned with 100 GB of disk per member, you get 200 GB of backup storage included at no cost.

### Overage charges
{: #pricing-storage-overage}

- Overage is billed monthly and applies when your snapshot storage exceeds the included allocation. 
- Total snapshot storage = (Initial single member snapshot * number of members) + (Daily change × 29 days).
- Any usage beyond the free allocation is charged at $0.095 per GB per month.

### Worked example, for a 2-member PostgreSQL deployment with 100 GB of data per member
{: #pricing-example}

- Day 1: A full snapshot is taken from the current primary. This consumes 100 GB of snapshot storage. 

This models the worst case scenario where the full snapshot is equal to the file system. In practice, especially for new databases (which will grow over time), the snapshot size is often smaller, reducing your backup bill. 
{: note} 

- Day 2-16: You write 10 GB of new data per day. Snapshots are incremental and only store changes. Over 15 days, this adds 150 GB, bringing total snapshot usage to 100 GB + 150 GB = 250 GB. 
- Day 17: A failover occurs, and the secondary becomes the new primary. A full snapshot is taken from this new primary, consuming another 100 GB. This uses up the remaining free allocation and brings total snapshot usage to 350 GB.
- Day 18-30: You continue writing 10 GB per day, adding 130 GB over 13 days. 
- Total snapshot = 100 GB (initial) + 150 GB (incremental) + 100 GB (failover snapshot) + 130 GB (post-failover incremental) = 480 GB.
- Free allocation = 100 GB x 2 members = 200 GB.
- Overage = 480 GB - 200 GB  = 280 GB.
- Monthly charge = (480 GB - 200 GB) X $0.095 = $26.6. 
- With large deployments and frequent writes, you’re more likely to exceed the free tier after the first snapshot, and your snapshot storage costs will grow quickly.
- Cross-region copies: If you choose to copy snapshots to another region, {{site.data.keyword.databases-for}} charges for the full size of the snapshot in the destination region and continued incremental growth in the original region as new snapshots are taken.

## Scaling per member
{: #scaling-member}

{{site.data.keyword.databases-for-postgresql}} deployments have minimum and maximum allocation for disk and RAM as shown. Scaling deployments through the API and CLI provides more granularity and also allows you to scale a database instance up to 4 TB of disk per member. Minimum and maximum CPU and RAM combinations vary per region, see [Isolated compute](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-isolated-compute&interface=ui#isolated-compute-sizing-ui). 

| Resource | Minimum | Maximum | Scaling granularity (API/CLI) |
| ---------- | ----- | ----- | ------- |
| Disk | 5 GB per member | 4 TB per member | 1024 MB per member |
| RAM | 16 GB | 240 GB | Isolated compute – Resource scaling with host sizes |
| CPU | 4 vCPU | 48 vCPU| Isolated compute – Resource scaling with host sizes |
{: caption="Scaling limits" caption-side="bottom"}
