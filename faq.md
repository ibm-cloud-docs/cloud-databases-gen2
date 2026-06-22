---

copyright:
  years: 2026
lastupdated: "2026-06-22"

keywords: ICD Gen 2 FAQ

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} Gen 2 – Frequently Asked Questions (FAQ)
{: #faq}
{: faq}
{: support}

[Gen 2]{: tag-purple}

## Overview
{: #faq-overview}

{{site.data.keyword.databases-for}} Gen 2 is built on **IBM Cloud VPC infrastructure**, replacing the older Classic infrastructure used by Gen 1 services. VPC provides stronger performance, enhanced security, modernized networking, and better operational controls for managed databases.

This FAQ summarizes the key differences for {{site.data.keyword.databases-for}} Gen 2 (VPC) and how it differs from the Classic (Gen 1) version.

---
### 1. What is the biggest difference between Classic and Gen 2?
{: #faq-1}

Classic services run on IBM's Original **Classic Platform**, while Gen 2 runs on **VPC (Virtual Private Cloud)** with software-defined networking.

#### Classic Gen 1 vs VPC Gen 2: Architectural differences
{: #faq-1-differences}

| Area | Classic | Gen 2 |
|------|------------------|--------------|
| **Infrastructure** | VLAN-based Classic data-center model | Modern, software-defined VPC regional model |
| **Performance** | Network speeds up to ~50 Gbps | Network speeds up to 200 Gbps |
| **Zone architecture** | Limited use of zone architecture | Strong multi-zone availability |
| **Security** | Older networking/security approach | VPEs, IAM-native integration, modern cloud networking |
| **Provisioning** | Less flexibile provisioning model, slower to modify | Fast, API/CLI/Terraform-first model |
| **Scaling** | Fixed instance profiles with Isolated and Shared Compute models| Faster, more flexible scaling with modern isolated compute profiles  |
{: caption="Key differences" caption-side="bottom"}


### 2. Why should I choose Gen 2?
{: #faq-2}

Gen 2 provides:

- Modern networking with higher throughput.
- Better multi-zone availability.
- Stronger security with Private only connections and IAM integration.
- Faster provisioning and automation alignment.
- Long-term strategic alignment with {{site.data.keyword.cloud}}

### 3. Does Gen 2 have any limitations compared to Classic?
{: #faq-3}

Yes, the following limitations exist at this point:

- Montreal, Chennai, and Mumbai region only.
- Context-based restrictions (CBR) is not yet supported.

### 4. Do Gen 2 databases support the same features as Gen 1?
{: #faq-4}

Gen 2 supports the same core database engines and delivers improved performance, security, and operational capabilities on VPC. Some Gen 1 features and use cases are still being added to Gen 2 as the platform expands, but coverage is increasing rapidly. Most workloads will run normally on Gen 2 today, and full use case parity will continue to grow over time. To track the differences between Gen 1 and Gen 2 Databases, check out the [Overview page](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2).


### 5. Are there differences in hosting models between Gen 1 and Gen 2?
{: #faq-5}

Gen 2 instances currently offer fixed, Isolated Compute profiles only. These profiles run on newer hardware built on 4th Gen Intel® Xeon® Scalable processors (Sapphire Rapids).

Gen 1 instances use a previous generation of hardware (Intel® Xeon® Platinum 8260 Cascade Lake) and support both shared and isolated hosting models.

The following table explains the differences between Shared Compute and Isolated Compute in Gen 1.

|  Shared Compute (multi-tenant) | Isolated Compute (single-tenant)|
|---------------|------------------|
| - Flexible CPU/RAM selections <br> - Small or custom presets <br> - Ideal for dev/test or cost-efficient workloads | - Dedicated compute <br> - Best for production workloads requiring isolation |
{: caption="Differences in hosting models" caption-side="bottom"}


### 6. How does performance differ between Classic and Gen 2?
{: #faq-6}

Gen 2 is built on newer underlying infrastructure that provides higher baseline capabilities, such as:

- Up to 200 Gbps networking.
- Improved CPU/memory profiles.
- IOPS-based scalable storage performance.
- Higher bandwidth with dedicated bandwidth for storage.
- Lower latency on the network level.
- Ability to select the CPU generation.
- Snapshot-based backups that do not impact database performance.
- Restores in the background while you can use the database. Thus, restore times are less dependent on database size.

However, application-level performance improvements will vary depending on workload characteristics, data access patterns and service configuration. While Gen 2 offers a more powerful platform, performance outcomes are not guaranteed and may differ based on your specific workload.


### 7. What about security differences?
{: #faq-7}

Gen 2 delivers:

- Private only access via Virtual Private Endpoints (VPEs).
- Cloud-native networking (VPN, LBaaS, NAT).
- Unified IAM integration.
- Consistent encryption at rest/in transit.


### 8. Does Gen 2 change backup and restore capabilities?
{: #faq-8}

Yes, with:

- Snapshot-based bakups.
- Enhanced point-in-time recovery (PITR).
- More performant and predictable backup and restore performance due to newer Gen 2 storage architecture.

For more information, see [Comparison of Gen 1 and Gen 2 backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-backup-restore).


### 9. How does high availability differ?
{: #faq-9}

Gen 2 provides:

- Multi-zone deployments.
- Faster failover.
- Up to 2 HA nodes + 1 DR replica in some database offerings.


### 10. Are there pricing changes?
{: #faq-10}

Yes. {{site.data.keyword.cloud}} Gen 2 Databases use the same pricing model as Gen 1, but the overall pricing structure is more aligned with broader market expectations. Backup-related pricing now follows a snapshot-based model consistent with standard database-industry practices. Storage costs are also approximately 60% lower. The exact impact on your workload depends on the your service and configuration.

### 11. Do Gen 2 database services integrate better with automation tools?
{: #faq-11}

Yes. Gen 2 Databases provide stronger integration with {{site.data.keyword.cloud}} automation tooling through:

- Improved Terraform support.
- Stronger API alignment across services.
- Resource Controller API for instance lifecycle management.
- {{site.data.keyword.cloud}} CLI support through Resource Controller CLI.


### 12. How does the CLI differ between Gen 1 and Gen 2?
{: #faq-12}

|  Classic CLI | Gen 2 CLI|
|---------------|------------------|
| Based on Classic infrastructure |  New CLI plugin required |
| Commands tied to Classic networking and resource constructs | VPC-native command model |
| **Does not work** with Gen 2 services | Works with Gen 2 compute models and VPE networking |
{: caption="Differences in CLI" caption-side="bottom"}

Gen 2 does not currently support the Databases CLI (CDB) plugin. For Gen 2 instances, you must use the IBM Cloud Resource Controller CLI commands. This includes operations like creating instances, updating configurations, and managing service credentials. See the [CLI reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-reference) documentation for Gen 2-specific commands.


### 13. Do monitoring and logging tools change?
{: #faq-13}

No. Both Gen 1 and Gen 2 instances fully integrate with:

- [{{site.data.keyword.logs_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-logging)
- [{{site.data.keyword.monitoringlong}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-monitoring)
