+++
title = "Using Cloud-init"
description = ""
weight=10
+++
{{%excerpt%}}
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

{{%/excerpt%}}
