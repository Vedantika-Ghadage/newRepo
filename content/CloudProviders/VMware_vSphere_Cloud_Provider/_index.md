+++
title = "VMware vSphere Cloud Provider"
description = ""
weight=70
+++
{{%excerpt%}}

To securely connect Nirmata to OpenStack in your Private Cloud or Data Center, setup a [`private-cloud-setup`](/cloudproviders/#private-cloud-setup).

Then, provide the vCenter SDK URL (`http://<server-address>/sdk`) and credentials.

In Nirmata, select Cloud Providers from the sidebar menu. Select *+Add Cloud Provider*.

![image](/images/gcecloud-3.png)

Enter the *Cloud Provider* information. Select *VMware vSphere* as the *Type* and select a *Private Cloud.* Click *Next.*

![image](/images/vspherecloud-1.png)

On the *Settings* tab, enter the Endpoint URL and Username and Password. Click *Next.*

![image](/images/vspherecloud-2.png)

Nirmata automatically validates account access.
Once account access is validated, setup a [VMWare vSphere Host Group](https://docs.nirmata.io/hostgroups/vmware_vsphere_host_group/).

**Next Steps**: Setup a [`vsphere-host-group`](/hostgroups/#vsphere-host-group).
{{%/excerpt%}}
