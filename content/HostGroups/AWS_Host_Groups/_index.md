+++
title = "AWS Host Groups"
description = ""
weight=30
+++
{{%excerpt%}}
To create an AWS Host Group, you must first setup an
[AWS Cloud Provider](/cloudproviders/#aws-provider).

Nirmata directly integrates with Amazon Web Services (AWS) and offers
several ways to provision and manage AWS hosts. For each AWS Host Group
you can use any of the following options to launch AWS cloud instances:

1. [Using Amazon Machine Images (AMIs)](#create-AMI).
2. [Using Auto Scaling Groups (ASGs)](#create-ASG).
3. [Using Spot Fleet Requests](#create-spot-fleet).
4. [Using Launch Configurations](#create-launch-config).

##### Using Amazon Machine Images (AMIs) {#create-AMI}

You can create your own AMI with Docker running on it. The AMI has the following requirements:

1.  Can be any Linux flavor that can run Docker
2.  Requires Docker 1.10+ ([download](https://www.docker.io/gettingstarted/))

You will need to setup the Nirmata agent container on that instance by
running the command:

    sudo curl -sSL https://www.nirmata.io/nirmata-host-agent/setup-nirmata-agent.sh | sudo sh -s -- --cloud aws

Once the instance is setup, create an AMI via the AWS console. This AMI
can be used with your Auto Scaling Group or Spot Fleet instances.


##### Using Auto Scaling Groups (ASGs) {#create-ASG}

Detailed information on creating and managing Auto Scaling groups can be
found here:

[AWS Documentation: Auto Scaling Groups](http://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/WorkingWithASG.html)

The Launch Configuration of the ASG must use the AMI created earlier or
you can use a standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to install Docker and Nirmata agent.

This will ensure that Docker and Nirmata Host Agent are pre installed.

![image](/images/aws-launch-config.png)

##### Using Spot Fleet Requests {#create-spot-fleet}

You can use AWS Spot Fleet Requests with Nirmata to take advantage of
discounted spot instance pricing. To use Spot Fleet Requests, you need
to first create the Spot Fleet Requests using AWS console. Detailed
information on creating and managing Spot Fleet Requests can be found
here:

[AWS Documentation: Spot FleetRequests](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet-requests.html)

The Spot Fleet Request can use the AMI created earlier or you can use a
standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to
install Docker and Nirmata agent.

##### Using Launch Configurations {#create-launch-config}

AWS Launch Configurations can be used with Nirmata in order to
provision/deprovision EC2 instances from Nirmata. Detailed information
on creating a Launch Configuration can be found here:

[AWS Documentation: Launch Configurations](http://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/WorkingWithLaunchConfig.html)

The Launch Configurations must use the AMI created earlier or you can
use a standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to install Docker and Nirmata agent.

##### Creating an AWS Host Group

To create an AWS Host Group, you must first setup a
[AWS Provider](/cloudproviders/#aws-provider).

Create a Host Group by specifying the Host Group Name and selecting the
Cloud Provider. Then you need to select the host instance type (AMI,
ASG, Spot Fleet Request or Launch Configuration).

![image](/images/create-aws-host-group-1.png)

![image](/images/create-aws-host-group-2.png)

##### Troubleshooting AWS Host Creation {#troubleshoot-aws-host-creation}

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
