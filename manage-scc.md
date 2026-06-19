---
copyright:
  years: 2025, 2026
lastupdated: "2023-05-11"

keywords: security and compliance for cloud databases, security for cloud databases, compliance for cloud databases, enterprisedb, redis, etcd, elasticsearch, postresgql, datastax, mongodb, rabbitmq, mysql

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with {{site.data.keyword.databases-for}}
{: #manage-security-compliance}

{{site.data.keyword.databases-for}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can monitor for controls and goals that pertain to {{site.data.keyword.databases-for}}.

## Monitoring security and compliance posture with {{site.data.keyword.databases-for}}
{: #monitor-cloud-databases}

As a security or compliance focal, you can use the {{site.data.keyword.databases-for}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for {{site.data.keyword.databases-for}} are added to the {{site.data.keyword.cloud_notm}} Control Library profile, but can also be mapped to other profiles.{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/workload-protection?topic=workload-protection-getting-started)

### Available goals for {{site.data.keyword.databases-for}}
{: #cloud-databases-available-goals}

* **Check whether {{site.data.keyword.databases-for}} is enabled with IBM-managed or customer-managed encryption.** All {{site.data.keyword.databases-for}} instances are automatically encrypted at rest with IBM-managed keys. For more information, see [Key Protect Integration](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-key-protect&interface=ui).
* **Check whether {{site.data.keyword.databases-for}} is accessible only through TLS.** All {{site.data.keyword.databases-for}} connections use TLS/SSL encryption for data in transit. The current supported versions of this encryption are TLS 1.2 and TLS 1.3.
