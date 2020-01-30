+++
title = "Oracle Cloud Provider"
description = ""
weight=50
+++
{{%excerpt%}}


To add Oracle Public Cloud to Nirmata, enter the  identity domain name, endpoint URL, and username and password associated with the Oracle Public Cloud account.

#### How to Find the Oracle Public Cloud Identity Domain Name and Endpoint URL

Sign in to the Oracle Public Cloud account. Navigate to *Service Listing* and click on the service name.

Select *Identity Domain Administration.* Note the *Identity Domain Name.*

Locate and note the [endpoint URL](https://docs.cloud.oracle.com/iaas/Content/API/Concepts/apiref.htm) for the account.

#### Add Oracle Public Cloud to Nirmata

To add the Oracle Public Cloud to Nirmata, select Cloud Providers from the sidebar menu. Select *+Add Cloud Provider*.

![image](/images/gcecloud-3.png)

Enter the *Cloud Provider* information. Select *Oracle Public Cloud Services* as the *Type.* Click *Next.*

![image](/images/oraclecloud-1.png)

On the *Settings* tab, enter the Endpoint URL, Identity Domain, and Username and Password. Click *Next.*

![image](/images/oraclecloud-2.png)

Nirmata automatically validates account access.
Once account access is validated, setup an [Oracle Public Cloud Host Group](https://docs.nirmata.io/hostgroups/oracle_public_cloud_host_group/).

**Next Steps**: Setup a [`opc-host-group`](/hostgroups/#opc-host-group)
Host Group.

{{%/excerpt%}}
