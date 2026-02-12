---

copyright:
  years: 2026
lastupdated: "2026-02-12"

keywords: ICD Gen 2 FAQ

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Cloud Databases Gen 2 – Frequently Asked Questions (FAQ)
{: #faq}
{: faq}
{: support}

[Gen 2]{: tag-purple}

## Overview
{: #faq-overview}

{{site.data.keyword.databases-for}} Gen 2 is built on **IBM Cloud VPC infrastructure**, replacing the older Classic infrastructure used by Gen 1 services. VPC provides higher performance, improved availability, modernized networking, and better operational controls for managed databases. 

This FAQ summarizes the key differences you encounter when transitioning from Classic/Gen 1 to the new Gen 2 platform.

---
### 1. What is the biggest difference between Classic and Gen 2?
{: #faq-1}

Classic services run on **Classic IaaS**, while Gen 2 runs on **VPC (Virtual Private Cloud)**.

#### Key differences
{: #faq-1-differences}

| Area | Classic | Gen 2 |
|------|------------------|--------------|
| **Infrastructure** | VLAN-based Classic data-center model | Modern, software-defined VPC regional model |
| **Performance** | Network speeds up to ~50 Gbps | Network speeds up to 200 Gbps | <! -- Uche, pls. confirm these numbers -->
| **Security** | Older networking/security approach | VPEs, better IAM integration, cloud-native networking |
| **Provisioning** | Slower provisioning | Faster provisioning |
| **Scaling** | Scaling through Shared and Isolated Compute models | Flexible scaling through Isolated Compute models |
{: caption="Key differences" caption-side="bottom"}


### 2. Why should I choose Gen 2?
{: #faq-2}

Gen 2 provides:

- Modern networking with higher throughput
- Better multi-zone availability
- Stronger security with VPEs and IAM integration
- Faster provisioning and automation alignment
- Long-term strategic alignment with {{site.data.keyword.cloud}}

### 3. Does Gen 2 have any limitations compared to Classic?
{: #faq-3}

Yes, the following limitations exist at this point:

- Montreal region only
- Context-based restrictions (CBR) is not yet supported
- Lack of public endpoints
- No autoscaling
- No Shared Compute


### 4. Are there differences in hosting models between Gen 1 and Gen 2?
{: #faq-4}

- Gen 1: Shared and Isolated hosting models
- Gen 2: Isolated hosting model

|  Shared Compute (multi-tenant) | Isolated Compute (single-tenant)|
|---------------|------------------|
| - Flexible CPU/RAM selections /n - Small or custom presets /n - Ideal for dev/test or cost-efficient workloads |  - Dedicated compute /n - Best for production workloads requiring isolation | 
{: caption="Differences in hosting models" caption-side="bottom"}


### 5. How does performance differ between Classic and Gen 2?
{: #faq-5}

Gen 2 offers:

- Up to 200 Gbps networking
- Improved CPU/memory profiles


### 6. What about security differences?
{: #faq-6}

Gen 2 delivers:
- VPEs for private access
- Cloud-native networking (VPN, LBaaS, NAT)
- Unified IAM integration
- Consistent encryption at rest/in transit


### 8. Does Gen 2 change backup and restore capabilities?
{: #faq-8}

Yes, with:
- [Snapshot-based backups](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-comparison-backups)


### 9. How does high availability differ?
{: #faq-9}

Gen 2 provides:
- Multi-zone deployments
- Faster failover
- Up to 2 HA nodes + 1 DR replica in some database offerings


### 10. Are there pricing changes?
{: #faq-10}

Yes:
- IOPS-based storage pricing
- Flexible compute pricing
- VPC sustained usage discounts


### 11. Do Gen 2 database services integrate better with automation tools?
{: #faq-11}

Yes:
- Stronger API alignment
- Faster provisioning


### 12. Do monitoring and logging tools change?
{: #faq-12}

Gen 2 integrates with:
- [{{site.data.keyword.logs_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-logging)
- [{{site.data.keyword.monitoringlong}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-monitoring)


### 13. How does the CLI differ between Gen 1 and Gen 2?
{: #faq-13}

|  Classic CLI | Gen 2 CLI|
|---------------|------------------|
| Based on Classic infrastructure |  New CLI plugin required | 
| Commands tied to Classic networking & resource constructs | VPC-native command model | 
| **Does not work** with Gen 2 services | Works with Gen 2 compute models and VPE networking | 
{: caption="Differences in CLI" caption-side="bottom"}
