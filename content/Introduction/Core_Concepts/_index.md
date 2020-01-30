+++
title = "Core Concepts"
description = ""
weight=40
+++
{{%excerpt%}}
This section discusses the core concepts in Nirmata. Most of these
concepts will be familiar, as Nirmata does not introduce any unnecessary
abstractions. The picture below shows the main entities, and their
relationships to each other. Each of these concepts are further defined
below:

![image](/images/concepts.png)

##### Applications
Applications are composed of multiple Components. Applications can be
defined in a Catalog and can run in one or more Environments. While
Nirmata has been designed for Microservices-style applications, it is
easy to model and manage traditional 3-tier applications as well.

##### Application Components
A Component is simply part of an Application. A Component maps to
Kubernetes workload API constructs. For example a stateless component
will map to a Deployment and be exposed by a Service, whereas a stateful
component will map to a StatefulSet and may be exposed by a headless
Service. Nirmata's intuitive and powerful user interfaces provide
step-by-step guidance to building Kubernetes applications, but can also
support low-level YAML manipulation for expert users.

##### Environments
An Environment contains runtime instances of one or more Applications.
Environments can be created for different stages of a development
pipeline, such as dev-test, staging, production or can be based on
deployment characteristics such as regions.

##### Clusters
Clusters represent Kubernetes components and nodes. With Nirmata, you
can deploy and operate Kubernetes clusters from scratch, or can discover
and operate existing clusters created by other providers.

##### Policies
Policies are used to govern resource usage, application constraints, and
ensure scalable, consistent, and repeatable behaviors across multiple
teams. In Nirmata declarative policies are used to manage all resources.

##### Cloud Providers
Cloud Providers supply resources to run application containers. You can
create one or more cloud providers, setup pools of hosts (Host Groups)
from them, and then compose clusters from the Host Groups.

Nirmata currently supports the following cloud providers:

-   Public Clouds

    -   Amazon Web Services (AWS)
    -   Microsoft Azure
    -   Google Compute Engine
    -   Oracle Cloud Services

-   Private Clouds:

    -   VMware vSphere
    -   OpenStack
    -   Diamanti

-   Direct Connect (any virtual or physical server)

Nirmata can securely manage both public and private clouds, without
requiring any special network or firewall configuration.

##### Host Groups
Host Groups are pools of container hosts with the same configuration,
created in a Cloud Provider. For example, you can allocate pools of
resources based on service tiers, application characteristics, or
application lifecycle needs. 

##### Containers
Each Service runs in a Container. Nirmata uses the [Docker
Engine](http://www.docker.io) as its container technology. Since Docker
is an open technology, you can always keep control of your images, and
can also run them outside of Nirmata.

##### Image Registries
An Image Registry stores Docker images, which are typically produced by
a build system. Nirmata supports both public and private image
registries. You can setup your build tools to generate images for each
service, and then trigger Nirmata to deploy the images.
{{%/excerpt%}}
