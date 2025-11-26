---

copyright:
  years: 2025
lastupdated: "2025-11-26"

keywords: certificate, cert, tls, ssl, mutual tls, client certificates

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Certificates FAQ
{: #faq-cert}
{: faq}
{: support}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).

{{site.data.keyword.databases-for}} certificates are authenticated by unique TLS certificates. To verify this, you can inspect the certificate that your service presents when opening a connection. The certificate contains the hostname for a single instance. {{site.data.keyword.databases-for}} data plane clusters possess their own distinctive root certificate. When you're engaged in certificate validation procedures, exercise caution and select the correct root certificate for each instance. For more information, see [Connecting an external application](#faq-cert-external-app).

## Connecting an external application documentation
{: #faq-cert-external-app}
{: faq}
{: support}

Choose the appropriate service documentation for connecting an external application:

- [{{site.data.keyword.databases-for-postgresql}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-external-app){: external}
- [{{site.data.keyword.databases-for-mongodb}}](/docs/databases-for-mongodb?topic=databases-for-mongodb-mongodb-external-app){: external}
- [{{site.data.keyword.databases-for-redis}}](/docs/databases-for-redis?topic=databases-for-redis-external-app){: external}
- [{{site.data.keyword.databases-for-elasticsearch}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-external-app){: external}
- [{{site.data.keyword.databases-for-mysql}}](/docs/databases-for-mysql?topic=databases-for-mysql-external-app){: external}
- [{{site.data.keyword.messages-for-rabbitmq}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-external-app){: external}
- [{{site.data.keyword.databases-for-enterprisedb}}](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-external-app){: external}
- [{{site.data.keyword.databases-for-etcd}}](/docs/databases-for-etcd?topic=databases-for-etcd-external-app){: external}

## Mutual TLS
{: #faq-cert-mutual-tls}
{: faq}
{: support}

{{site.data.keyword.databases-for}} does not support mutual TLS for client connections. Presenting client certificates or configuring trusted root certificate authorities (CAs) for client certificates is not supported.
