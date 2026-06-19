---

copyright:
  years: 2026
lastupdated: "2026-06-19"

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Identity and Access Management integration (IAM)
{: #iam}

[Gen 2]{: tag-purple}


Management access to {{site.data.keyword.databases-for}} service instances for users in your account is controlled by [{{site.data.keyword.iamlong}}(IAM)](/docs/account?topic=account-cloudaccess).

This document covers the integration of {{site.data.keyword.iamshort}} with {{site.data.keyword.databases-for}}: {{site.data.keyword.databases-for-postgresql}} and {{site.data.keyword.databases-for-mongodb}}.
{: .note}

IAM is only integrated with high-level service access, which governs privileges and operations to perform management functions. It does not govern database-level users and privileges. Database access is governed by the standard access controls provided by the database. IAM does not control database users.

For more information about assigning user roles in {{site.data.keyword.cloud_notm}}, see [Managing IAM access](/docs/secure-enterprise?topic=secure-enterprise-userroles).

Gen 2 {{site.data.keyword.databases-for}} use service credentials for access management. This means:

- Instance/deployment passwords no longer exist and all credentials surfaced are {{site.data.keyword.cloud}} service credentials, which can have different roles (for example, Admin, Writer, Reader).
- You can create new service credentials through the platform, but updating an existing password is not supported.
- For database-level user management, you are advised to create and manage users directly within the database using your preferred method.

The following table provides a general overview of actions that are mapped to platform. Service management roles enable you to perform tasks on service resources at the service level. For example, assign user access for the service, create or delete service IDs, create instances, and bind instances to applications.

| Platform roles | Description of actions | Example actions |
| ----------------- | ----------------- | ----------------- |
| Viewer | As a Viewer, you can view database instances but you can't make configuration changes. | View service overview and view alerts. |
| Operator | As an operator, you can view database instances and make configuration changes that include managing database credentials. | Scale a deployment, create a new user password/service credential. |
| Editor | As an Editor, you can perform all platform actions (including making configuration changes and managing credentials) except for managing the account and assigning access policies. | Scale a deployment, create a new user password/ service credential. |
| Administrator | As an Administrator, you can perform all platform actions, including assigning access policies to other users. | Scale a deployment, create a new service credential, create and delete access policies. |
{: caption="IAM user roles and actions" caption-side="top"}

## Actions for {{site.data.keyword.databases-for}} API
{: #actions}

IAM access for Gen 2 {{site.data.keyword.databases-for}} is no longer managed through the {{site.data.keyword.databases-for}} API or CLI plug in; it is now handled via IBM Cloud Resource Controller.

Access to certain API endpoints and requests is governed by role. The following lists the access policy for each role for {{site.data.keyword.databases-for}}.

### Viewer
{: #viewer}

The allowed actions for the Viewer role.

```sh
GET /v5/ibm/deployables
Read Deployables
---
GET /v5/ibm/regions
Read Discover available regions
---
GET /v5/ibm/tasks/:task_id
Read a Task
---
GET /v5/ibm/backups/:backup_id
Read a Backup
---
GET /v5/ibm/deployments/:deployment_id
Read a Deployment
---
GET /v5/ibm/deployables/:deployable_id/groups
Read deployable group
---
GET /v5/ibm/deployments/:deployment_id/point_in_time_recovery_data
Read all deployment point-in-time-recovery data
---
GET /v5/ibm/deployments/:deployment_id/tasks
Read all deployment tasks
---
GET /v5/ibm/deployments/:deployment_id/backups
Read all deployment backups
---
GET /v5/ibm/deployments/:deployment_id/remotes
Read all deployment remotes
---
GET /v5/ibm/deployables/:deployable_id/groups
Read all deployment groups
---
GET /v5/ibm/deployments/:deployment_id/configuration/schema
Read deployment configuration schema
---
GET /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Read deployment user connections
---
POST /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Create deployment user connections
---
GET /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Read Allowlisted IP Addresses
```

### Operator and Editor
{: #operator}

The Operator and Editor roles are functionally the same for {{site.data.keyword.databases-for}}. This list contains allowed actions for the Operator and the Editor roles.

```sh
GET /v5/ibm/deployables
Read Deployables
---
GET /v5/ibm/regions
Read Discover available regions
---
GET /v5/ibm/tasks/:task_id
Read a Task
---
GET /v5/ibm/backups/:backup_id
Read a Backup
---
GET /v5/ibm/deployments/:deployment_id
Read a Deployment
---
GET /v5/ibm/deployables/:deployable_id/groups
Read deployable group
---
GET /v5/ibm/deployments/:deployment_id/point_in_time_recovery_data
Read all deployment point-in-time-recovery data
---
GET /v5/ibm/deployments/:deployment_id/tasks
Read all deployment tasks
---
GET /v5/ibm/deployments/:deployment_id/backups
Read all deployment backups
---
POST /v5/ibm/deployments/:deployment_id/backups
Create an on-demand backup
---
GET /v5/ibm/deployments/:deployment_id/remotes
Read all deployment remotes
---
POST /v5/ibm/deployments/:deployment_id/remotes/resync
Resync remote replica
---
GET /v5/ibm/deployables/:deployable_id/groups
Read all deployment groups
---
PATCH /v5/ibm/deployments/:deployment_id/groups/:group_id
Set scaling values on a specified group.
---
DELETE /v5/ibm/deployments/:deployment_id/management/database_connections
Closes all the connections on a deployment. Available for PostgreSQL and EnterpriseDB ONLY.
---
PATCH /v5/ibm/deployments/:deployment_id/configuration
Update deployment configuration
---
GET /v5/ibm/deployments/:deployment_id/configuration/schema
Read deployment configuration schema
---
POST /v5/ibm/deployments/:deployment_id/users/:user_type
Create a user based on user type
---
DELETE /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id
Remove a user based on user type
---
GET /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Read deployment user connections
---
POST /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Create deployment user connections
---
GET /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Read Allowlisted IP Addresses
---
POST /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Create an Allowlisted IP Addresses
---
DELETE /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses/:ip_address_id
Remove an Allowlisted IP Addresses
---
PUT /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Bulk allowlist IP addresses
---
POST /v5/ibm/deployments/:deployment_id/elasticsearch/file_syncs
Create elasticsearch file sync
```

### Administrator
{: #admin}

The allowed actions for the Administrator role.

```sh
GET /v5/ibm/deployables
Read Deployables
---
GET /v5/ibm/regions
Read Discover available regions
---
GET /v5/ibm/tasks/:task_id
Read a Task
---
GET /v5/ibm/backups/:backup_id
Read a Backup
---
GET /v5/ibm/deployments/:deployment_id
Read a Deployment
---
GET /v5/ibm/deployables/:deployable_id/groups
Read deployable group
---
GET /v5/ibm/deployments/:deployment_id/point_in_time_recovery_data
Read all deployment point-in-time-recovery data
---
GET /v5/ibm/deployments/:deployment_id/tasks
Read all deployment tasks
---
GET /v5/ibm/backups/:backup_id
Read all deployment backups
---
POST /v5/ibm/deployments/:deployment_id/backups
Create an on-demand backup
---
GET /v5/ibm/deployments/:deployment_id/backups
Read all deployment remotes
---
POST /v5/ibm/deployments/:deployment_id/remotes/resync
Resync remote replica
---
GET /v5/ibm/deployables/:deployable_id/groups
Read all deployment groups
---
PATCH /v5/ibm/deployments/:deployment_id/groups/:group_id
Read deployment group
---
DELETE /v5/ibm/deployments/:deployment_id/management/database_connections
Kill all database connections
---
PATCH /v5/ibm/deployments/:deployment_id/configuration
Update deployment configuration
---
GET /v5/ibm/deployments/:deployment_id/configuration/schema
Read deployment configuration schema
---
POST /v5/ibm/deployments/:deployment_id/users/:user_type
Create a user based on user type
---
PATCH /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id
Update a DeploymentUser
---
DELETE /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id
Remove a user based on user type
---
GET /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Read deployment user connections
---
POST /v5/ibm/deployments/:deployment_id/users/:user_type/:user_id/connections/:endpoint_type
Create deployment user connections
---
GET /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Read Allowlisted IP Addresses
---
POST /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Create an Allowlisted IP Addresses
---
DELETE /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses/:ip_address_id
Remove an Allowlisted IP Addresses
---
PUT /v5/ibm/deployments/:deployment_id/allowlists/ip_addresses
Bulk allowlist IP addresses
---
POST /v5/ibm/deployments/:deployment_id/elasticsearch/file_syncs
Create elasticsearch file sync
```
