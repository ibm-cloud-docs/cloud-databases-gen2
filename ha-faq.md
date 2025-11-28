---
copyright:
  years: 2025
lastupdated: "2025-11-28"

subcollection: cloud-databases-gen2

keywords: 

---

{{site.data.keyword.attribute-definition-list}}

# High-availability FAQ
{: #faq-high-availability}
{: faq}
{: support}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

You encounter the following error: `READONLY You can't write against a read only replica`.
{: shortdesc}

{{site.data.keyword.databases-for}} instances are deployed as [highly available](/docs/databases-for-redis?topic=databases-for-redis-redis-ha-dr){: external}. The `READONLY` error message occurs when an application retains an active connection against a replica and attempts to write to the database, after a switchover has occurred. To resolve this error, the application should recreate their connection so they establish a new connection against the leader.
