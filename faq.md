---

copyright:
  years: 2026
lastupdated: "2026-02-04"

keywords: 

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

IBM Cloud Databases Gen 2 is built on **IBM Cloud VPC infrastructure**, replacing the older Classic infrastructure used by Gen 1 services. VPC provides higher performance, improved availability, modernized networking, and better operational controls for managed databases. 

This FAQ summarizes the key differences you encounter when transitioning from Classic/Gen 1 to the new Gen 2 platform.

---
## 1. What is the biggest difference between Gen 1 (Classic) and Gen 2?
{: #faq-1}

Gen 1 services ran on **Classic IaaS**, while Gen 2 runs on **VPC (Virtual Private Cloud)**.

### Key Differences
{: #faq-1-differences}

| Area | Classic (Gen 1) | VPC (Gen 2) |
|------|------------------|--------------|
| **Infrastructure** | VLAN-based Classic data-center model | Modern, software-defined VPC regional model |
| **Performance** | Network speeds up to ~50 Gbps | Network speeds up to 200 Gbps |
| **Availability** | Limited use of zone architecture | Strong multi-zone availability |
| **Security** | Older networking/security approach | VPEs, better IAM integration, cloud-native networking |
| **Provisioning** | More static system | Faster provisioning, API/CLI/Terraform-first model |
| **Scaling** | Constrained | Flexible scaling through Shared & Isolated Compute models |

---
## 2. Why did IBM migrate Cloud Databases to VPC Gen 2?
{: #faq-2}

Gen 2 provides:

- Modern networking with higher throughput
- Better multi-zone availability
- Stronger security with VPEs and IAM integration
- Faster provisioning and automation alignment
- Long-term strategic alignment with IBM Cloud

---
## 3. Are there differences in hosting models between Gen 1 and Gen 2?
{: #faq-3}

|  Shared Compute (multi-tenant) | Isolated Compute (single-tenant)|
|---------------|------------------|
| Flexible CPU/RAM selections |  Dedicated compute | 
| Small or custom presets | Best for production workloads requiring isolation| 
| Ideal for dev/test or cost-efficient workloads |  | 

---
## 4. How does performance differ between Classic and Gen 2?
{: #faq-4}

Gen 2 offers:

- Up to 200 Gbps networking
- Improved CPU/memory profiles
- IOPS-based scalable storage performance

---
## 5. What about security differences?
{: #faq-5}

Gen 2 delivers:
- VPEs for private access
- Cloud-native networking (VPN, LBaaS, NAT)
- Unified IAM integration
- Consistent encryption at rest/in transit

---
## 6. How do networking and connectivity differ?
{: #faq-6}

|  Classic | Gen 2 |
|---------------|------------------|
| POD-based constructs |  Regional VPC (no PODs) | 
| VLAN dependencies | Built-in NAT, routing, VPN, load balancers | 
| Customer-managed appliances for routing/NAT | Larger subnets and simplified connectivity | 

---
## 7. Does Gen 2 change backup and restore capabilities?
{: #faq-7}

Yes, with:
- IOPS-based scalable storage
- Snapshot-based backups
- PITR enhancements

---
## 8. How does high availability differ?
{: #faq-8}

Gen 2 provides:
- Multi-zone deployments
- Faster failover
- Up to 2 HA nodes + 1 DR replica in some database offerings

---
## 9. Are there pricing changes?
{: #faq-8}

Yes:
- IOPS-based storage pricing
- Flexible compute pricing (Shared vs Isolated)
- VPC sustained usage discounts

---
## 10. Do Gen 2 database services integrate better with automation tools?
{: #faq-10}

Yes:
- Improved Terraform integration
- Stronger API alignment
- Faster provisioning

---
## 11. Do monitoring and logging tools change?
{: #faq-11}

Gen 2 integrates with:
- IBM Cloud Logs
- IBM Cloud Monitoring

---
## 12. What should I consider before migrating?
{: #faq-12}

- Networking differences (VLAN → VPC)
- Connectivity updates (VPE)
- Updated hosting models
- Storage architecture differences
- IAM/resource-group alignment
- DB version updates

---
## 13. How does the CLI differ between Gen 1 and Gen 2?
{: #faq-13}

|  Classic CLI | Gen 2 CLI|
|---------------|------------------|
| Based on Classic infrastructure |  New CLI plugin required | 
| Commands tied to Classic networking & resource constructs | VPC-native command model | 
| **Does not work** with Gen 2 services | Works with Gen 2 compute models and VPE networking | 


---
## Summary
{: #faq-summary}

Gen 2 offers major improvements in performance, security, networking, automation, HA, and pricing. The shift to VPC infrastructure is the foundation of these improvements and aligns with IBM Cloud’s future direction.
