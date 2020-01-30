+++
title = "Digital Ocean Host Group"
description = ""
weight=70
+++
{{%excerpt%}}
To create a Digital Ocean Host Group, you must first setup a
[Digital Ocean Cloud Provider](/cloudproviders/#digital-ocean-provider).

Nirmata integrates with Digital Ocean APIs to automate container host
provisioning. To enable this automation, you must first create a VM
template.

Launch a Linux droplet in Digital Ocean. Then, connect to the VM and
setup Nirmata agent by running the following command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud digitalocean

Now, power down the droplet and create an image snapshot from the Images
page. This image should be selected when creating a host group for your
Digital Ocean provider

![image](/images/create-digital-ocean-image.png)

Next, create a Host Group by selecting the Digital Ocean cloud provider,
specifying the number of desired hosts, region and selecting the VM
image created earlier. Select the droplet size.

![image](/images/create-digital-ocean-host-group-1.png)

![image](/images/create-digital-ocean-host-group-2.png)

Once this is done, Nirmata will create and setup droplets (VMs). Once
the VMs are powered on, they will connect to Nirmata SaaS. Now you can
create applications and deploy them to your Digital Ocean resources.

{{%/excerpt%}}
