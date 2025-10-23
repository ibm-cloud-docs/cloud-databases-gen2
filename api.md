---

copyright:
  years: 2025
lastupdated: "2025-10-23"

subcollection: cloud-databases-gen2

keywords: api

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} API
{: #api}

The {{site.data.keyword.databases-for}} API generally utilizes the [Resource Controller API](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#intro) for operation purposes. Use this API document to work with your data services.

## Authentication
{: #api-authentication}

Access to the API uses token authentication, by using the header Authorization: Bearer <token>. The token must be IAM-issued. You can send in an IAM API key directly as the token 
or use the API key to generate an IAM Bearer Token.

To call each method, you'll need to be assigned a role that includes the required IAM actions. Each method lists the associated action. For more information about IAM actions 
and how they map to roles, see Managing access for IBM Cloud.

## Error Handling
{: #api-error-handling}

The API uses standard HTTP response codes to indicate whether a method completed successfully. A 200 response always indicates success. A 4xx type response is some sort of failure, 
and a 500 type response usually indicates an internal system error. Any of these responses might be accompanied by a JSON formatted body that contains more detailed error information.

## Event tracking
{: #api-event-tracking}

You can monitor API activity within your account by using the IBM Cloud Activity Tracker service. Whenever an API method is called, an event is generated that you can then track 
and audit from within Activity Tracker. The specific event type is listed for each individual method.

For more information about how to track Certificate Manager activity, see [Auditing events for IBM Cloud]() <— THIS LINK IS BROKEN.

## Deployment IDs and CRNs
{: #api-deployment}

Deployment IDs are CRNs on the Cloud Data Services platform. When you use the CRN, remember to URL encode the CRN value as it might include the forward-slash (/) %2F character. 
For example,

`crn:v1:bluemix:public:databases-for-redis:us-south:a/274074dce64e9c423ffc238516c755e1:29caf0e7-120f-4da8-9551-3abf57ebcfc7::`

becomes

`crn:v1:bluemix:public:databases-for-redis:us-south:a%2F274074dce64e9c423ffc238516c755e1:29caf0e7-120f-4da8-9551-3abf57ebcfc7::`

when URL encoded.

## Pagination
{: #api-pagination}

No endpoint currently returns paginated data.

## Rate Limiting
{: #api-rate-limiting}

No endpoint currently implements rate limiting.

## Methods
{: #api-methods}

### List all deployed products
{: #api-methods-list-deployed}

Returns a list of all deployed cloud services.

`GET /v2/resource_instances`

Example request:

```curl
curl -X GET https://resource-controller.cloud.ibm.com/v2/resource_instances -H "Authorization: Bearer <IAM token>"
```
{: pre}

Example response:

```curl
Name:                test-mysql-01
Location:            us-south
Family:              resource_controller
Resource Type:       resource-instance
Resource Group ID:   eb922ba0717f47589ca26d202c5cc915
CRN:                 crn:v1:bluemix:public:databases-for-mysql:us-south:a/40ddc34a953a8c02f10987b59085b60e:09a8b8a3-29cf-4c1b-85ad-35e25611a414::
Tags:
Service Tags:
Access Tags:

Name:                test-mysql-02
Location:            us-south
Family:              resource_controller
Resource Type:       resource-instance
Resource Group ID:   eb922ba0717f47589ca26d202c5cc915
CRN:                 crn:v1:bluemix:public:databases-for-mysql:us-south:a/40ddc34a953a8c02f10987b59085b60e:3a81147c-ae5a-48c4-a0e5-cbf3e88cf215::
Tags:
Service Tags:
Access Tags:
```
{: pre}

### Get deployment information
{: #api-methods-get-deployment}

Gets the full data that is associated with a deployment. This data includes the ID, name, database type, and version.

`GET /v2/resource_instances/{id}`

Example request:

curl -X GET https://resource-controller.cloud.ibm.com/v2/resource_instances/8d7af921-b136-4078-9666-081bd8470d94 -H "Authorization: Bearer <IAM token>" \

Example response:

```curl
[
    {
        "guid": "5aa314a5-76d9-4440-8e84-faa343d40127",
        "id": "crn:v1:staging:public:databases-for-postgresql-cdp-dev:us-east:a/cf8d4161fa0243b9a2a5494cd7ff66b7:5aa314a5-76d9-4440-8e84-faa343d40127::",
        "url": "/v2/resource_instances/5aa314a5-76d9-4440-8e84-faa343d40127",
        "created_at": "2025-08-28T16:35:07.650372748Z",
        "updated_at": "2025-08-28T16:41:53.419092609Z",
        "deleted_at": null,
        "name": "omar-pg-cdp-test",
        "region_id": "us-east",
        "account_id": "cf8d4161fa0243b9a2a5494cd7ff66b7",
        "resource_plan_id": "databases-for-postgresql-cdp-dev-standard",
        "resource_group_id": "97bc590fddc845ee903645bce8771bab",
        "crn": "crn:v1:staging:public:databases-for-postgresql-cdp-dev:us-east:a/cf8d4161fa0243b9a2a5494cd7ff66b7:5aa314a5-76d9-4440-8e84-faa343d40127::",
        "extensions": {
          "dataservices": {
            "resources": {
              "database": {
                "storage_gb": 10,
                "members": 2,
                "host_flavor": "b3c.8x32.encrypted"
              }
            },
            "connection": {
                "cli": {
                    "arguments": [
                        "host=5aa314a5-76d9-4440-8e84-faa343d40127.private.axd.us-east.postgresql.dataservices.dev.appdomain.cloud port=5432 dbname=postgres user=$PGUSER password=$PGPASSWORD"
                    ],
                    "bin": "psql",
                    "composed": [
                        "psql 'host=5aa314a5-76d9-4440-8e84-faa343d40127.private.axd.us-east.postgresql.dataservices.dev.appdomain.cloud port=5432 dbname=postgres user=$PGUSER password=$PGPASSWORD'"
                    ],
                    "type": "cli"
                },
                "postgres": {
                    "composed": [
                        "postgres://$PGUSER:$PGPASSWORD@5aa314a5-76d9-4440-8e84-faa343d40127.private.axd.us-east.postgresql.dataservices.dev.appdomain.cloud:5432/postgres"
                    ],
                    "database": "postgres",
                    "hosts": [
                        {
                            "hostname": "5aa314a5-76d9-4440-8e84-faa343d40127.private.axd.us-east.postgresql.dataservices.dev.appdomain.cloud",
                            "port": 5432
                        }
                    ],
                    "path": "/postgres",
                    "port": 5432,
                    "query_options": {
                        "sslmode": "require"
                    },
                    "scheme": "postgres",
                    "type": "uri"
                }
            },
            "encryption": {
              "disk": "crn:v1..."
            },
            "endpoints": "private",
            "version": "18",
            "$schema": {
              "version": "1.0.0"
            },
            "virtual_private_endpoints": {
                    "dns_domain": "private.axd.us-east.postgresql.dataservices.dev.appdomain.cloud",
                    "dns_hosts": [
                        "5aa314a5-76d9-4440-8e84-faa343d40127",
                        "*.5aa314a5-76d9-4440-8e84-faa343d40127"
                    ],
                    "endpoints": [
                        {
                            "ip_address": "10.16.117.27",
                            "zone": "us-east-1"
                        },
                        {
                            "ip_address": "10.16.119.1",
                            "zone": "us-east-2"
                        },
                        {
                            "ip_address": "10.16.123.0",
                            "zone": "us-east-3"
                        }
                    ],
                    "origin_type": "vpc",
                    "ports": [
                        {
                            "port_max": 5432,
                            "port_min": 5432
                        }
                    ]
                }
            },
          }
        }
        "create_time": 0,
        "created_by": "IBMid-5500013U80",
        "state": "active",
        "type": "service_instance",
        "resource_id": "0de4305b-b472-449d-b369-07d14bba2d1d",
        "dashboard_url": null,
        "allow_cleanup": false,
        "locked": false,
        "onetime_credentials": true,
        "last_operation": {
            "type": "create",
            "state": "succeeded",
            "description": "Provision completed successfully",
            "updated_at": null,
            "cancelable": true
        },
        "account_url": "",
        "resource_plan_url": "",
        "resource_bindings_url": "/v2/resource_instances/5aa314a5-76d9-4440-8e84-faa343d40127/resource_bindings",
        "resource_aliases_url": "/v2/resource_instances/5aa314a5-76d9-4440-8e84-faa343d40127/resource_aliases",
        "siblings_url": "",
        "target_crn": "crn:v1:staging:public:globalcatalog::::deployment:databases-for-postgresql-cdp-dev-standard-deployment-us-east-72d307a5"
    }
]
```
{: pre}

### How to manage and update your database configuration

`POST /v2/resource_instances`

Example request:

```curl
curl -X POST https://resource-controller.cloud.ibm.com/v2/resource_instances -H "Authorization: Bearer <IAM token>" -H 'Content-Type: application/json' -d '{
    "name": "my-instance",
    "target": "ca-mon",
    "resource_group": "5c49eabc-f5e8-5881-a37e-2d100a33b3df",
    "resource_plan_id": "databases-for-postgresql-standard",
    "dataservices": {
      "resources": {
        "database": {
          "storage_gb": 10,
          "members": 2,
          "host_flavor": "b3c.8x32.encrypted"
        }
      },
      "encryption": {
        "disk": "crn:v1..."
      },
      "version": "18",
      "$schema": {
        "version": "1.0.0"
      }
    },
  }'

Input Parameters

   "dataservices": Object

{

      "resources":  Object

{

        "database": Object

{

          "storage_gb":  Integer,

          "members": Integer,

          "host_flavor": String

      }

      },

      "encryption":  Object

{

        "disk": String

      },

      "version": String,

      "$schema": Object

{

        "version": String

      }

   },
```
{: pre}

### How to scale your database

`POST /v2/resource_instances`

Example request:

```curl
curl -X POST https://resource-controller.cloud.ibm.com/v2/resource_instances -H "Authorization: Bearer <IAM token>" -H 'Content-Type: application/json' -d '{
    "name": "my-instance",
    "target": "ca-mon",
    "resource_group": "5c49eabc-f5e8-5881-a37e-2d100a33b3df",
    "resource_plan_id": "databases-for-postgresql-standard",
    "dataservices": {
      "$schema": {
          "version": "1.0.0"
      },
      "resources": {
          "database": {
              "host_flavor": "bx2.4x16", <--- UPDATE
              "members": 1, <--- UPDATE
              "storage_gb": 10 <--- UPDATE
          }
      },
      "version": "18"
    },
  }'

Input Parameters

   "dataservices": Object

{

      "resources":  Object

{

        "database": Object

{

          "storage_gb":  Integer,

          "members": Integer,

          "host_flavor": String

      }

      },

}
```
{: pre}

Get the schema of the database configuration (INFO SEEMS TO BE MISSING)

## Transition doc


Information you can expect to get back:

The last task you have conducted is seen under the `last_operation`

Product connection information under connection parameter

Product specific information under the product object (e.g. postgresql)

Creates a user based on user type - TBD

Deletes a user based on user type - TBD

Update your database configuration (INFO SEEMS TO BE MISSING)


### Methods not available for MVP

- List read-only replica information
- Resync read-only replica
- Promote read-only replica to a full deployment
- Get information about a backup
- Get earliest point-in-time-recovery timestamp
- Get the autoscaling configuration from a deployment
- Set the autoscaling configuration from a deployment
- Kill connections to a PostgreSQL or EnterpriseDB deployment
- Sync files uploaded to Elasticsearch deployment
- Create a new logical replication slot
- Delete a logical replication slot
- Discover capability information from a backup
- Upgrade your database version

Waiting for CBR implementation:

- Retrieve the allowlisted addresses and ranges for a deployment.
- Set the allowlist for a deployment.
- Add an address or range to the allowlist for a deployment.
- Delete an address or range from the allowlist of a deployment.

Migrated to GC: 

- Discover capability information.
- Discover capability information from a deployment.

Limitations

- Getting backup information is only available via our UI.
- List currently available backups from a deployment.
- Listing backups is only available via our UI.
- Initiate an on-demand backup (INFO SEEMS TO BE MISSING HERE)
- Creating backups is only available via our UI.


List currently available scaling groups from a deployment

Needs documentation from product detailing all the available host flavors and scaling values associated with out products

Set scaling values on a specified product.
