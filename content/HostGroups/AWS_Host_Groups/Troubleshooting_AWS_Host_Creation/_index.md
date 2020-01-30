+++
title = "Troubleshooting AWS Host Creation"
description = ""
weight=70
+++
{{%excerpt%}}
In some cases, host creation on AWS may fail due to various reasons.
Here are a few things to check when the host creation fails:

1.  Check if Docker Engine and Nirmata agent were successfully installed
    and started on the instances provisioned on AWS. To check if Nirmata
    agent is running, ssh to your AWS instance and use command: sudo
    docker ps. This command will list all the running containers. Verify
    that the nirmata-agent container is running
2.  If Nirmata agent is running on your AWS instance but the state
    displaying on the Nirmata console is 'Pending Connect' or 'Not
    Connected', the Nirmata agent might be unable to connect back to
    Nirmata server. Verify that AWS security groups for your instance
    allow outbound HTTPS traffic. You can check be accessing a website
    e.g. www.google.com using curl or wget (e.g. `curl -XGET
    http://www.google.com`)
3.  When creating AWS instances using Launch Configuration mode, ensure
    that the network selected in Nirmata is the same as the network of
    security group configured for the launch configuration. If this is
    not the case, instance creation will fail.
{{%/excerpt%}}
