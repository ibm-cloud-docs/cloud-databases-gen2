---

copyright:
  years: 2026
lastupdated: "2026-10-23"

keywords: cloud databases release notes

subcollection: cloud-databases-gen2

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes
{: #databases-relnotes}

[Gen 2]{: tag-purple}

Use these release notes to learn about the latest updates to {{site.data.keyword.databases-for}} that are grouped by _date_ or _build number_.
{: shortdesc}

## 21 October 2026
{: #cloud-databases-gen2-21Oct2026}
{: release-note}

Single-node deployments (Beta) now available for select databases
:  {{site.data.keyword.databases-for}} now supports single-node deployments (Beta) for select databases in select regions. Single-node deployments provision a single database member instead of the default two or three-member high-availability configuration and are intended for development, testing, and proof-of-concept workloads. Single-node deployments can be converted to a high-availability deployment without requiring data migration. For more information, see [Provisioning for PostgreSQL](/docs/databases-for-postgresql-gen2?topic=databases-for-postgresql-gen2-provisioning&interface=ui) and [MongoDB Enterprise Sharding](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-enterprise-sharding-provisioning-single-node&interface=cli).

Customer-defined maintenance windows now available for select databases
:   You can now configure the days and start time for maintenance on your {{site.data.keyword.databases-for}} deployment for select databases. Customer-defined maintenance windows allow you to schedule maintenance activities during times that align with your operational requirements while ensuring critical security, reliability, and platform updates are applied. For more information, see [Customer-defined maintenance windows](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-maintenance-windows&interface=cli).

## 12 October 2026
{: #cloud-databases-gen2-12Oct2026}
{: release-note}

Context-based restrictions (CBR) support now available
:  You can now use context-based restrictions (CBR) to restrict access to {{site.data.keyword.databases-for}} resources based on network context, such as IP addresses, VPCs, and {{site.data.keyword.cloud}} services. For more information, see [Managing access with context-based restrictions](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cbr&interface=ui#cbr-overview).

## 7 October 2026
{: #cloud-databases-gen2-07Oct2026}
{: release-note}

Enhanced Bring Your Own Key (BYOK) experience in the provisioning UI
 : The provisioning experience now includes an updated encryption configuration component for customer-managed encryption keys through {{site.data.keyword.keymanagementservicefull}}. This update provides a more consistent key management experience during deployment creation. Learn more about [{{site.data.keyword.keymanagementserviceshort}} integration](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-key-protect&interface=ui) or provision a new {{site.data.keyword.databases-for}} Gen 2 database with customer-managed encryption enabled.

## 30 September 2026
{: #cloud-databases-gen2-30sep2026}
{: release-note}

The {{site.data.keyword.databases-for}} Gen 2 is now available in all VPC multizone regions
:  You can now deploy {{site.data.keyword.databases-for}} Gen 2 in all supported {{site.data.keyword.cloud}} VPC multizone regions (MZRs). This release adds support for Toronto (ca-tor), Tokyo (jp-tok), Osaka (jp-osa), and Sao Paulo (br-sao). For more information, see [Overview of Gen 1 and Gen 2](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-overview-gen1-gen2#feature-differentiators).

## 17 September 2026
{: #cloud-databases-gen2-17sep2026}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now available in Dallas and London
: {{site.data.keyword.databases-for}} Gen 2 is now available in Dallas (us-south) and London (eu-gb), in addition to Washington (us-east), Chennai - Airtel (in-che), Montreal (ca-mon), Mumbai (in-mum), Frankfurt (eu-de), Sydney (au-syd) and Madrid (eu-es). For more information, see [Overview of Gen 1 and Gen 2](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2&interface=ui#feature-differentiators).

## 1 September 2026
{: #cloud-databases-gen2-01sep2026}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now available in multiple regions
: {{site.data.keyword.databases-for}} Gen 2 is now available in Madrid DC (eu-es) and Sydney (au-syd), in addition to Washington (us-east), Chennai - Airtel (in-che), Montreal (ca-mon), Mumbai (in-mum), and Frankfurt (eu-de). For more information, see [Overview of Gen 1 and Gen 2](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2&interface=ui#feature-differentiators).

## 20 July 2026
{: #cloud-databases-gen2-20jul2026}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now available in Washington DC
: {{site.data.keyword.databases-for}} Gen 2 is now also available in Washington DC (us-east), in addition to Chennai - Airtel (in-che), Montreal (ca-mon), Mumbai (in-mum), and Frankfurt (eu-de). For more information, see [Overview of Gen 1 and Gen 2](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2&interface=ui#feature-differentiators).

## 6 July 2026
{: #cloud-databases-gen2-06jul2026}
{: release-note}

{{site.data.keyword.databases-for-redis}} Gen 2, {{site.data.keyword.databases-for-elasticsearch}} Gen 2, {{site.data.keyword.databases-for-mysql}} Gen 2, and {{site.data.keyword.messages-for-rabbitmq}} Gen 2 are now generally available (GA)
:  Gen 2 offers the same fully managed {{site.data.keyword.databases-for}} engine on newer VPC‑based infrastructure with improved security, networking, and more performant snapshot‑based backups.

{{site.data.keyword.databases-for}} Gen 2 is now available in Frankfurt
: {{site.data.keyword.databases-for}} Gen 2 is now also available in Frankfurt (eu-de), in addition to Chennai - Airtel (in-che), Montreal (ca-mon), and Mumbai (in-mum). For more information, see [Overview of Gen 1 and Gen 2](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2&interface=ui#feature-differentiators).

## 01 June 2026
{: #cloud-databases-gen2-01jun2026}
{: release-note}

{{site.data.keyword.databases-for-postgresql}} Gen 2 and {{site.data.keyword.databases-for-mongodb}} Gen 2 are now available in Mumbai
: {{site.data.keyword.databases-for}} Gen 2 is now also available in Mumbai (in-mum), in addition to Chennai - Airtel (in-che) and Montreal (ca-mon). For more information, see [Overview of Gen 1 and Gen 2](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-overview-gen1-gen2&interface=ui#feature-differentiators).

## 29 May 2026
{: #cloud-databases-gen2-18may2026}
{: release-note}

Introduction of Flex profiles for {{site.data.keyword.databases-for}} Gen 2 (on VPC), pricing and billing changes
: Flex profiles are introduced as the new baseline pricing option for {{site.data.keyword.databases-for}} Gen 2 (on VPC). Non-Flex (Fixed) profiles are repositioned as a premium offering and are subject to a price increase in existing regions.

: Billing for compute and the software-defined storage transitions from monthly prorated pricing to true hourly pricing model.

## 27 March 2026
{: #cloud-databases-gen2-27mar2026}
{: release-note}

Deprecation of {{site.data.keyword.hscrypto}}
: {{site.data.keyword.cloud}} is transitioning its dedicated key management offering from {{site.data.keyword.hscrypto}} to {{site.data.keyword.keymanagementservicelong}} Dedicated (Single Tenant). As part of this transition, {{site.data.keyword.hscrypto}} will reach **End of Life (EOL) on March 20, 2027**. After this date, the service will no longer be supported, and any remaining instances will be terminated.
To ensure continued service availability and support, you must migrate all existing HPCS root keys to {{site.data.keyword.keymanagementservicelong_notm}} Dedicated (Single Tenant) before the EOL date. For more information on how to migrate your encryption keys, see [Migrating from {{site.data.keyword.hscrypto}} (HPCS) to {{site.data.keyword.keymanagementserviceshort}} Dedicated (KP-ST)](/docs/EventStreams-gen2?topic=EventStreams-gen2-managing_encryption#migrating_hpcs_to_kp).

## 02 March 2026
{: #cloud-databases-gen2-02mar2026}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now available in Chennai
: {{site.data.keyword.databases-for}} Gen 2 is now also available in Chennai - Airtel (in-che), in addition to Montreal (ca-mon). For more information,
see [Overview of Gen 1 and Gen 2{{site.data.keyword.databases-for}}](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-overview-gen1-gen2#feature-differentiators).

## 26 February 2026
{: #cloud-databases-gen2-26feb2026}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now generally available (GA)
: {{site.data.keyword.databases-for}} Gen 2 offers the same fully managed {{site.data.keyword.databases-for}} engine on newer VPC‑based infrastructure with improved security, networking, and more performant snapshot‑based backups.
[Try {{site.data.keyword.databases-for}} Gen 2 now](/docs/databases-for-postgresql-gen2?topic=databases-for-postgresql-gen2-provisioning).

## 15 December 2025
{: #cloud-databases-gen2-15dec2025}
{: release-note}

{{site.data.keyword.databases-for}} Gen 2 is now in beta
: Support for Mongo v8: Built on VPC architecture with software-defined networking, delivering enhanced security and flexibility.
: Now available in the Montreal region, giving developers early access to next-generation database innovation.
