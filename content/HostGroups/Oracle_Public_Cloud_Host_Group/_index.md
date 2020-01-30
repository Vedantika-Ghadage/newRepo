+++
title = "Oracle Public Cloud Host Group"
description = ""
weight=60
+++
{{%excerpt%}}
To create a Oracle Public Cloud Host Group, you must first setup an [Oracle Cloud Provider](/cloudproviders/#opc-provider).

To create a Host Group, provide the name and select the Cloud Provider.

In the Settings Tab select host instances:

-   Orchestration - to discover instances provisioned by the
        selected orchestration
-   Identity Domain - to discover all instances in the identity
        domain

Once all the information is provided and the wizard is completed, a host
group will be created and the instances will be discovered. Once the
instances connect to Nirmata, they are ready to be used to deploy your
application.

![image](/images/create-oracle-hg.png)

**Note:** For Oracle Public Cloud, the instances need to be created
directly using the Oracle Public Cloud Console or API. For the instance
to be discovered by Nirmata, Docker Engine and Nirmata agent should be
installed on running on the instance. See the [Container Host Setup](/hostgroups/#container-host-setup) section.

{{%/excerpt%}}
