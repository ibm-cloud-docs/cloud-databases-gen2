---

copyright:
  years: 2025
lastupdated: "2025-12-06"

keywords: logging, monitoring, metrics

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Set up logging and monitoring
{: #set-up-logging-monitoring}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

1. Use **{{site.data.keyword.mon_full}}** to gain operational visibility into the performance and health of your applications, services, and platforms. For more information, see {{site.data.keyword.databases-for}} [{{site.data.keyword.mon_full}} integration](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-monitoring).

Your Gen 2 {{site.data.keyword.databases-for}} instance will have up to five critical alerts auto-enabled for each {{site.data.keyword.databases-for}} instance when platform metrics are active. These alerts track key resources, such as memory, CPU, and disk I/O, with notifications sent to the account owner's email. For more information, see [default alerts reference](link).< --- need to add correct link here  --->

1. Use the **{{site.data.keyword.logs_full}}** service to capture a record of your {{site.data.keyword.databases-for}} activities and manage logs including audit and operational events. For more information, see {{site.data.keyword.databases-for}} [{{site.data.keyword.atracker_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2).

1. Use **{{site.data.keyword.logs_full}}** to add log management capabilities to your {{site.data.keyword.databases-for}} architecture. For more information, see {{site.data.keyword.databases-for}} [{{site.data.keyword.logs_full}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-logging).

## Next steps
{: #logging-monitoring-next-steps}

You provisioned a {{site.data.keyword.databases-for}} service, set up notifications, and set up monitoring. Now, work on [Securing your service](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-secure-service).
