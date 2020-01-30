+++
title = "Policies"
description = ""
weight=90
+++

Nirmata offers a rich set of policies that can be used to decouple
environment specific information from application definition. This
allows your application to be more portable across clusters and across
cloud providers.

Here is a summary of the available policies. Each one of these is
described in more detail in the sections below.

  Policy | Description
  -------|----------
  Config Maps |Used to provide environment specific configuration for your applications
  Secrets | Used to provide environment specific secrets for your applications
  Patch Policies | Used to override properties in the application configuration based on the environment
  Cluster Policies | Used to create new Kubernetes Clusters

#### Config Maps {#config-maps-policy}
{{%excerpt-include filename="Policies/Config_Maps/_index.md" /%}}

#### Secrets {#secrets-policy}
{{%excerpt-include filename="Policies/Secrets/_index.md" /%}}

#### Patch Policy
{{%excerpt-include filename="Policies/Patch_Policy/_index.md" /%}}

#### Cluster Policies
A cluster policy is used to define the configuration of your cluster.
For details on how to create and manage cluster policies, see
[Cluster Policies](/policies/cluster_policies/).

