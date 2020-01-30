+++
title = "Using Auto Scaling Groups (ASGs)"
description = ""
weight=20
+++
{{%excerpt%}}
Detailed information on creating and managing Auto Scaling groups can be
found here:

[AWS Documentation: Auto Scaling Groups](http://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/WorkingWithASG.html)

The Launch Configuration of the ASG must use the AMI created earlier or
you can use a standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to install Docker and Nirmata agent.

This will ensure that Docker and Nirmata Host Agent are pre installed.

![image](/images/aws-launch-config.png)

{{%/excerpt%}}
