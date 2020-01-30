+++
title = "ConfigMaps"
description = ""
weight=50
+++
{{%excerpt%}}
ConfigMaps allow you to decouple configuration from your container
image, ensuring that your containerized application is portable.

ConfigMaps can be made available to your pod as:

 1.  Environment variables
 2.  Volumes

A ConfigMap can be shared across multiple pod templates further
simplifying your application configuration.

#### How to Add a Config Map to Your Application

To add a Config Map to your Application, click on *Catalog* in the sidebar menu and then select *Applications.* Open an application and click on the *Config & Storage* tab.

Click on the + icon on the *Config Maps* card.

![image](/images/config-maps-1.png)

Enter the Config Map data and click *Next*.

![image](/images/config-maps-2.png)

Enter the Config Map *Labels & Annotations* and click *Next*.

![image](/images/config-maps-3.png)

The new Config Map is displayed.

![image](/images/config-maps-4.png)

{{%/excerpt%}}
