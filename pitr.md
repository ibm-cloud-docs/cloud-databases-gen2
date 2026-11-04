---

copyright:
  years: 2019, 2026
lastupdated: "2026-11-04"

subcollection: cloud-databases

keywords: point-in-time recovery, PITR, backups, restore, recovery

---

{{site.data.keyword.attribute-definition-list}}

# Point-in-time recovery
{: #point-in-time-recovery}

Point-in-time recovery (PITR) lets you restore a deployment to an available recovery point within the recovery period. PITR uses continuous incremental backups and transaction logs to recover data to a selected point in time.

PITR is enabled automatically for supported deployments and remains active regardless of the automatic backup setting.

When you perform a PITR restore, a new deployment is created. The restore process begins after the new deployment is provisioned. The restored deployment is billed as a separate deployment.

## Recovery points
{: #pitr-recovery-points}

PITR maintains continuous incremental backups for the previous 7 days.

You can restore your deployment to:

- The latest available recovery point.
- A specific recovery point within the recovery period.

Recovery points are available only within the supported recovery period.

## Restore options
{: #pitr-restore-options}

When you restore a deployment, select one of the following options.

### Restore to the latest available recovery point
{: #pitr-latest-recovery-point}

Restores the deployment to the most recent recovery point that is available when the restore request is submitted.

Use this option to recover the latest available data.

### Restore to a specific recovery point
{: #pitr-specific-recovery-point}

Restores the deployment to a selected date and time within the recovery period.

Specify the recovery point by using an ISO 8601 UTC timestamp, for example:

```text
2026-11-04T09:30:00Z
```
{: codeblock}

The user interface displays recovery times in your local time zone.

If the selected time is not available, choose an earlier recovery point or restore to the latest available recovery point.

## How PITR works
{: #how-pitr-works}

When a PITR restore is initiated:

1. A new deployment is provisioned.
2. The most appropriate backup is restored to the new deployment.
3. Transaction logs are replayed until the selected recovery point is reached.
4. The restored deployment becomes available.
5. The source deployment is not modified during the restore process.

## Considerations
{: #pitr-considerations}

- Restoring from PITR always creates a new deployment.
- The restored deployment is billed separately from the source deployment.
- Restore duration depends on deployment size, backup size, and the amount of transaction data that must be replayed.
- The source deployment remains available during the restore process.
- Do not delete the source deployment until you verify that the restored deployment is functioning as expected.

## Related information
{: #pitr-related-information}

For service-specific recovery procedures, limitations, and restore methods, see the documentation for your database service.
