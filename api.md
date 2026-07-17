---

copyright:
  years: 2026
lastupdated: "2026-07-17"

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

```json
{
  "rows_count": 100,
  "next_url": "/v2/resource_instances?start=<token>",
  "resources": [
    {
      "id": "crn:v1:bluemix:public:databases-for-redis:eu-de:a/40ddc34a953a8c02f10987b59085b60e:07d523b1-6eea-4263-bd03-c17edf355e0b::",
      "guid": "07d523b1-6eea-4263-bd03-c17edf355e0b",
      "url": "/v2/resource_instances/07d523b1-6eea-4263-bd03-c17edf355e0b",
      "created_at": "2026-07-17T06:41:51.267012883Z",
      "updated_at": "2026-07-17T06:42:11.22949657Z",
      "deleted_at": null,
      "created_by": "Id-270000000X",
      "updated_by": "",
      "deleted_by": "",
      "scheduled_reclaim_at": null,
      "restored_at": null,
      "scheduled_reclaim_by": "",
      "restored_by": "",
      "name": "test-redis-gen2",
      "region_id": "eu-de",
      "account_id": "40ddc34a953a8c02f10987b59085b60e",
      "reseller_channel_id": "",
      "resource_plan_id": "databases-for-redis-gen2-standard",
      "resource_group_id": "eb922ba0717f47589ca26d202c5cc915",
      "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/40ddc34a953a8c02f10987b59085b60e::resource-group:eb922ba0717f47589ca26d202c5cc915",
      "target_crn": "crn:v1:bluemix:public:globalcatalog::::deployment:databases-for-redis-standard-gen2%3Aeu-de",
      "parameters": {
        "dataservices": {
          "redis": {
            "host_flavor": "bxf.4x16",
            "members": 2,
            "storage_gb": 15,
            "version": "8.2"
          }
        }
      },
      "allow_cleanup": false,
      "crn": "crn:v1:bluemix:public:databases-for-redis:eu-de:a/40ddc34a953a8c02f10987b59085b60e:07d523b1-6eea-4263-bd03-c17edf355e0b::",
      "state": "provisioning",
      "type": "service_instance",
      "sub_type": "Public",
      "resource_id": "databases-for-redis",
      "dashboard_url": null,
      "last_operation": {
        "type": "create",
        "state": "in progress",
        "async": true,
        "description": "Provision in progress",
        "cancelable": true,
        "poll": true
      },
      "resource_keys_url": "/v2/resource_instances/07d523b1-6eea-4263-bd03-c17edf355e0b/resource_keys",
      "plan_history": [
        {
          "resource_plan_id": "databases-for-redis-gen2-standard",
          "start_date": "2026-07-17T06:41:51.267012883Z",
          "requestor_id": "Id-270000000X"
        }
      ],
      "migrated": false,
      "controlled_by": "",
      "locked": false,
      "onetime_credentials": false
    }
  ]
}
```
{: pre}

Additional resource objects are returned in the `resources` array. Use the `next_url` token to retrieve the next page of results.

### Get deployment information
{: #api-methods-get-deployment}

Gets the full data that is associated with a deployment. This data includes the ID, name, database type, and version.

```sh
GET /v2/resource_instances/{id}
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

You can get the following information from the API response:

- `last_operation` object - Shows the last task you have performed.
- `connection` object - Shows product connection information.
- Product-specific information is shown under the product object (for example, `postgresql`).

### How to provision your database
{: #api-provision}

```sh
POST /v2/resource_instances
```
{: pre}

Example request:

```sh
curl -X POST https://resource-controller.cloud.ibm.com/v2/resource_instances \
  -H "Authorization: Bearer <IAM token>" \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "my-instance",
    "target": "ca-mon",
    "resource_group": "5c49eabc-f5e8-5881-a37e-2d100a33b3df",
    "resource_plan_id": "databases-for-postgresql-gen2-standard",
    "parameters": {
      "dataservices": {
        "postgresql": {
          "storage_gb": 10,
          "members": 2,
          "host_flavor": "b3c.8x32.encrypted",
          "version": "18"
        },
        "encryption": {
          "disk": "crn:v1..."
        },
        "$schema": {
          "version": "1.0.0"
        }
      }
    }
  }'
```
{: pre}

Input Parameters

- `name` (String) - The name of the instance.
- `target` (String) - The region to deploy to (for example, `us-south`, `eu-de`).
- `resource_group` (String) - The ID of the resource group.
- `resource_plan_id` (String) - The plan ID (for example, `databases-for-postgresql-gen2-standard`).
- `parameters` (Object)
   - `dataservices` (Object)
      - `<service>` (Object) - The service name key (for example, `postgresql`, `mysql`).
         - `storage_gb` (Integer) - Storage size in GB.
         - `members` (Integer) - Number of members.
         - `host_flavor` (String) - The host flavor ID (for example, `b3c.8x32.encrypted`).
         - `version` (String) - The database version (for example, `"18"`).
      - `encryption` (Object, optional) - Disk encryption settings.
         - `disk` (String) - CRN of the Key Protect key for disk encryption.
      - `$schema` (Object) - Schema metadata.
         - `version` (String) - Schema version, must be `"1.0.0"`.

#### How to scale your database
{: #api-scale-db}

```sh
PATCH /v2/resource_instances/{id}
```
{: pre}

Example request:

```sh
curl -X PATCH https://resource-controller.cloud.ibm.com/v2/resource_instances/ed9d2c9b-444b-421d-bbc0-503ca8dd3036 \
  -H "Authorization: Bearer <IAM token>" \
  -H 'Content-Type: application/json' \
  -d '{
    "parameters": {
      "dataservices": {
        "postgresql": {
          "storage_gb": 12,
          "members": 2,
          "host_flavor": "bxf.4x16"
        }
      }
    }
  }'
```
{: pre}

Input Parameters

- `parameters` (Object)
   - `dataservices` (Object)
      - `<service>` (Object) - The service name key (for example, `postgresql`, `mysql`).
         - `storage_gb` (Integer) - Storage size in GB.
         - `members` (Integer) - Number of members.
         - `host_flavor` (String) - The host flavor ID (for example, `bxf.4x16`).
