---

copyright:
  years: 2026
lastupdated: "2026-11-24"

subcollection: cloud-databases-gen2

keywords: version for cloud-databases, database version, end of life, end-of-life, major version, minor version, deprecate, deprecation, version number, deprecated, eol

---

{{site.data.keyword.attribute-definition-list}}

# Versioning policy
{: #versioning-policy}

[Gen 2]{: tag-purple}

This topic describes the versioning policy for {{site.data.keyword.databases-for}} Gen 2. For the versioning policy for Gen 1, see [Versioning policy for Gen 1](/docs/cloud-databases?topic=cloud-databases-versioning-policy).

{{site.data.keyword.databases-for}} Gen 2 is the strategic platform for future database version adoption. Compare how versions are managed on each platform.

| Platform | Versioning policy |
|----|----|
| **Gen 2** | Gen 2 is the strategic platform for future database version adoption. New major database versions are onboarded to Gen 2. Gen 2 deployments receive all new minor versions, feature updates, and security patches across all supported major versions. |
| **Gen 1** | {{site.data.keyword.databases-for}} continues to provide supported, stable, and secure database versions across both platforms. Gen 1 customers remain on actively maintained major versions and continue to receive minor version updates, security patches, and platform support in accordance with the published lifecycle policy. |
{: caption="Versioning policy by platform" caption-side="top"}

When you provision a {{site.data.keyword.databases-for}} instance, you can choose from the versions currently available on {{site.data.keyword.cloud}}. Find the latest versions from the [catalog pages](https://cloud.ibm.com/catalog?category=databases){: external}, the [{{site.data.keyword.databases-for}} CLI plug-in](/docs/cloud-databases?topic=cloud-databases-cdb-reference#deployables-show){: external}, or the [{{site.data.keyword.databases-for}} API](/apidocs/cloud-databases-api/cloud-databases-api-v5#listdeployables){: external}.

## Major versions defined
{: #version-definitions}

| Service | {{site.data.keyword.databases-for}} versioning schema| Next known end-of-life version and date | Preferred major version | End-of-life procedure [^tabletext4] |
|----|----|----|----|----|
| {{site.data.keyword.databases-for-mongodb}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a `major.x.patch` version number. In cases where `x` is even, it is a stable release suitable for production. Even `x` versions are the only ones available on {{site.data.keyword.databases-for}}. | None announced | v8.0 | Automatically upgraded in place to next major version. |
| {{site.data.keyword.databases-for-elasticsearch}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a `release.version`.maintenance version number. | None announced | v8.19 | Automatically upgraded in place to next major version. |
| {{site.data.keyword.databases-for-redis}} | {{site.data.keyword.databases-for}} major versions are the first number in a `major.minor.patch` version number. | None announced | v8.2 | Automatically upgraded in place to next major version. |
| {{site.data.keyword.databases-for-postgresql}} | {{site.data.keyword.databases-for}} major version is defined by the first number in the version number. | None announced | v18 | Automatically upgraded in place to next major version. |
| {{site.data.keyword.databases-for-mysql}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a `major.x.patch` version number. | None announced | v8.4 | Automatically upgraded in place to next major version. |
| {{site.data.keyword.messages-for-rabbitmq}} | {{site.data.keyword.databases-for}} major versions are the first number in a `major.x.patch` version number. Minor versions are patched within the major version. | None announced | v4 | Automatically upgraded in place to next major version. |
{: caption="Major versions for {{site.data.keyword.databases-for}} Gen 2" caption-side="top"}

[^tabletext4]: This column describes the actions that will be taken by the {{site.data.keyword.cloud}} team on database instances that have not been upgraded to a new version prior to the version end-of-life (EOL) date. For more information, see [End-of-life procedure](#version-EOL).

### End-of-life procedure
{: #version-EOL}

End-of-life handling depends on the service and versioning model. The following approach describes what happens when a version reaches its end-of-life date.

Forced automatic upgrade to the next supported version after end of life
:   After the end-of-life date, all active deployments running on a deprecated version are automatically upgraded to the next supported version. For example, PostgreSQL version 18 is automatically upgraded to version 19.

    Automatic upgrades are not recommended as a replacement for a planned upgrade. They have the following risks and limitations::
    {: important}

    * No SLAs are provided for this type of forced upgrade.
    * Data loss might occur.
    * Applications might experience downtime.
    * Applications might stop working if they have any incompatibilities with the new database version.
    * You cannot control the timing of the forced upgrade of your instances.
    * There is no rollback process for forced upgrades.
    * Therefore, upgrade {{site.data.keyword.databases-for}} instances to the latest version available as soon as possible after that version is made available.

## Subscribe for version updates
{: #version-updates-subscribe}

Availability of a new major database version in {{site.data.keyword.cloud_notm}} is communicated via the release notes and [{{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status){: external}. Set up {{site.data.keyword.cloud_notm}} status notifications, as described in the [documentation](/docs/cloud-databases?topic=cloud-databases-getting-started-cdb-setup-notifs), in order to receive a notification when new release notes are published.

## Major version end-of-life procedures
{: #version-deprecation}

End-of-life dates for major database versions in {{site.data.keyword.databases-for}} are determined after considering two primary factors.

1. **End of vendor or community support**: The date when the open-source community or vendor responsible for maintaining the database version ends support for that version.
2. **Industry security best practices**: Industry best practices generally discourage using software that is no longer maintained because bugs and security vulnerabilities are unlikely to be fixed.

The frequency of major releases and maintenance lifecycle policies vary across the databases offered in the {{site.data.keyword.cloud_notm}} portfolio. As a result, the time between the general availability of a major database version in {{site.data.keyword.cloud_notm}} and its end-of-life date varies by database and release.

When the end-of-life date for a major version is determined, {{site.data.keyword.cloud_notm}} publishes a notification on the status announcements page. After receiving the notification, we strongly recommend that you begin upgrading your instances to the latest supported major version before the end-of-life date.

At the end-of-life date, any database instances that are still running a deprecated major version are handled according to the procedure described in the End-of-life procedure column in Table 1. If the end-of-life procedure includes creating a backup of an instance, the backup remains available for 30 days. During this period, you can restore the backup to a new instance running a supported version. After 30 days, the backup is deleted.

Requests to re-enable instances that have been disabled as part of the end-of-life process are not supported.

End-of-life procedures and related actions might take several days to complete after the end-of-life date. These actions are generally performed outside local business hours, but this cannot be guaranteed. To maintain greater control over the upgrade process, upgrade your instances before their end-of-life date.
{: note}

## Version tags
{: #version-tags}

| Version tag | Description|
|-------------|-------------|
| **Preferred** | The recommended and default version for all new instances. It's the most stable, up-to-date version from both an instance-level and service-level perspective.|
| **Preview** | A preview version is released for a limited time to try available functions. Often it is the newest available version available from the project maintainers in preparation for making it the "Preferred" version. While deployable, preview versions are not suitable for production, as they are excluded from service-level agreements and support. Also, a preview version isn't guaranteed to become a production-level release. IBM reserves the right to ask a customer to delete an instance that uses a preview version. |
| **Deprecated** | Old versions and versions near their end-of-life dates are marked as "Deprecated". Provisions and restores of instances that run a deprecated version are still available and instances that run a deprecated version continue to be supported. However, you are encouraged to upgrade to the new "Preferred" version as deprecated versions are eventually removed from {{site.data.keyword.cloud_notm}} and are no longer provisionable, restorable, or supported.  |
| **Untagged** | Untagged versions are fully supported and deployable versions. They are usually slightly older than the current preferred version, but they are still supported by the project maintainers. They continue to be supported on {{site.data.keyword.databases-for}} instances until their deprecation is announced.|
| **Hidden** | A hidden version cannot be provisioned. Existing instances that are using a version marked as hidden are still able to be restored to the hidden version. |
{: caption="{{site.data.keyword.databases-for}} version tags" caption-side="bottom"}

## Minor versions
{: #minor-versions}

{{site.data.keyword.cloud_notm}} is committed to providing secure, up-to-date versions of services. As updates are released by project maintainers, they are tested, evaluated, and released to {{site.data.keyword.databases-for}} instances. Your instance's minor version and patch updates are handled automatically and are not user configurable.

## Major versioning end-of-life notification
{: #-major-version-eol}

The amount of advance notice provided for the end-of-life date of a major database version depends on how much advance notice the associated open-source community or vendor provides before ending maintenance of that version.

When the open-source community or vendor announces an end-of-maintenance date in advance, notifications about the upcoming end-of-life date might be provided through the following channels:

1. **{{site.data.keyword.cloud_notm} status page announcement**: For example: [End of support notices](https://cloud.ibm.com/status/announcement?query=End+of+Support+Notices){: external}.
2. **Service release notes**: For example: [{{site.data.keyword.databases-for-postgresql}} version 12 end of life on January 22, 2025](/docs/databases-for-postgresql?topic=databases-for-postgresql-postgresql-relnotes#databases-for-postgresql-18jan2023){: external}
3. **Email notification**: Email notifications are sent if your account notification settings are configured to include email addresses. The email contains a *Notifications* link that takes you to the **Notifications Management** page. For more information, see [Setting up distribution lists for {{site.data.keyword.cloud_notm}} notifications](https://cloud.ibm.com/docs/account?topic=account-add-users-distribution-list){: external} and [Setting email preferences for notifications](https://cloud.ibm.com/user/notifications){: external}.

Ensure that your account is configured to receive both platform and resource notifications:

* Enable the **Major and minor** toggle under **Platform tab** > Announcements > Major and minor**. 
* Enable **Service updates** under the **Resource tab > Resource activity > Service updates**.

You can also check the version status of all your {{site.data.keyword.databases-for}} instances programmatically by using the CLI or API. For more information, see [Programmatic methods for checking version status](#-major-version-eol-check-version-status).

### Programmatic methods for checking version status
{: #-major-version-eol-check-version-status}

**On the CLI** the following [{{site.data.keyword.databases-for}} `deployables-show` command](/docs/cloud-databases?topic=cloud-databases-cdb-reference#deployables-show) shows deployable service types, specifically the available versions and their `preferred` or `stable` status.

```sh
ibmcloud cdb deployables-show [--stable] [--preferred] [--json]
```
{: pre}

Check the status of a major version by reviewing the output of the `deployable` command, specifically `Status` and `Preferred`. The following output example shows that version 7 is the `Preferred` version and version 6 `Status` is `deprecated`.

```text
Service Type:  mongodb
Version   Status       Preferred
7       stable       true
6       deprecated   false
```
{: pre}

**On the {{site.data.keyword.databases-for}} API** the [`deployables` endpoint](/apidocs/cloud-databases-api/cloud-databases-api-v5#listdeployables){: external} returns all deployable services. Use the `version` parameter to return the version number.

```sh
GET /v5/ibm/deployables
```
{: pre}

### Major versions and Terraform
{: #-major-version-eol-terraform}

Note that you cannot currently upgrade to a new major version using Terraform. Changing the version number on a Terraform script could lead to your data being destroyed. The recommended method of version upgrade is restoring a backup into a new deployment with the latest version. For more information, see [Restoring a backup](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui#restore-backup).
{: important}
