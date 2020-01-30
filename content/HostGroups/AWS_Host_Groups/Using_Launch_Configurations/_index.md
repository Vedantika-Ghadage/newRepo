+++
title = "Using Launch Configurations"
description = ""
weight=40
+++
{{%excerpt%}}
AWS Launch Configurations can be used with Nirmata in order to
provision/deprovision EC2 instances from Nirmata. Detailed information
on creating a Launch Configuration can be found here:

[AWS Documentation: Launch Configurations](http://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/WorkingWithLaunchConfig.html)

The Launch Configurations must use the AMI created earlier or you can
use a standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to install Docker and Nirmata agent.
{{%/excerpt%}}
