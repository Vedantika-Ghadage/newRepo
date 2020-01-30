+++
title = "Using Spot Fleet Requests"
description = ""
weight=30
+++
{{%excerpt%}}
You can use AWS Spot Fleet Requests with Nirmata to take advantage of
discounted spot instance pricing. To use Spot Fleet Requests, you need
to first create the Spot Fleet Requests using AWS console. Detailed
information on creating and managing Spot Fleet Requests can be found
here:

[AWS Documentation: Spot FleetRequests](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet-requests.html)

The Spot Fleet Request can use the AMI created earlier or you can use a
standard Linux AMI and use [cloud-init](/hostgroups/#nirmata-agent-setup) to
install Docker and Nirmata agent.
{{%/excerpt%}}
