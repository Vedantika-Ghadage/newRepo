+++
title = "GCE Host Groups"
description = ""
weight=50
+++
{{%excerpt%}}
To create a GCE Host Group, you must first setup a
[GCE Cloud Provider](/cloudproviders/#gce-provider).

To create a Host Group, provide the name and select the Cloud Provider.
Then select the desired host count.

In the Settings Tab enter value for:

  -   Zone
  -   Configuration Type:
          -   Image: to use a pre-built image
          -   Instance Group: to use the instance group

Provide additional settings based on the configuration type selected.

On the Tags tab enter the tags to apply to the instances.

On the StartUp Script Tab, click on checkbox to use a default script to
install Docker and Nirmata agent or provide your own script.

Once all the information is provided and the wizard is completed, a host
group will be created and the instances will be provisioned. Once the
instances connect to Nirmata, they are ready to be used to deploy your
application.
{{%/excerpt%}}
