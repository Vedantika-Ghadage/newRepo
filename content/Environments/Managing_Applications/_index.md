+++
title = "Managing Applications"
description = ""
weight=70
+++
{{%excerpt%}}
Once an application is running, you can select it to get complete
visibility and manage any of its components.

![image](/images/environments-running-application.png)

From the main application view you can drill-down into components, and
even individual containers.

![image](/images/environments-running-pod.png)

##### Change Management
When an application is modified in the Catalog, Nirmata will propagate the changes to each running instance of the application. The changes will be processed based on the Update Policy of each environment. If the Update Policy is set to "View" a notification is shown when changes are available. You can then view the changes and decide to accept or reject them.

![image](/images/environments-pending-changes.png)

##### Scaling Pods
You can scale Pods for your Deployments or StatefulSets in a running
Application. Simply select the scaling icon next to a component, or at
the top right of the components table and set the desired replica
counts.

![image](/images/environments-scaling.png)

##### Application Activity

Nirmata automatically tracks and correlates all user and system changes made to applications. You can view all activity for an application in the activity panel:

![image](/images/environments-activity.png)

##### Application Metrics
Nirmata collects and aggregates several statistic from each Pod and
automatically aggregates them by components and applications. You can
view these statistics (aggregated) at the application level, or for an
individual resources:

![image](/images/environments-monitoring.png)

##### Application Events & Tasks
Nirmata records all Kubernetes tasks performed (e.g. API calls) and also
records events received from Kubernetes. This makes it very easy to
troubleshoot application issues:

![image](/images/environments-events-n-tasks.png)

##### Cloud Shell
Using Nirmata, you can launch a remote shell into an application
container without requiring complex VPN or host access. To launch a
Cloud Shell navigate to the "Running Containers" panel and click
"Launch Terminal":

 ![image](/images/environments-cloud-shell-1.png)

This action opens a new browser window with an embedded shell:

 ![image](/images/environments-cloud-shell-2.png)


##### Container Logs
You can also stream a containers log (STDOUT and STDERR) output, by
selecting the "View Logs" action:

 ![image](/images/environments-container-logs.png)


{{%/excerpt%}}
