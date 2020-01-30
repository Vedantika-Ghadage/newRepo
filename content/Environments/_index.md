+++
title = "Environments"
description = ""
weight=80
+++
An Environment is a logical grouping of applications to which you can
apply policies and common configuration. You can run an application in
several Environments. Typically environments are created for lifecycle
phases in you delivery pipeline (e.g. dev-test, staging, production).

You can create several environments on the same Kubernetes cluster, and
each environment is fully contained in a cluster.

![image](/images/concepts-environments.png)

#### Running Applications {#run-application}
{{%excerpt-include filename="Environments/Running_Applications/_index.md" /%}}

#### Access Controls
{{%excerpt-include filename="Environments/Access_Controls/_index.md" /%}}

#### Update Policy
{{%excerpt-include filename="Environments/Update_Policy/_index.md" /%}}

#### Managing Applications
{{%excerpt-include filename="Environments/Managing_Applications/_index.md" /%}}
