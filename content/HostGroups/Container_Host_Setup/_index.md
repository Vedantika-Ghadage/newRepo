+++
title = "Container Setup"
description = ""
weight=10
+++
{{%excerpt%}}
Here are the general requirements for a Container Host that is managed
by Nirmata.

 1.  Can be any Linux flavor that can run Docker.
 2.  Requires Docker 1.10+ (see <https://docs.docker.com/install/>)
 3.  The Nirmata agent must be installed (see [Using Cloud Init](/hostgroups/#nirmata-agent-setup))

##### Using cloud-init {#nirmata-agent-setup}

If your OS provisioning system supports cloud-init, cloud-config, or
similar initialization and provisioning mechanisms, you can easily
install Docker and the Nirmata Agent as follows (assumes use of Direct
Connect / Other Host Groups):

> **Ubuntu:**
>
> ``` {.sourceCode .bash}
> #!/bin/bash -x
> # Install Docker
> wget -qO- https://get.docker.com/ | sh
>
> # Install Nirmata Agent
> sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud other --hostgroup <key>
> ```
>
> **CentOS:**
>
> ``` {.sourceCode .bash}
> #!/bin/bash -x
> # Install Docker
> sudo yum update -y
>
> sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
> [dockerrepo]
> name=Docker Repository
> baseurl=https://yum.dockerproject.org/repo/main/centos/7/
> enabled=1
> gpgcheck=1
> gpgkey=https://yum.dockerproject.org/gpg
> EOF
>
> sudo yum install -y docker-engine
> sudo systemctl enable docker.service
> sudo systemctl start docker
>
> # Install Nirmata Agent
> sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud other --hostgroup <key>
> ```
>
> **Amazon Linux:**
>
> ``` {.sourceCode .bash}
> #!/bin/bash -x
> # Install docker
> sudo yum update -y
> sudo yum install -y docker
> sudo service docker start  
>
> # Install Nirmata Agent
> sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud other --hostgroup <key>
> ```

##### Nirmata Agent Setup

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

**Note:** Setup-nirmata-agent.sh uses [upstart](http://upstart.ubuntu.com/)/[systemd](http://wiki.debian.org/systemd) to enable management of nirmata-agent as a service. If upstart or systemd is not available on your host instance, you can directly run nirmata-agent container using docker.


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

##### Host Labels

You can setup host labels when installing the Nirmata agent. Nirmata
agent can detect host labels directly from Docker Engine. Host labels
can also be passed in to Nirmata agent using environment variables.

> Docker Engine:
>
>     Add the label option when start Docker Engine. Depending on your docker-engine installation, you can add the label option to DOCKER_OPTS
>        e.g. --label environment-type="production"
>
> Environment variable:
>
>     You can add the labels to Nirmata agent as environment variables. For this, you can modify the Nirmata agent init script (/etc/init/nirmata-agent.conf) and update the HOST_LABELS field. The labels should be specified in json format without any whitespaces.
>
> > e.g.
> > HOST_LABELS={"host-type":"SSD","host-location":"us-east"}

Once you setup the host labels, you will need to restart the Nirmata
agent. The host labels should be detected and display in Nirmata console
once the host connects. Now, you can use these labels to control the
placement of your containers.

##### HTTP Proxy

You can setup Nirmata agent to use a HTTP proxy to communicate to the
internet. Here are the instructions.

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

##### Host Networking

Nirmata does nor require any special networking setup, and works with
your existing Host networking. Nirmata uses the Docker bridge network
mode on each Host, so each application service is addressable using the
Host IP address and an allocated (static or dynamic) port. Based on the
cloud provider, Nirmata will detect the public and private IP addresses
of your Host. When available, the Host's private IP address will be
used for communication between services.

{{%/excerpt%}}
