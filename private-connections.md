---

copyright:
  years: 2025
lastupdated: "2025-11-19"

keywords: postgresql, databases, gen 2, postgresql connection strings, postgresql connection ibm application

subcollection: cloud-databases-gen2

---

{{site.data.keyword.attribute-definition-list}}

# Setting up a private connection for Gen 2 {{site.data.keyword.databases-for}}
{: #setting-up-private-endpoints-gen2}

Gen 2 {{site.data.keyword.databases-for}} enable a secure by default approach using private connections enabled by Virtual Private Endpoints (VPE). {{site.data.keyword.cloud}} recommends 
private endpoints because they restrict access to your internal network, protecting your data and applications from unwanted access and security vulnerabilities.

Private endpoints also provide better control and visibility over network traffic to your databases and enable you to demonstrate adherence to compliance and regulatory requirements. 
Gen 2 {{site.data.keyword.databases-for}} support context-based restrictions, which allow account owners and administrators to define and enforce access restrictions for {
{site.data.keyword.cloud}} resources based on the context of access requests.

## Options to connect to your VPC instance via private endpoints
{: #options-private-endpoints}

You can access your instance from your local device or non-VPC client via private endpoints. Connect to VPE for VPC to provide a secure connectivity to services or instances originating 
from your VPC network. The instructions to connect to your Gen 2 (VPC) instance depend on where you connect from and where your application is running.

1. VPE via VSI (client-to-site) - This method uses a Virtual Server Instance (VSI) that resides in your Virtual Private Cloud (VPC) and leverages the Virtual Private Endpoint (VPE) to provide secure and private connectivity between resources within the VPC and 
external {{site.data.keyword.cloud}} services. For more information, see [client-to-site method](add link).
2. Use a VPN connection established through a VPE. The VPN lets you connect and manage from a local laptop or client via the VPC/VPE.
3. Use a VPC/VPN gateway for secure and private on-premises access to cloud resources. For more information, see [site-to-site method](add link).

## How to connect
{: #howto-privateendpoints}

### Create a Virtual Private Cloud (VPC)
{: #howto-private-endpoints}
{: step}

Follow [{site.data.keyword.cloud}} instructions](add link) to create a Virtual Private Cloud (VPC). Ensure that the VPC is in the same region as your database deployment.

### Create a VSI
{: #howto-private-endpoints}
{: step}

Provision a VSI within the VPC using [virtual server instances](/docs/vpc?topic=vpc-creating-virtual-servers&interface=ui). Assign a public IP to the VSI to allow external SSH access 
(optional for testing). Generate and attach an SSH key for secure login. For detailed instructions on how to create an SSH key, see 
[getting started with VPC](/docs/vpc?topic=vpc-ssh-keys&interface=ui).

Log in to your VSI and change the permissions of the key:

`$ chmod 400 <COPY_LOCAL_LOCATION_OF_THE_SSH_KEY>`

SSH into your VSI using the following command:

`$ ssh -i ~/.ss/<NAME_OF_THE_SSH_KEY> root@<FLOATING_IP_ADDRESS>`

### Create a VPE
{: #howto-privateendpoints}
{: step}

1. Follow [{site.data.keyword.cloud}} instructions](/docs/cloud-databases?topic=cloud-databases-hosting-model-transition&interface=ui) to create a VPE for your database service.
2. Bind the VPE to your VPC and subnet.

### Update VPC security groups
{: #howto-privateendpoints}
{: step}

1. Modify the security group to allow outbound traffic from your VSI to the database instance. 
1. Ensure ports required by your database (for example, PostgreSQL, MongoDB) are open.

### Bind Database Deployment to VSI
{: #howto-privateendpoints}
{: step}

Use {site.data.keyword.cloud}} CLI or UI to bind your database deployment to your VSI. This stores the connection strings in a secret.

### Configure Application
{: #howto-privateendpoints}
{: step}

1. Retrieve the connection string from the secret.
2. Update your application configuration to use the private endpoint connection string. This stores the connection strings in a secret.

### Install Client Tools on VSI
{: #howto-privateendpoints}
{: step}

1. Use {site.data.keyword.cloud}} CLI or UI to bind your database deployment to your VSI. This stores the connection strings in a secret. 
1. SSH into your VSI. 

### Connect to your Database with private endpoints. 
{: #howto-privateendpoints}
{: step}

Install the required client. Connect to the VSI from a local environment by sending a root certificate from a local machine to a VSI. This command will vary depending on the database 
service and the client. The instructions required per database arelisted in the following table. 

| Service | Client tool | Sample command                                                                 |
|-----------------------------|------------------|-------------------------------------------------------------------------------------|
| {{site.data.keyword.databases-for-postgresql}}    | `psql`           | You can connect to the VSI from a local environment by sending the root certificate from a local machine 
to a VSI.`$  PGPASSWORD=$PASSWORD psql “<PASSWORD>` You can verify your connection with the following command (optional):`$ /list`       |
| {{site.data.keyword.databases-for-mongodb}}       | --          | --      |
{: caption="Client tools and example connection commands for private access" caption-side="bottom"}
