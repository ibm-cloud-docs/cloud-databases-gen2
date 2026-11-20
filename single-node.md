---

copyright:
  years: 2026
lastupdated: "2026-11-20"

keywords: single-node, single node, beta, availability, regions, postgresql, mongodb

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Single-node deployments (Beta)
{: #single-node}

[Gen 2]{: tag-purple}

Single-node deployments are in Beta and are available for select databases in select regions.
{: beta}

Single-node deployments provision one database member instead of the default two or three-member high-availability configuration. They are intended for development, testing, and proof-of-concept workloads.
{: shortdesc}

## About single-node deployments
{: #single-node-about}

A single-node deployment runs your database on one member. Because the deployment has no additional members, it doesn't provide the high availability of the default configuration. Use single-node deployments for development, testing, and proof-of-concept workloads.

You can convert a single-node deployment to a high-availability deployment without migrating your data.

## Availability by service and region
{: #single-node-availability}

The following table shows where single-node deployments are available.

| | `eu-de` |
| --- | --- | --- |
| {{site.data.keyword.databases-for-postgresql}} | Available |
| {{site.data.keyword.databases-for-mongodb}} | Available |
{: row-headers}
{: caption="Single-node deployment availability by service and region" caption-side="bottom"}
{: summary="This table has row and column headers. The row headers identify the database service. The column headers identify the region. Each cell indicates whether single-node deployments are available for that service in that region."}
{: #single-node-availability-table}

## Provisioning a single-node deployment
{: #single-node-provisioning}

For provisioning instructions, see the following topics:

- [Provisioning for PostgreSQL](/docs/databases-for-postgresql-gen2?topic=databases-for-postgresql-gen2-provisioning&interface=ui)
- [MongoDB Enterprise Sharding](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-enterprise-sharding-provisioning-single-node&interface=cli)
