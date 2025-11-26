---

copyright:
  years: 2018, 2025
lastupdated: "2025-11-26"

keywords: activity tracker

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}



# Activity tracking events for {{site.data.keyword.databases-for}}
{: #at_events}

[Gen 2]{: tag-purple}

{{site.data.keyword.databases-for}} Gen 2 is currently in Beta. The Beta plan is provided exclusively for evaluation and testing purposes. It is not covered by warranties, SLAs, or support, and is not intended for production use. For more information, see [Beta reference](/docs/cloud-databases-gen2?topic=cloud-databases-gen2-icd-gen2-beta).
{: beta}

{{site.data.keyword.cloud}} services, such as {{site.data.keyword.databases-for}}, generate activity tracking events that capture changes to the state of a service. These events help you identify critical actions, investigate unusual activity, and support audit and compliance efforts.
{: shortdesc}

With [{{site.data.keyword.atracker_full}}](/docs/atracker?topic=atracker-about), you can direct these events to specific destinations by configuring targets and routes, giving you control over how auditing data is collected and where it is sent. This enables timely investigation of abnormal activity, supports security and compliance needs, and helps meet regulatory audit requirements.

You need an [{{site.data.keyword.logs_full}}](https://cloud.ibm.com/observability/logging) instance to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}}.
{: note}

## Locations where activity tracking events are generated
{: #at-locations}



### Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.databases-for}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |  Paris (`eu-par01`) |
|---------------------------------------------------------------|---------------------|------------------|------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |  [No]{: tag-red}
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

## Enabling activity tracking events for {{site.data.keyword.databases-for}}
{: #at-enable}






Create an {{site.data.keyword.logs_full_notm}} instance and configure {{site.data.keyword.atracker_full_notm}} by setting the routing rule between the {{site.data.keyword.databases-for}} instance and the {{site.data.keyword.logs_full_notm}} target instance. 

## Viewing activity tracking events for {{site.data.keyword.databases-for}}
{: #at-viewing}



Deploy an [{{site.data.keyword.logs_full_notm}}](https://cloud.ibm.com/observability/logging) instance to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the {{site.data.keyword.databases-for}} dashboard
{: #log-launch-integrated}



Select your [{{site.data.keyword.databases-for}}](https://cloud.ibm.com/databases-overview/resources) instance from the databases resource list. Then click on _Overview_ and scroll to the _Observability_ section. Click on *{{site.data.keyword.logs_full_notm}}* to view your logging instances. Click on _Open Dashboard_ to access the logs.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## List of platform events
{: #at_actions_platform}



The following table lists the activity tracking event actions that {{site.data.keyword.databases-for}} and {{site.data.keyword.cloud_notm}} generate.

| Action name | Legacy action name | Description |
| ------- | ------- | ------- |
| `<service_name>.deployment-backup.create`|`<service_id>.backup-ondemand.create` | An on-demand backup of your instance was created. If the backup failed, a "-failure" flag is included in the message. |
|`<service_name>.deployment-backup-scheduled.create`| `<service_id>.backup-scheduled.create`| A scheduled backup of your instance was created. If the backup failed, a "-failure" flag is included in the message. |
|`<service_name>.deployment-user.update`|`<service_id>.user-password.update`| A user's password was updated. A "-failure" flag is included in the message if the attempt to update a user's password failed. |
|`<service_name>.deployment-user.create`|`<service_id>.user.create` | A user was created. A "-failure" flag is included in the message if the attempt to create a user failed. |
|`<service_name>.deployment-user.delete`|`<service_id>.user.delete` | A user was deleted. A "-failure" flag is included in the message if the attempt to delete a user failed. |
|`<service_name>.deployment-group.update`|`<service_id>.resources.scale` | A scaling operation was performed. If the scaling operation failed, a "-failure" flag is included in the message. |
|`<service_name>.deployment-allowlist-ip-addresses.update` | `<service_id>.whitelisted-ips-list.update`|The allowlist was modified. A "-failure" flag is included in the message if the attempt to modify the allowlist failed. |
|`<service_name>.deployment.update`|`<service_id>.serviceendpoints.update` | A change was made to the service endpoints configuration. If the operation failed, a "-failure" flag is included in the message. |
|`<service_name>.deployment-group-autoscaling.update` | `<service_id>.autoscaling.update` | An autoscaling configuration change or an autoscaling operation was performed. If an autoscaling operation was performed the message includes `autoscale resources for instance <deployment-id>`. If the autoscaling operation or the configuration change failed, a "-failure" flag is included in the message. |
|`<service_name>.deployment-volumes.update`|`<service_id>.volumes.update` | An activity was performed on the encryption key that is used by the database, such as rotation or shredding. Details of the action are in the event. |
{: caption="List of events and event descriptions by {{site.data.keyword.databases-for}}" caption-side="bottom"}

The `service_name` field indicates the type of {{site.data.keyword.databases-for}} instance. For example, `databases-for-postgresql` or `messages-for-rabbitmq`.

Auditing of global events, such as `<service_name>.instance.create`, is covered by the {{site.data.keyword.cloud_notm}} global event. For more resource-related global events, see [Auditing events for service instances](/docs/atracker?topic=atracker-at_events_rc).
