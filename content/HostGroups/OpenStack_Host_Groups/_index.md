+++
title = "OpenStack Host Groups"
description = ""
weight=90
+++
{{%excerpt%}}
To create a OpenStack Host Group, you must first setup a
[OpenStack Cloud Provider](/cloudproviders/#openstack-provider).

To securely connect Nirmata to OpenStack in your Private Cloud or Data
Center, first setup a [Private Cloud](/cloudproviders/#private-cloud-setup).

Setting up OpenStack consists of the following steps:

1.  [Create a VM template](#create-OpenStack-Template).
2.  [Create an OpenStack Host Group](#create-OpenStack-HostGroup).

##### Create a VM Template {#create-OpenStack-Template}

Create and launch a Linux VM using OpenStack. Connect to the VM and
setup Nirmata agent by running the following command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud openstack

Now you can create a template for the VM using OpenStack Horizon. This
template should be selected when creating a host group for your
OpenStack provider.

##### Create OpenStack Host Group {#create-OpenStack-HostGroup}

Create a host group by selecting the OpenStack provider, specifying the
number of desired hosts and selecting the template created earlier.
Provide the resource information such as flavor, keypair, network and
security group.

![image](/images/create-openstack-hg-0.png)

![image](/images/create-vsphere-hg-1.png)

Once this is done, Nirmata will create and setup VMs. Once the VMs
start, they will connect to Nirmata SaaS. Now you can create
applications and deploy them to your OpenStack resources.
{{%/excerpt%}}
