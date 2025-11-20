---
 
copyright:
  years: 2025, 2025
lastupdated: "2025-11-20"

keywords: cloud databases, migrating, disk size, memory size, CPU size, resources, cli, postgresql administrator, cloud database cli

subcollection: cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} CLI
{: #cdb-reference}

To interact with Cloud Data Services on VPC via the CLI you must utilize the IBM Cloud Resource Controller's CLI. For more info please see [General IBM Cloud CLI (ibmcloud) commands](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_cli).


## Getting started - Create an instance
{: #ibmcloud-cdb-help-create}

You can create an instance by using the following command: 

```sh
ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN_NAME> <LOCATION> -g <RESOURCE_GROUP>
```
{: .pre}


Example of Full command for Postgresql
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


Example of Full command for MongoDB
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


Full command for Event Streams
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

## Getting Information About Your Instance


You can get instance information using the following command: 

```sh
ibmcloud resource service-instance <INSTANCE_NAME> -o JSON
```
{: .pre}

## Update Your Instance

To update your instance (this includes operations like scaling and modifying other parts of your service), use the following command:

```sh
ibmcloud resource service-instance-update <INSTANCE_NAME> -p '<{FIELDS_TO_UPDATE}>'
```

Example of Full Updates for Postgresql
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

Example of Full Updates for MongoDB
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

Example of Full Updates for Event Streams
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

## Restoring a Postgresql or MongoDB Instance

See creating an instance. It follows the same flow.

## Creating and Listing Backups

This is not available via the CLI at the time being. To create or list a backup please utilize the UI

## Manage Users

!!!!Reach out to Doug Cowie and David Piteria to understand if this is possible via the CLI!!!

## Managing IP Addresses (aka Allowlisting)

Cloud Data Services utilizes Context-based restrictions for its allowlisting needs. To manage your IP address via the CLI please see [Context-based restrictions CLI plug-in](https://cloud.ibm.com/docs/account?topic=account-cbr-plugin).
