---

copyright:
  years: 2026
lastupdated: "2026-07-15"

subcollection: cloud-databases-gen2

keywords: api

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} API
{: #api}

[Gen 2]{: tag-purple}


The {{site.data.keyword.databases-for}} API generally utilizes the [Resource Controller API](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#intro) for operation purposes. Use this API document to work with your data services.
{: note}

## Authentication
{: #api-authentication}

Access to the API uses token authentication, by using the header `Authorization: Bearer <token>`. The token must be [IAM-issued](/apidocs/iam-identity-token-api). You can send in an IAM API key directly as the token or [use the API key to generate an IAM bearer token](/docs/iam?topic=iam-iamtoken_from_apikey&interface=ui).

To call each method, you'll need to be [assigned a role](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-iam) that includes the required IAM actions. Each method lists the associated action. For more information about IAM actions and how they map to roles, see [Managing access for {{site.data.keyword.cloud}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-iam).

## Error handling
{: #api-error-handling}

The API uses standard `HTTP` response codes to indicate whether a method completed successfully. A `200` response always indicates success. A `4xx` type response is some sort of failure, and a `500` type response usually indicates an internal system error. Any of these responses might be accompanied by a JSON formatted body that contains more detailed error information.

## Event tracking
{: #api-event-tracking}

You can monitor API activity within your account by using the [{{site.data.keyword.cloudaccesstraillong}}](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-at_events&interface=terraform) service. Whenever an API method is called, an event is generated that you can then track and audit from within Activity Tracker. The specific event type is listed for each individual method.



## Deployment IDs and CRNs
{: #api-deployment}

Deployment IDs are CRNs on the Cloud Data Services platform. When you use the CRN, remember to URL encode the CRN value as it might include the forward-slash (/) %2F character.

Example: The following CRN

```sh
   crn:v1:bluemix:public:databases-for-redis:us-south:a/274074dce64e9c423ffc238516c755e1:29caf0e7-120f-4da8-9551-3abf57ebcfc7::
   ```
{: pre}

becomes as follows when URL encoded.

```sh
   crn:v1:bluemix:public:databases-for-redis:us-south:a%2F274074dce64e9c423ffc238516c755e1:29caf0e7-120f-4da8-9551-3abf57ebcfc7::
   ```
{: pre}


## Pagination
{: #api-pagination}

No endpoint currently returns paginated data.

## Rate limiting
{: #api-rate-limiting}

No endpoint currently implements rate limiting.

## Methods
{: #api-methods}

#### List all deployed products
{: #api-methods-list-deployed}

Returns a list of all deployed cloud services.

```sh
GET /v2/resource_instances
```
{: pre}

Example request:

```sh
curl -X GET https://resource-controller.cloud.ibm.com/v2/resource_instances -H "Authorization: Bearer <IAM token>"
```
{: pre}

Example response:

```sh
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

#### Get deployment information
{: #api-methods-get-deployment}

Gets the full data that is associated with a deployment. This data includes the ID, name, database type, and version.

```sh
GET /v2/resource_instances/{id}`
```
{: pre}

Example request:

```sh
curl -X GET https://resource-controller.cloud.ibm.com/v2/resource_instances/95004d03-9fec-443b-9f6e-083f2b25e73a -H "Authorization: Bearer <IAM token>" \
```
{: pre}

Example response:

```sh
{
	"id": "crn:v1:bluemix:public:databases-for-postgresql:us-east:a/23b09aee04da4545b6e32805fa93249d:95004d03-9fec-443b-9f6e-083f2b25e73a::",
	"guid": "95004d03-9fec-443b-9f6e-083f2b25e73a",
	"url": "/v2/resource_instances/95004d03-9fec-443b-9f6e-083f2b25e73a",
	"created_at": "2026-07-02T14:04:29.613949688Z",
	"updated_at": "2026-07-02T14:15:54.226535327Z",
	"deleted_at": null,
	"created_by": "Id-4700030B2K",
	"updated_by": "",
	"deleted_by": "",
	"scheduled_reclaim_at": null,
	"restored_at": null,
	"scheduled_reclaim_by": "",
	"restored_by": "",
	"name": "Databases for PostgreSQL-3b",
	"region_id": "us-east",
	"account_id": "23b09aee04da4545b6e32805fa93249d",
	"reseller_channel_id": "",
	"resource_plan_id": "databases-for-postgresql-gen2-standard",
	"resource_group_id": "c21a4e8564c14d1aab2a9a8b441904eb",
	"resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/23b09aee04da4545b6e32805fa93249d::resource-group:c21a4e8564c14d1aab2a9a8b441904eb",
	"target_crn": "crn:v1:bluemix:public:globalcatalog::::deployment:databases-for-postgresql-standard-gen2%3Aus-east",
	"parameters": {
		"dataservices": {
			"postgresql": {
				"host_flavor": "bx3d.4x20",
				"members": 2,
				"storage_gb": 10,
				"version": "18"
			}
		}
	},
	"allow_cleanup": false,
	"crn": "crn:v1:bluemix:public:databases-for-postgresql:us-east:a/23b09aee04da4545b6e32805fa93249d:95004d03-9fec-443b-9f6e-083f2b25e73a::",
	"state": "active",
	"type": "service_instance",
	"sub_type": "Public",
	"resource_id": "databases-for-postgresql",
	"dashboard_url": null,
	"last_operation": {
		"type": "create",
		"state": "succeeded",
		"async": true,
		"description": "Provision completed successfully",
		"cancelable": true,
		"poll": true
	},
	"resource_keys_url": "/v2/resource_instances/95004d03-9fec-443b-9f6e-083f2b25e73a/resource_keys",
	"plan_history": [
		{
			"resource_plan_id": "databases-for-postgresql-gen2-standard",
			"start_date": "2026-07-02T14:04:29.613949688Z",
			"requestor_id": "Id-4700030B2K"
		}
	],
	"migrated": false,
	"extensions": {
		"dataservices": {
			"$schema": {
				"version": "1.0.0"
			},
			"connection": {
				"cli": {
					"arguments": [
						"host=95004d03-9fec-443b-9f6e-083f2b25e73a.private.uhp.postgresql.us-east.dataservices.appdomain.cloud port=5432 dbname=postgres user=$PGUSER password=$PGPASSWORD sslmode=verify-full"
					],
					"bin": "psql",
					"composed": [
						"PGUSER=$PGUSER PGPASSWORD=$PGPASSWORD PGSSLMODE=verify-full PGSSLROOTCERT=system psql 'host=95004d03-9fec-443b-9f6e-083f2b25e73a.private.uhp.postgresql.us-east.dataservices.appdomain.cloud port=5432 dbname=postgres'"
					],
					"environment": {
						"PGPASSWORD": "$PGPASSWORD",
						"PGSSLMODE": "verify-full",
						"PGSSLROOTCERT": "system",
						"PGUSER": "$PGUSER"
					},
					"type": "cli"
				},
				"postgres": {
					"authentication": {
						"method": "direct",
						"password": "$PGPASSWORD",
						"username": "$PGUSER"
					},
					"composed": [
						"postgres://$PGUSER:$PGPASSWORD@95004d03-9fec-443b-9f6e-083f2b25e73a.private.uhp.postgresql.us-east.dataservices.appdomain.cloud:5432/postgres?sslmode=verify-full"
					],
					"database": "postgres",
					"hosts": [
						{
							"hostname": "95004d03-9fec-443b-9f6e-083f2b25e73a.private.uhp.postgresql.us-east.dataservices.appdomain.cloud",
							"port": 5432
						}
					],
					"path": "/postgres",
					"port": 5432,
					"query_options": {
						"sslmode": "verify-full"
					},
					"scheme": "postgres",
					"type": "uri"
				}
			},
			"postgresql": {
				"configuration": {
					"max_connections": 115
				},
				"cpu_count": 4,
				"host_flavor": "bx3d.4x20",
				"members": 2,
				"memory_gb": 20,
				"storage_gb": 10,
				"version": "18"
			}
		},
		"virtual_private_endpoints": {
			"dns_domain": "95004d03-9fec-443b-9f6e-083f2b25e73a.private.uhp.postgresql.us-east.dataservices.appdomain.cloud",
			"dns_hosts": [
				"",
				"*"
			],
			"endpoints": [
				{
					"ip_address": "10.51.217.34",
					"zone": "us-east-1"
				},
				{
					"ip_address": "10.51.219.57",
					"zone": "us-east-2"
				},
				{
					"ip_address": "10.51.221.12",
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
	"controlled_by": "",
	"locked": false,
	"onetime_credentials": false
}
```
{: pre}

#### How to manage and update your database configuration
{: #api-manage-config}

```sh
POST /v2/resource_instances
```
{: pre}

Example request:

```sh
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

#### How to scale your database
{: #api-scale-db}

```sh
POST /v2/resource_instances
```
{: pre}

Example request:

```sh
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

## Transition documentation
{: #api-transition-doc}

Information you can expect to get back:

- The last task you have conducted is seen under `last_operation`.
- Product connection information under connection parameter.
- Product specific information under the product object (for example, postgresql).
