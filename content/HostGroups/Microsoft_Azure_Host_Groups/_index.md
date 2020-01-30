+++
title = "Microsoft Azure Host Groups"
description = ""
weight=40
+++
{{%excerpt%}}
To create a Azure Host Group, you must first setup a
[Microsoft Azure Cloud Provider](/cloudproviders/#azure-provider).

Nirmata integrates with Azure Resource Manager. Prior to creating a Host
Group in Nirmata, you need to create a Resource Group in Azure. Within
your resource group, you should also create the following items:

 1.  Virtual Network
 2.  Network Security Group
 3.  Route table
 4.  Storage Account

Create a host group by selecting the Azure provider, specifying the
number of desired hosts and selecting the resource group. Select the
image, instance type, virtual network, security group and the storage
account. You can also select if you want to attach public IP addresses.
Enter the username and password to access your instance.

You need to install Docker Engine and Nirmata agent using cloud-init by
adding the installation script in User Data. Clicking on 'Install
Nirmata Agent' will add the following script to User Data:

    #!/bin/bash -x
    # Install Docker
    wget -qO- https://get.docker.com/ | sh

    # Install Nirmata Agent
    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud azure

Once this is done, Nirmata will create and setup VMs. Once the VMs are
powered on, they will connect to Nirmata SaaS. Now you can create
applications and deploy them to your Azure resources.
{{%/excerpt%}}
