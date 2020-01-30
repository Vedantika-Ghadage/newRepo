+++
title = "AWS Cloud Provider"
description = ""
weight=20
+++
{{%excerpt%}}

Nirmata requires read-only access to EC2 service if using ASGs or Spot
Fleet Requests and full access to EC2 service if using Launch
Configuration to provision your VMs. If using Nirmata Cloud Edition, the secure way to provide access is by configuring an IAM role for Nirmata in your AWS account. To configure
a role, you will need the Nirmata AWS account ID and an unique external
ID. When the role is configured, you provide Nirmata the role ARN
(Amazon Resource Name).

For Nirmata Private Edition, you need to create a new user with necessary policy access, and then use the user access credentials (access key ID and secret access key) for cloud provider integration authenticaion.

This process may seem involved, but only takes a few minutes to set up!
Here are the detailed steps:

{{%excerpt%}}
