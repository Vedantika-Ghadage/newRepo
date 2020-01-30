+++
title = "OpenStack Cloud Provider"
description = ""
weight=80
+++
{{%excerpt%}}

To securely connect Nirmata to OpenStack in your Private Cloud or Data
Center, first setup a [`private-cloud-setup`](/cloudproviders/#private-cloud-setup).

Next, add OpenStack Cloud to Nirmata by providing the OpenStack Keystone Identity Service URL, Project Name, and Credentials.

To add the OpenStack Cloud to Nirmata, select Cloud Providers from the sidebar menu. Select *+Add Cloud Provider*.

![image](/images/gcecloud-3.png)

Enter the *Cloud Provider* information. Select *Oracle Public Cloud Services* as the *Type.* Click *Next.*

![image](/images/openstack-1.png)

On the *Settings* tab, enter the Endpoint URL, Tenant ID/Project ID, Username, and Password. Click *Next.*

![image](/images/openstack-2.png)

Nirmata automatically validates account access.
Once account access is validated, setup an [OpenStack Cloud Provider Host Group](https://docs.nirmata.io/hostgroups/openstack_host_groups/).


**Next Steps**: Setup a [`openstack-host-group`](/hostgroups/#openstack-host-group).
{{%/excerpt%}}
