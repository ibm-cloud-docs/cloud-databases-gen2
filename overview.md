---
copyright:
  years: 2025
lastupdated: "2025-12-05"

keywords: cloud databases gen 2

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Overview of Gen 1 (Classic) and Gen 2 (VPC)
{: #overview-gen1-gen2}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

{{site.data.keyword.databases-for}} support an extensive portfolio of relational and non-relational (NoSQL) databases and integrations to support building a wide range of application types across all industries. The following page outlines the key differences between {{site.data.keyword.databases-for}} built on IBM’s Classic platform (Gen 1) and the latest VPC based platform (Gen 2).

## Generation  1 (Classic)
{: #gen1}

IBM’s original platform consisting of all databases across all regions and a rich feature set. Gen 1 Databases support both private and public endpoints, with options for isolated and shared compute. This environment is best suited for workloads that benefit from simpler networking and isolation features.

## Generation 2 (VPC)
{: #gen2}

Gen 2 databases are built on IBM’s latest platform, based on highly secure software-defined networking architecture and ideal for cloud-native applications. Gen 2 Databases currently are only available in select regions only and support private endpoints and isolated compute options. This environment is ideal for modern applications that demand advanced networking and secure, software-defined isolation.

## Feature differentiators
{: #feature-differentiators}

| Category                     | Gen 1                                                            | Gen 2                                             |
|-----------------------------|-------------------------------------------------------------------|---------------------------------------------------|
| Regions                     | Multizone location (MZR) <br> Dallas (us-south) <br> Sao Paulo (br-sao) <br> Toronto (ca-tor) <br> Washington (us-east) <br> Frankfurt (eu-de) <br> London (eu-gb) <br> Madrid (eu-es) <br> Osaka (jp-osa) <br> Sydney (au-syd) <br> Tokyo (jp-tok) | Single-campus MZR (SC-MZR) <br> Montreal (ca-mon)   |
| Database editions           | PostgreSQL <br> MongoDB (Standard and Enterprise) <br> MySQL <br> ElasticSearch (Enterprise and Platinum) <br> RabbitMQ <br> Redis              | PostgreSQL <br> MongoDB (Standard)     |
| Endpoints                   | Private endpoints <br> Public endpoints                           | Private endpoints                                 |
| Hosting models              | Isolated compute <br> Shared compute                              | Isolated compute                                  |
| Database versions supported | Minimum 2, varies per database                                    | Latest                                            |
| Autoscaling                 | Yes                                                               | Future release                                    |
| Read replicas (SQL only)    | Yes                                                               | Future release                                    |
{: caption="Feature differentiators" caption-side="bottom"}

## Performance differentiators
{: #performance-differentiators}

| Category               | Gen 1                                                                 | Gen 2                                               |
|------------------------|-----------------------------------------------------------------------|-----------------------------------------------------|
| Compute generation     | IBM Classic infrastructure                                            | IBM Cloud VPC                                       |
| Availability           | High availability                                                     | High availability                                   |
| Deployment timeframe   | Minutes                                                               | Seconds                                             |
| Pricing                | Hourly and monthly billing                                            | Hourly and monthly billing                          |
| Backup and restore     | Timing depends on size of backup and performance impact during backup | Consistent, fast [add link](link to Backup/restore gen 2 page)|
{: caption="Performance differentiators" caption-side="bottom"}

## Access, compliance, and security differentiators
{: #access-compliance-security-differentiators}

| Category               | Gen 1                                                                 | Gen 2                                              |
|------------------------|-----------------------------------------------------------------------|----------------------------------------------------|
| User and role management | [Database `admin` user created by IBM](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-user-management&interface=ui) | Database "manager" via service-credential                              |
| Certificate type       | Signed by IBM Cloud Database Certificate Authority                    | Certificates signed by a Certificate Authority (Let's encrypt)         |
| Encryption             | Encryption at Rest <br> Encryptions in Transit <br> Customer-managed encryption - Bring your own key (BYOK) | Encryption at Rest <br> Encryptions in Transit <br> Customer-managed encryption - Bring your own key (BYOK) |
| Compliance             | FS Cloud <br> GDPR <br> ISO 27001, 27017, 27018 <br> SOC 1, SOC 2 <br> PCI DSS <br> HIPAA  | FS Cloud <br> GDPR <br> ISO 27001, 27017, 27018SOC 1 <br> SOC 2 <br> PCI DSS <br> HIPAA      |
{: caption="Access, compliance, and security differentiators" caption-side="bottom"}
