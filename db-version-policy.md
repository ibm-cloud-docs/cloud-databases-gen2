---

copyright:
  years: 2026
lastupdated: "2026-08-20"

subcollection: cloud-databases-gen2

keywords: version for cloud-databases, database version, end of life, major version, minor version, deprecate, deprecation, version number, deprecated, eol

---

{{site.data.keyword.attribute-definition-list}}

# Versioning policy
{: #versioning-policy}

[Gen 2]{: tag-purple}

When you provision a {{site.data.keyword.databases-for}} instance, you can choose from the versions currently available on {{site.data.keyword.cloud}}. Currently, only the latest versions are available for Gen 2 {{site.data.keyword.databases-for}} and this is shown in the [catalog pages](https://cloud.ibm.com/catalog?category=databases){: external}, the [Resource Controller CLI](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-cdb-reference), or the [Resource Controller API](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-api).

## Major versions defined
{: #version-definitions}



| Service | {{site.data.keyword.databases-for}} versioning schema| Next known end-of-life version and date | Preferred major version | End-of-life procedure [^tabletext4] |
|----|----|----|----|----|
| {{site.data.keyword.databases-for-postgresql}} | {{site.data.keyword.databases-for}} major version is defined by the first number in the version number. |  v14, 21 October 2026 |   v18 | Automatically upgraded in place to next major version, [Customer-initiated in-place upgrade from v14 to v15 supported](/docs/databases-for-postgresql-gen2?topic=databases-for-postgresql-gen2-upgrading&interface=ui#upgrading-in-place) |
| {{site.data.keyword.databases-for-mongodb}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a `major.x.patch` version number. In cases where `x` is even, it is a stable release suitable for production. Even `x` versions are the only ones available on {{site.data.keyword.databases-for}}. |  v8.0, 24 Oct 2029 |  v8.0  | Automatically upgraded in place to next Major version, [Customer-initiated in-place upgrade to the next major version is supported for Standard and Enterprise plans](/docs/databases-for-mongodb-gen2?topic=databases-for-mongodb-gen2-upgrading&interface=ui#upgrading-in-place) |
| {{site.data.keyword.databases-for-redis}} | {{site.data.keyword.databases-for}} major versions are the first number in a `major.minor.patch` version number. | N/A |   v8.2   | Automatically upgraded in place to next Major version|
| {{site.data.keyword.databases-for-elasticsearch}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a `release.version`.maintenance version number. | N/A  |   v8.19   | Automatically upgraded in-place to next major version, Customer-initiated in-place upgrade to the version 8.19 is supported. |
| {{site.data.keyword.databases-for-mysql}} | {{site.data.keyword.databases-for}} major versions are the first two numbers in a major.x.patch version number. | v8.4, 30 April 2029 |   v8.4 | Automatically upgraded in place to next major version |
| {{site.data.keyword.messages-for-rabbitmq}} | {{site.data.keyword.databases-for}} Major versions are the first numbers in a `major.x.patch` version number. | N/A |   v4   | Backup taken and access removed for Major version, <br> Automatically upgraded in place to next minor version|
| {{site.data.keyword.databases-for-valkey}} | {{site.data.keyword.databases-for}} Major versions are the first two numbers in a `major.x.patch` version number. | N/A  |   v9  |Automatically upgraded in place to next major version |
{: caption="Major versions for {{site.data.keyword.databases-for}}" caption-side="top"}

[^tabletext4]: This column describes the actions that will be taken by the {{site.data.keyword.cloud}} team on database instances that have not been upgraded to a new version prior to the version EoL date. This approach is not recommended. For more information, see [End-of-life procedure](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-versioning-policy).

## Subscribe for version updates
{: #version-updates-subscribe}

{{site.data.keyword.databases-for}} major version updates are posted in each service's Release Notes. To stay up to date with major version announcements, go to the [{{site.data.keyword.cloud_notm}} Status page](https://cloud.ibm.com/status){: external} and sign up for notifications. Service release notes are included in these status notifications.

## Deprecation of major versions
{: #version-deprecation}

{{site.data.keyword.databases-for}} aims to support a major version for approximately 3 years from its release. If a version is deprecated or marked end of life by the upstream open source maintainers, {{site.data.keyword.databases-for}} will initiate its own deprecation process.

When a major version is deprecated, a six-month transition window is opened for current users of the deprecated version. At the beginning of the period, we contact users affected by the deprecation. During the six-month transition window, users are able to initiate an upgrade to a supported major version. Existing instances continue to run as normal.

Restoration of existing instances into new instances of the deprecated major version is available during the six-month deprecation, although we recommend upgrading to a nondeprecated major version as soon as possible.

At the end of the transition window, deprecated major versions cannot be deployed on {{site.data.keyword.databases-for}}. A backup of the instance is taken and access to instances that are running a deprecated version is removed or instances are automatically upgraded to the next major version. The backup is available to be restored into a new supported version.

Backups are retained for 30 days only. Requests to re-enable disabled formations of end-of-life versions cannot not accommodated.

Failure to act can result in compatibility issues with your apps when IBM upgrades in-place. On rare occasions, failure can result, impacting your availability. If a failure occurs, the instance is disabled, and you need to restore from backup. We recommend self-migrating before the end of support date.
{: important}

## Version tags
{: #version-tags}

Currently, only one version per Gen 2 {{site.data.keyword.databases-for}} service is supported. As new versions become available, the following version tags will apply.
{: .note}

| Version tag | Description|
|-------------|-------------|
| **Preferred** | The recommended and default version for all new instances. It's the most stable, up-to-date version from both an instance-level and service-level perspective.|
| **Preview** | A preview version is released for a limited time to try available functions. Often it is the newest available version available from the project maintainers in preparation for making it the "Preferred" version. While deployable, preview versions are not suitable for production, as they are excluded from service-level agreements and support. Also, a preview version isn't guaranteed to become a production-level release. IBM reserves the right to ask a customer to delete an instance that uses a preview version. |
| **Deprecated** | Old versions and versions near their end-of-life dates are marked as "Deprecated". Provisions and restores of instances that run a deprecated version are still available and instances that run a deprecated version continue to be supported. However, you are encouraged to upgrade to the new "Preferred" version as deprecated versions are eventually removed from {{site.data.keyword.cloud_notm}} and are no longer provisionable, restorable, or supported. |
| **Untagged** | Untagged versions are fully supported and deployable versions. They are usually slightly older than the current preferred version, but they are still supported by the project maintainers. They continue to be supported on {{site.data.keyword.databases-for}} instances until their deprecation is announced.|
| **Hidden** | A hidden version cannot be provisioned. Existing instances that are using a version marked as hidden are still able to be restored to the hidden version. |
{: caption="{{site.data.keyword.databases-for}} Version tags" caption-side="bottom"}

## Minor versions
{: #minor-versions}

{{site.data.keyword.cloud_notm}} is committed to providing secure, up-to-date versions of services. As updates are released by project maintainers, they are tested, evaluated, and released to {{site.data.keyword.databases-for}} instances. Your instance's minor version and patch updates are handled automatically and are not user configurable.

## Major versioning end-of-life notifications
{: #-major-version-eol}

You receive multiple notifications when a major version reaches its end of life. You can typically expect:

* A Cloud status page announcement, for example: [End of support notices](https://cloud.ibm.com/status/announcement?query=End+of+Support+Notices){: external}.
* An announcement in your service's release notes, for example: [IBM Cloud® Databases for PostgreSQL version 12 end of life on January 22, 2025](/docs/databases-for-postgresql-gen2?topic=databases-for-postgresql-gen2-postgresql-relnotes#databases-for-postgresql-15Dec2025).
* A notification by email through the {{site.data.keyword.IBM_notm}} API. This email contains a *Notifications* link that takes you to a Notifications Management page. **Make sure that these announcements are not being caught by your email service's spam filter.** For more information, see [Adding users to a distribution list](/docs/support?topic=support-add-users-distribution-list){:external}.
* Ensure that your account is enabled to receive notifications and announcements. You **must** enable toggle to receive platform and resource updates. Turn on major and minor toggle under the Platform tab > Announcements > Major and Minor, and service updates under the Resource tab > Resource Activity > Service Updates. For more information, see [Setting email preferences for notifications](/docs/support?topic=support-email-prefs){:external}.

For more information, see [Programmatic methods for checking version status](#-major-version-eol-check-version-status). Customers are encouraged to use **programatic ways**, via CLI or API, to get updated about database version status. For more information, see [Programmatic methods for checking version status](#-major-version-eol-check-version-status).

Any actions taken after an EOL date happen over several days after the EOL date. We try, but cannot guarantee, to make these upgrades outside of business hours in the local regions. If you want more control over the upgrade process of your instance, we recommend that you upgrade following our [backup and restore process](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-dashboard-backups&interface=ui) before the EOL date of your version.
{: .note}

### Programmatic methods for checking version status
{: #-major-version-eol-check-version-status}



**Via an API** Gen 2 {{site.data.keyword.databases-for}} utilize the Resource Controller API for operation purposes. The following command gets the full data that is associated with a deployment. This data includes the ID, name, database type, and version.

```sh
GET /v2/resource_instances/{id}`
```
{: pre}

Example request:

```sh
curl -X GET https://resource-controller.cloud.ibm.com/v2/resource_instances/8d7af921-b136-4078-9666-081bd8470d94 -H "Authorization: Bearer <IAM token>" \
```
{: pre}
