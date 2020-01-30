+++
title = "Using Amazon Machine Images (AMIs)"
description = ""
weight=10
+++
{{%excerpt%}}
You can create your own AMI with Docker running on it. The AMI has the following requirements:

1.  Can be any Linux flavor that can run Docker
2.  Requires Docker 1.10+ ([download](https://www.docker.io/gettingstarted/))

You will need to setup the Nirmata agent container on that instance by
running the command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud aws

Once the instance is setup, create an AMI via the AWS console. This AMI
can be used with your Auto Scaling Group or Spot Fleet instances.
{{%/excerpt%}}
