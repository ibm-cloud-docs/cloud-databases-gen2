---
copyright:
  years: 2025
lastupdated: "2025-09-23"

keywords: cloud databases gen 2

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Gen 1 (Classic) and Gen 2 (VPC)
{: #overview-gen1-gen2}

{{site.data.keyword.databases-for}} support an extensive portfolio of relational and non-relational (NoSQL) databases and integrations to support building a wide range of application types across 
all industries. The following page outlines the key differences between {{site.data.keyword.databases-for}} built on IBM’s Classic platform (Gen 1) and the latest VPC based platform (Gen 2). 

- Generation  1

  IBM’s original platform consisting of all databases across all regions and a rich feature set. Gen 1 Databases support both private and public endpoints, with options for isolated 
and shared compute. This environment is best suited for workloads that benefit from simpler networking and isolation features. 

- Generation 2

  Gen 2 databases are built on IBM’s latest platform, based on highly secure software-defined networking architecture and ideal for cloud-native applications. 
Gen 2 Databases currently are only available in select regions only and support private endpoints and isolated compute options. This environment is ideal for modern applications 
that demand advanced networking and secure, software-defined isolation. 

Feature differentiators: 


| Category                     | Gen 1                                                                         | Gen 2                                                                 |
|-----------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Regions                     | Multizone location (MZR) \\n Dallas (us-south) \\n Sao Paulo (br-sao) \\n Toronto (ca-tor) \\n Washington (us-east) \\n Frankfurt (eu-de) \\n 
London (eu-gb) \\n Madrid (eu-es) \\n Osaka (jp-osa) \\n Sydney (au-syd) \\n Tokyo (jp-tok) | Single-campus MZR (SC-MZR) \\n Montreal (ca-mon)   |
| Database editions           | PostgreSQL \\n MongoDB (Standard and Enterprise) \\n MySQL \\n ElasticSearch (Enterprise and Platinum) \\n RabbitMQ \\n Redis              | PostgreSQL \\n 
MongoDB (Standard)     |
| Endpoints                   | Private endpoints \\n Public endpoints                                          | Private endpoints                                                      |
| Hosting models              | Isolated compute \\n Shared compute                                             | Isolated compute                                                       |
| Database versions supported | Minimum 2, varies per database                                                  | Latest                                                                 |
| Autoscaling                 | Yes                                                                             | Future release                                                         |
| Read replicas (SQL only)    | Yes                                                                             | Future release                                                         |
{: caption="Feature differentiators" caption-side="bottom"}

Performance differentiators:

| Category               | Gen 1                                                                 | Gen 2                                               |
|------------------------|-----------------------------------------------------------------------|-----------------------------------------------------|
| Compute generation     | IBM Classic infrastructure                                            | IBM Cloud VPC                                       |
| Availability           | High availability                                                     | High availability                                   |
| Deployment timeframe   | Minutes                                                               | Seconds                                             |
| Pricing                | Hourly and monthly billing                                            | Hourly and monthly billing                          |
| Backup and restore     | Timing depends on size of backup and performance impact during backup | Consistent, fast [add link](link to Backup/restore gen 2 page)|
{: caption="Performance differentiators" caption-side="bottom"}

Access, compliance, and security differentiators:

| Category               | Gen 1                                                                 | Gen 2                                                                 |
|------------------------|-----------------------------------------------------------------------|------------------------------------------------------------------------|
| User and role management | [Database `admin` user created by IBM](docs/databases-for-mongodb?topic=databases-for-mongodb-user-management&interface=ui)                            | Database "manager" via service-credential                              |
| Certificate type       | Signed by IBM Cloud Database Certificate Authority                    | Certificates signed by a Certificate Authority (Let's encrypt)         |
| Encryption             | Encryption at Rest \\n Encryptions in Transit \\n Customer-managed encryption - Bring your own key (BYOK) | Encryption at Rest \\n Encryptions in Transit \\n 
Customer-managed encryption - Bring your own key (BYOK) |
| Compliance             | FS Cloud \\nGDPR \\nISO 27001, 27017, 27018 \\nSOC 1, SOC 2PCI DSS \\nHIPAA  | FS Cloud \\nGDPR \\nISO 27001, 27017, 27018SOC 1 \\nSOC 2PCI DSS \\nHIPAA      |
{: caption="Access, compliance, and security differentiators" caption-side="bottom"}
