+++
title = "Applications"
description = ""
weight=60
+++

An Application is composed of one or more Components, where each
Component maps to a construct in the Kubernetes Workloads API. In most
cases an Application contains Kubernetes controllers like Deployments
and StatefulSets, exposed as Services. The number of components will
depend on your application architecture. For example some 3-tier
applications may have a few components, or even a single component,
where as Microservices style applications may have hundreds of services.

Applications are defined and stored in the Catalog. Once defined, an
Application can be run in one or more Environments.

![image](/images/catalog-model-application.png)

Changes made to an Application in the Catalog, can be propagated to
Application instances running in Environments, based on the
Environment's Update Policy.

Here are some of the common constructs you can use to build Kubernetes
applications with Nirmata:

#### Deployments (stateless components)
{{%excerpt-include filename="Applications/Deployments/_index.md" /%}}

#### StatefulSets (stateful components)
{{%excerpt-include filename="Applications/StatefulSets/_index.md" /%}}

#### Ingresses
{{%excerpt-include filename="Applications/Ingresses/_index.md" /%}}

#### Persistent Volume Claims
{{%excerpt-include filename="Applications/Persistent_Volume_Claims/_index.md" /%}}

#### ConfigMaps
{{%excerpt-include filename="Applications/ConfigMaps/_index.md" /%}}

#### Secrets
{{%excerpt-include filename="Applications/Secrets/_index.md" /%}}

#### Network Policies
{{%excerpt-include filename="Applications/Network_Policies/_index.md" /%}}

#### Custom and Other Resources
{{%excerpt-include filename="Applications/Custom_and_Other_Resources/_index.md" /%}}

#### Kubernetes References
{{%excerpt-include filename="Applications/Kubernetes_References/_index.md" /%}}
