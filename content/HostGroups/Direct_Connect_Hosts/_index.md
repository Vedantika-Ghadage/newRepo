+++
title = "Direct Connect Hosts"
description = ""
weight=20
+++
{{%excerpt%}}
You can connect any (public or private cloud) server into Nirmata using
the 'Direct Connect' cloud provider type. In this type of deployment
you control which servers are made available in a Host Group. Auto
scaling and recovery of hosts is not supported for this host type.

A container engine is required on your host. To install the Docker
engine see the [Docker installation guide](https://docs.docker.com/installation/).

To setup a Create a Host Group of type 'Direct Connect' by navigating
to Host Groups -> Direct Connect -> Add Host Group. Give your Host
Group a name and drill down into its details page. This will display an
message as follows:

    Install the Nirmata Host Agent using the key: <key>

To complete the setup, install Docker Engine and launch the Nirmata Host
Agent passing in the provider type and Host Group ID:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud other --hostgroup <key>

If your server is a Virtual Machine, you can also save it as a template
or image to create additional Nirmata Host instances from it.

**Note:** Remove the file: */usr/share/nirmata/conf/host\_agent.id* and
the directory: */opt/nirmata/db/* prior to saving the VM as a template.

{{%/excerpt%}}
