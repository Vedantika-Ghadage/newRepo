+++
title = "Nirmata Agent Setup"
description = ""
weight=20
+++
{{%excerpt%}}
To setup the Nirmata agent on the host instance

> 1.  Run the Nirmata Agent configuration script:
>
>         sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud <CloudProvider> --hostgroup <HostGroupId>
>
>         where:
>           CloudProvider = [aws | azure | oraclecs | openstack | vsphere | google | digitalocean | other]
>           HostGroupId = unique ID for the Host Group. Only required for the 'Direct Connect' container hosts
>
> 2.  Verify that Nirmata Agent has started:
>
>         sudo docker ps

{{% notice note %}} Setup-nirmata-agent.sh uses / to enable management of nirmata-agent as a service. If upstart or systemd is not available on your host instance, you can directly run nirmata-agent container using docker.
{{% /notice %}}
To start/stop Nirmata agent you can use:

> Upstart:
>
>     sudo start nirmata-agent
>     sudo stop nirmata-agent
>
> Systemd:
>
>     systemctl start nirmata-agent
>     systemctl stop nirmata-agent

To setup the Nirmata agent on any host instance using commandline (for
'other' cloud provider):

    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v /var/log/nirmata-agent:/var/log/supervisor \
                -v /opt/nirmata/conf:/usr/share/nirmata/conf -v /opt/nirmata/db:/usr/share/nirmata/db --name=nirmata-agent \
                -v /sys:/sys:ro -e NIRMATA_HOST_ADDRESS=<HostName> -e NIRMATA_CLOUD_PROVIDER_TYPE=other -e NIRMATA_USE_HTTP=false\
                -e NIRMATA_HOST_GATEWAY=www.nirmata.io/host-gateway/manager -e NIRMATA_LABELS=<HostLabels> -e NIRMATA_HOST_GROUP_ID=<HostGroupId> nirmata/nirmata-agent:latest

    where:
      HostName = Host name or IP address of your host
      HostGroupId = unique ID for the Host Group. Required for the 'other' cloud provider type
      HostLabels = Host labels in json format without any spaces between keys and values. e.g. NIRMATA_LABELS={"host-type":"SSD","host-location":"us-east"}
{{%/excerpt%}}
