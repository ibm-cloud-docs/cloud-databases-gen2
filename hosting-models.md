---

copyright:
  years: 2025
lastupdated: "2025-09-23"

subcollection: cloud-databases-gen2

keywords: isolated compute, host size, vcpu, ram

---

{{site.data.keyword.attribute-definition-list}}

# Gen 2 isolated compute
{: #isolated-compute}

{{site.data.keyword.databases-for}} (on Gen 2 platform) offers an isolated compute hosting model designed for enterprise-grade workloads that demand high performance, security, and dedicated resources.
{: shortdesc}

The isolated compute hosting model provisions your database on a single-tenant virtual machine, providing hypervisor-level isolation and dedicated storage bandwidth. This model is ideal for workloads that demand consistent performance, security, and compliance.

All user-data management agents are also isolated, ensuring that your resources are not shared with other tenants.

## Resource management
{: #isolated-compute-resource-mgmt}

In the isolated compute model, CPU and RAM resources are fixed at the time of provisioning. You can manually scale your deployment using the IBM Cloud UI, CLI, API, or Terraform. Disk autoscaling will be supported soon, while CPU and RAM autoscaling are unavailable.

[{{site.data.keyword.monitoringfull}}](/docs/cloud-databases-gen2?topic=cloud-databases-monitoring) can be integrated to help you track memory, disk space, and disk I/O utilization.

## Capacity
{: #isolated-compute-capacity}

Isolated compute fully isolates your database, including database management containers. These management containers take up some overhead in your isolated compute instance, consuming a portion of the machine's CPU and RAM, with the remainder available for your database to use.

## Sizing
{: #isolated-compute-sizing}

You can choose from a range of host sizes to match your workload requirements. Each size defines a specific CPU and RAM configuration. This machine will be exclusively assigned to running your database instance. Storage is selected separately, allowing you to customize disk and IOPS size.

Scale your database and change your machine size using your preferred method: the [Cloud Databases CLI plug-in](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference), the [Cloud Databases API](new link), or using [Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/database).

## Size selections in the UI
{: #isolated-compute-sizing-ui}
{: ui}

Isolated compute features 6 size selections with [Flex profiles]() in the UI.

| Host size | vCPU x RAM | Regional availability |
| --- | --- | --- |
| 4x16 | 4 vCPU x 16 GB RAM | |
| 8x32 | 8 vCPU x 32 GB RAM | |
| 8x64 | 8 vCPU x 64 GB RAM | |
| 16x64 | 16 vCPU x 64 GB RAM | |
| 32x128 | 32 vCPU x 128 GB RAM | |
| 30x240 | 30 vCPU x 240 GB RAM | |
{: caption="Isolated compute UI selections" caption-side="bottom"}

Isolated compute features the following selections with Intel 8474C processor.

These selections are only available in selected regions. For more information, see [VPC compute profiles](/docs/vpc?topic=vpc-profiles&interface=ui#vhmemory).
{: note}

| Host size | vCPU x RAM | Regional availability |
| --- | --- | --- |
| 4x20 | 4 vCPU x 20 GB RAM | |
| 8x40 | 8 vCPU x 40 GB RAM | |
| 8x80 | 8 vCPU x 80 GB RAM | |
| 16x80 | 16 vCPU x 80 GB RAM | |
| 32x160 | 32 vCPU x 160 GB RAM | |
| 48x240 | 48 vCPU x 240 GB RAM | |
{: caption="Isolated compute UI selections for Intel 8474C processor" caption-side="bottom"}


## Size selections in the CLI
{: #isolated-compute-sizing-cli}
{: cli}

Isolated compute features 6 size selections:

The host_flavor parameter defines your Compute sizing. Input the appropriate value for your desired size.

| Host size | vCPU x RAM           | host_flavor value         | Regional availability  |
|-----------|----------------------|---------------------------|------------------------|
| 4x16      | 4 vCPU x 16 GB RAM   | b3c.4x16.encrypted        |                        |
| 8x32      | 8 vCPU x 32 GB RAM   | b3c.8x32.encrypted        |                        |
| 8x64      | 8 vCPU x 64 GB RAM   | m3c.8x64.encrypted        |                        |
| 16x64     | 16 vCPU x 64 GB RAM  | b3c.16x64.encrypted       |                        |
| 32x128    | 32 vCPU x 128 GB RAM | b3c.32x128.encrypted      |                        |
| 30x240    | 30 vCPU x 240 GB RAM | m3c.30x240.encrypted      |                        |
{: caption="Isolated compute CLI selections" caption-side="bottom"}

Isolated compute features the following selections with Intel 8474C processor.

These selections are only available in selected regions. For more information, see [VPC compute profiles](/docs/vpc?topic=vpc-profiles&interface=ui#vhmemory).
{: note}

| Host size | vCPUxRAM           | host_flavor value | Regional availability    (Check the [regional availability of confidential computing profiles for machine sizes](/docs/vpc?topic=vpc-profiles&interface=ui#confidential-computing-profiles) in this table.)                                   |
|-----------|----------------------|-------------------|----------------------------------------------------------------------------------------|
| 4x20      | 4 vCPU x 20 GB RAM   | ?                 | Dallas (us-south) \\n Washington DC (us-east) \\n Frankfurt (eu-de)                    |
| 8x40      | 8 CPU x 40 GB RAM    | ?                 |                                                                                        |
| 8x80      | 8 CPU x 80 GB RAM    | ?                 |                                                                                        |
| 16x80     | 16 CPU x 80 GB RAM   | ?                 |                                                                                        |
| 32x160    | 32 CPU x 160 GB RAM  | ?                 |                                                                                        |
| 48x240    | 48 CPU x 240 GB RAM  | ?                 |                                                                                        |
{: caption="Isolated compute Terraform selections for Intel 8474C processor" caption-side="bottom"}

## Size selections in Terraform
{: #isolated-compute-sizing-tf}
{: terraform}

Isolated compute features 6 size selections:

The host_flavor parameter defines your Compute sizing. Input the appropriate value for your desired size.

| Host size | vCPU x RAM             | host_flavor value         |
|-----------|----------------------|----------------------------|
| 4x16      | 4 vCPU x 16 GB RAM   | b3c.4x16.encrypted         |
| 8x32      | 8 vCPU x 32 GB RAM   | b3c.8x32.encrypted         |
| 8x64      | 8 vCPU x 64 GB RAM   | m3c.8x64.encrypted         |
| 16x64     | 16 vCPU x 64 GB RAM  | b3c.16x64.encrypted        |
| 32x128    | 32 vCPU x 128 GB RAM | b3c.32x128.encrypted       |
| 30x240    | 30 vCPU x 240 GB RAM | m3c.30x240.encrypted       |
