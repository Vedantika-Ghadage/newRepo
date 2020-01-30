+++
title = "Create a vSphere Template"
description = ""
weight=20
+++
{{%excerpt%}}
Create and launch a Linux VM using vSphere. Connect to the VM and setup
Nirmata agent by running the following command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud vsphere

Now you can create a template for the VM using vCenter. This template
should be selected when creating a host group for your vSphere provider.
{{%/excerpt%}}
