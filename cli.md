---

copyright:
  years: 2026
lastupdated: "2026-05-21"

keywords: cloud databases, migrating, disk size, memory size, CPU size, resources, cli, postgresql administrator, cloud database cli

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} CLI
{: #cdb-reference}

[Gen 2]{: tag-purple}


To interact with {{site.data.keyword.databases-for}} on Gen 2 via the CLI you must utilize the IBM Cloud Resource Controller's CLI. For more info please see [General {{site.data.keyword.cloud}} CLI (ibmcloud) commands](/docs/cli?topic=cli-ibmcloud_cli).

The {{site.data.keyword.databases-for}} plugin supports only Gen 1 instances. For Gen 2 instances, use the Resource Controller CLI.
{: note}

## Getting started - Create an instance
{: #ibmcloud-cdb-help-create}

You can create an instance by using the following command:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP>
```
{: .pre}

Example of full command for {{site.data.keyword.databases-for-postgresql}}:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP>  -p '{
   "dataservices":{
      "postgresql": {
         "storage_gb": 10,
         "members": 2,
         "host_flavor": "b3c.8x32.encrypted",
         "version": "NUMBER"
      },
      "encryption": {
         "disk": "crn:v1..."
      },
      "$schema": {
         "version": "1.0.0"
      }
   }
}'
```
{: .pre}

Example of full command for {{site.data.keyword.databases-for-mongodb}}:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP> -p '{
   "dataservices":{
      "mongodb": {
         "storage_gb": 10,
         "host_flavor": "b3c.8x32.encrypted",
         "version": "NUMBER"
      },
      "encryption": {
         "disk": "crn:v1..."
      },
      "$schema": {
         "version": "1.0.0"
      }
   }
}'
```
{: .pre}

Full command for {{site.data.keyword.messagehub}}:

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP> -p '{
   "dataservices":{
      "kafka": {
        "throughput_mb_s": 1000,
        "storage_gb": 200
      },
      "encryption": {
         "disk": "crn:v1..."
      },
      "$schema": {
         "version": "1.0.0"
      }
   }
}'
```
{: .pre}

## Getting information about your instance
{: #ibmcloud-cdb-getting-info}

You can get instance information using the following command:

```sh
ibmcloud resource service-instance <INSTANCE_NAME> -o JSON
```
{: .pre}

## Update your instance
{: #ibmcloud-cdb-update-instance}

To update your instance (this includes operations, such as scaling and modifying other parts of your service), use the following command:

```sh
ibmcloud resource service-instance-update <INSTANCE_NAME> -p '<{FIELDS_TO_UPDATE}>'
```
{: .pre}

Example of full updates for {{site.data.keyword.databases-for-postgresql}}:

```sh
ibmcloud resource service-instance-update <INSTANCE_NAME> -p'{
   "dataservices":{
      "postgresql": {
         "storage_gb": 10, <------ Change to the value you desire
         "members": 2, <------ Change to the value you desire
         "host_flavor": "b3c.8x32.encrypted" <------ Change to the value you desire
      },
   }
}'
```
{: .pre}

Example of full updates for {{site.data.keyword.databases-for-mongodb}}:

```sh
ibmcloud resource service-instance-update <INSTANCE_NAME> -p'{
   "dataservices":{
      "mongodb": {
         "storage_gb": 10, <------ Change to the value you desire
         "host_flavor": "b3c.8x32.encrypted" <------ Change to the value you desire
      },
   }
}'
```
{: .pre}

Example of full updates for {{site.data.keyword.messagehub}}:

```sh
ibmcloud resource service-instance-update <INSTANCE_NAME> -p'{
   "dataservices":{
      "kafka": {
         "throughput_mb_s": 1000, <------ Change to the value you desire
         "storage_gb": 200 <------ Change to the value you desire
      },
   }
}'
```
{: .pre}

## Restore an {{site.data.keyword.databases-for-postgresql}} or {{site.data.keyword.databases-for-mongodb}} instance
{: #ibmcloud-cdb-restore-instance}

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP>  -p '{
   "dataservices":{
      "restore_backup_id": "crn:v1...123-456-7890"
   }
}'
```
{: .pre}

## Create and list backups
{: #ibmcloud-cdb-create-backups}

This is currently not available via the CLI. To create or list a backup, use the UI.

## Manage users
{: #ibmcloud-cdb-manage-users}

To create a user:

```sh
ibmcloud resource service-key-create NAME [ROLE_NAME] ( --instance-id SERVICE_INSTANCE_ID | --instance-name SERVICE_INSTANCE_NAME) [--service-id SERVICE_ID]
```
{: .pre}

To delete a user:

```sh
ibmcloud resource service-key-delete ( NAME | ID ) [-g RESOURCE_GROUP]
```
{: .pre}

Updating a user is not possible for Gen 2 instances.
{: note}

## Manage IP addresses (Allowlisting)
{: #ibmcloud-cdb-allowlisting}

{{site.data.keyword.databases-for}} utilizes context-based restrictions for its allowlisting needs. To manage your IP address via the CLI, see [Context-based restrictions CLI plug-in](/docs/account?topic=account-cbr-plugin).
