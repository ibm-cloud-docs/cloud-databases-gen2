---

copyright:
  years: 2026
lastupdated: "2026-10-21"

keywords: maintenance window, maintenance start time, scheduled maintenance, emergency maintenance, postgresql maintenance window, mongodb maintenance window

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Customer-defined maintenance windows
{: #maintenance-windows}

[Gen 2]{: tag-purple}

Set the days and start time for maintenance on your deployment. {{site.data.keyword.databases-for}} controls the duration of the maintenance window, and all maintenance work is completed or stopped within 4 hours of your scheduled start time.
{: shortdesc}

## Availability
{: #maintenance-windows-availability}

Customer-defined maintenance windows are available for:

- {{site.data.keyword.databases-for-postgresql}} in `eu-de`.
- {{site.data.keyword.databases-for-mongodb}} Enterprise Edition in `eu-de`. 

Support for more databases and regions will be added over time.

Configure a daily maintenance window unless your organization requires maintenance to run on specific days only. A daily window allows pending or incomplete maintenance, 
including security and reliability updates, to resume the next day rather than waiting until the next week.
{: tip}

## What maintenance includes
{: #maintenance-windows-scope}

Maintenance includes any change that directly affects your deployment, such as:

- Database software and image updates.
- Updates to the worker nodes that your deployment runs on.
- Security, reliability, and supportability updates.

These changes run during your maintenance window, even when they don't cause a visible service impact. Changes that you request yourself, such as scaling your deployment, run when you request them.

During maintenance, your deployment might fail over to a new primary. Make sure that your applications can reconnect automatically. 
For more information, see [High availability](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-ha-dr).

## Default maintenance window
{: #maintenance-windows-default}

You don't have to set a maintenance window. If you don't, {{site.data.keyword.databases-for}} uses the regional default: a start time between 23:00 UTC and 10:00 UTC, Monday to Friday. The exact start time isn't shown.

To go back to the regional default after you set your own window, set `system_assigned` to `true`.

## Maintenance window requirements
{: #maintenance-windows-requirements}

- You can set only a start time. You can't set a duration or end time. {{site.data.keyword.databases-for}} controls the length of the maintenance window.
- Specify the start time in UTC by using the `hh:mmZ` format.
- Select at least one maintenance day per week. A daily maintenance window is recommended. For more information, see [If maintenance doesn't finish in time](#maintenance-windows-incomplete).
- Set your start time at least 60 minutes before the maintenance window that you want it to apply to.
- You can update your maintenance window at any time. Changes take effect for the next eligible maintenance window. If maintenance has already completed for the day, the updated schedule takes effect the next time maintenance is eligible to run.
- If you update the maintenance window while maintenance is in progress, the current maintenance operation isn't restarted. The updated schedule applies to the next eligible maintenance window.
- Maintenance notifications are based on the schedule in effect when the notification is generated. Changes made shortly before a maintenance window might not apply to notifications that were already generated or sent.

## How maintenance windows work
{: #maintenance-windows-how}

The maintenance window lasts 4 hours from the scheduled start time, and all maintenance work is completed or stopped within that period.

For example, if your maintenance start time is 02:00 UTC:

| Time (UTC) | What happens |
|------------|--------------|
| 02:00 - 6:00 | Maintenance begins, and maintenance activities are initiated. Your deployment might switch over to a new primary, and your applications might need to reconnect.|
| By 06:00 | All maintenance work is completed or stopped. |
{: caption="Example maintenance window with a start time of 02:00 UTC" caption-side="bottom"}

When you choose a start time, plan for the full 4-hour window, not just the start time. Choose a time when your application has the least traffic and your operations team is available.

Your backups never overlap with your maintenance window. {{site.data.keyword.databases-for}} adjusts the backup schedule automatically.

## Set a maintenance window
{: #maintenance-windows-set}

You can set your maintenance days and start time by using the console, CLI, API, or Terraform.

### Set a maintenance window in the console
{: #maintenance-windows-ui}
{: ui}

You can configure a maintenance window when you create a deployment or after provisioning.

1. In the {{site.data.keyword.cloud_notm}} console, create a deployment or open an existing deployment.
1. Go to **Maintenance window** and click **Edit**.
1. Select the days of the week when maintenance can start. A daily maintenance schedule is recommended.
1. Select a maintenance start time. You can display the time in UTC or your local time zone.
1. Review the maintenance schedule and click **Save**.

To return to the regional default maintenance window, click **Reset to default**.

### Set a maintenance window by using the CLI
{: #maintenance-windows-cli}
{: cli}

You can set a specific maintenance window by using the following command:

```sh
ibmcloud resource service-instance-create \
  <INSTANCE_NAME> \
  <SERVICE_NAME> \
  <SERVICE_PLAN_NAME> \
  <LOCATION> \
  -g <RESOURCE_GROUP> \
  -p '{
    "dataservices": {
      "maintenance": {
        "window": {
          "start_time": "05:00Z",
          "days": "Wednesday,Thursday"
        }
      }
    }
  }'
```
{: pre}

You can set `system_assigned` maintenance window by using the following commands:

```sh
ibmcloud resource service-instance-create \
  <INSTANCE_NAME> \
  <SERVICE_NAME> \
  <SERVICE_PLAN_NAME> \
  <LOCATION> \
  -g <RESOURCE_GROUP> \
  -p '{
    "dataservices": {
      "maintenance": {
        "window": {
          "system_assigned": true
        }
      }
    }
  }'
```
{: pre}

### Set a maintenance window by using the API
{: #maintenance-windows-api}
{: api}

You can set a specific maintenance window by using the following request:

```sh
curl -X POST \
  "https://resource-controller.cloud.ibm.com/v2/resource_instances" \
  -H "Authorization: Bearer <IAM_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "<DATABASE_INSTANCE_NAME>",
    "target": "<REGION>",
    "resource_group": "<RESOURCE_GROUP_ID>",
    "resource_plan_id": "<DATABASE_SERVICE_PLAN_ID>",
    "parameters": {
      "dataservices": {
        "maintenance": {
          "window": {
            "start_time": "05:00Z",
            "days": "Wednesday,Thursday"
          }
        }
      }
    }
  }'
```
{: pre}

You can set `system_assigned` maintenance window by using the following request:

```sh
curl -X POST \
  "https://resource-controller.cloud.ibm.com/v2/resource_instances" \
  -H "Authorization: Bearer <IAM_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "<DATABASE_INSTANCE_NAME>",
    "target": "<REGION>",
    "resource_group": "<RESOURCE_GROUP_ID>",
    "resource_plan_id": "<DATABASE_SERVICE_PLAN_ID>",
    "parameters": {
      "dataservices": {
        "maintenance": {
          "window": {
            "system_assigned": true
          }
        }
      }
    }
  }'
```
{: pre}


## Set a maintenance window by using Terraform
{: #maintenance-windows-tf}
{: terraform}

You can set a specific maintenance window by using the following Terraform request:

```sh
maintenance_days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

data "ibm_resource_group" "rg" {
  name = var.resource_group_name
}

resource "ibm_database" "cmw_test" {
  name              = "<DATABASE_INSTANCE_NAME>"
  resource_group_id = data.ibm_resource_group.rg.id
  service = "<DATABASE_SERVICE_NAME>"
  plan    = "<DATABASE_SERVICE_PLAN_ID>"
  location          = "<GEN2-REGION>"
  service_endpoints = "private"
  maintenance {
    window {
      start_time = "05:00Z"
      days       = var.maintenance_days
    }
  }
}
```
{: pre}

You can set `system_assigned` maintenance window by using the following Terraform request:

```sh
data "ibm_resource_group" "rg" {
  name = var.resource_group_name
}

resource "ibm_database" "cmw_test" {
  name              = "<DATABASE_INSTANCE_NAME>"
  resource_group_id = data.ibm_resource_group.rg.id
  service = "<DATABASE_SERVICE_NAME>"
  plan    = "<DATABASE_SERVICE_PLAN_ID>"
  location          = "<GEN2-REGION>"
  service_endpoints = "private"
  maintenance {
    window {
      system_assigned = true
    }
  }
}
```
{: pre}


## Tracking maintenance
{: #maintenance-windows-tracking}

When maintenance is pending for your deployment, you receive an {{site.data.keyword.at_full_notm}} event at least 2 hours before your maintenance activity starts. 

{{site.data.keyword.at_full_notm}} events are also triggeered as a result of any service instance update due to a successful maintenance window. Check out the full list of Database [{{site.data.keyword.at_short}} events](/docs/cloud-databases?topic=cloud-databases-activity-tracker).

## Incomplete maintenance
{: #maintenance-windows-incomplete}

Maintenance never runs past the end of your maintenance window. If maintenance is still running 4 hours after your start time, {{site.data.keyword.databases-for}} stops it. 
The remaining work runs in your next maintenance window. Your deployment stays available in the meantime.

**Set a daily maintenance window.** If you select only one day each week, maintenance that wasn't completed, including security fixes, waits up to a week for your next window. With a daily window, maintenance resumes the next day, and your deployment stays up to date and secure.
{: important}

## Emergency maintenance
{: #maintenance-windows-emergency}

In exceptional circumstances, such as a critical security vulnerability or a high-severity defect, {{site.data.keyword.IBM_notm}} will apply maintenance outside your maintenance window. Emergency maintenance is used only when waiting for your next maintenance window would put the security or stability of your deployment at risk. Because emergency maintenance is time-sensitive, advance notifications and scheduled maintenance events are not available.
