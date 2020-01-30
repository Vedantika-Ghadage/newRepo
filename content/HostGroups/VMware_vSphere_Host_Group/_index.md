+++
title = "VMware vSphere Host Group"
description = ""
weight=80
+++
{{%excerpt%}}
To create a vSphere Host Group, you must first setup a
[VMware vSphere Cloud Provider](/cloudproviders/#vsphere-provider).

To securely connect Nirmata to a vSphere in your Private Cloud or Data
Center, first setup a [Private Cloud](/cloudproviders/#private-cloud-setup).

Setting up VMware consists of the following steps:

 1.  [Setup Resource Pool in vCenter](#setup-VMware-ResourcePool).
 2.  [Create a vSphere template](#setup-VMware-Template).
 3.  [Create a VMware vSphere Host Group](#setup-VMware-HostGroup).

##### Setup a Resource Pool in vCenter {#setup-VMware-ResourcePool}

Refer to VMWare vSphere
[documentation](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.resourcemanagement.doc_40/managing_resource_pools/t_create_resource_pools.html)
for instructions on setting up a Resource Pool.

##### Create a vSphere Template {#setup-VMware-Template}

Create and launch a Linux VM using vSphere. Connect to the VM and setup
Nirmata agent by running the following command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud vsphere

Now you can create a template for the VM using vCenter. This template
should be selected when creating a host group for your vSphere provider.

##### Create a VMware vSphere Cloud Provider {#setup-VMware-CloudProvider}

Create a VMWare vSphere provider by providing the vCenter SDK URL
(<http://serveraddress/sdk>) and credentials:

![image](/images/create-vsphere-provider-1.png)

After entering the credentials, validate access to your cloud provider
before closing the wizard:

![image](/images/create-vsphere-provider-2.png)

##### Create a VMware vSphere Host Group {#setup-VMware-HostGroup}

Next, you can create a host group by selecting the vSphere provider,
specifying the number of desired hosts, providing the data center
information and selecting the resource pool, image template, flavor,
network and datastore.

![image](/images/create-vsphere-hg-0.png)

![image](/images/create-vsphere-hg-1.png)

Once this is done, Nirmata will create and setup VMs. Once the VMs are
powered on, they will connect to Nirmata SaaS. Now you can create
applications and deploy them to your VMWare vSphere resources.

{{%/excerpt%}}
