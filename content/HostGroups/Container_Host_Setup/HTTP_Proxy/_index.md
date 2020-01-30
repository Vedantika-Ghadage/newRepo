+++
title = "HTTP Proxy"
description = ""
weight=50
+++
{{%excerpt%}}
The Nirmata agent can use a HTTP proxy to communicate to the
internet. To set this up, complete the following:  

> **Note:** Install this agent only during the initial deployment of the Nirmat host group.

> Upstart:
>
>     Add the following to the docker run command in /etc/init/nirmata-agent.conf file:
>         -e HTTPS_PROXY=<http(s) proxy address and port>
>
>     e.g. -e HTTPS_PROXY=https://192.162.11.11:443
>
> Systemd:
>
>     Add the following to the docker run command in /opt/nirmata/bin/start-nirmata-agent.sh file:
>         -e HTTPS_PROXY=<http(s) proxy address and port>
>
>     e.g. -e HTTPS_PROXY=https://192.162.11.11:443

Restart Nirmata agent using the appropriate command.

To deploy the cluster, create a [Cluster Policy](https://docs.nirmata.io/clusters/cluster_policies/).
{{%/excerpt%}}
