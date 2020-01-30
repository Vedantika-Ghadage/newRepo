+++
title = "Jira Change Management"
description = ""
weight=120
+++

{{%excerpt%}}

Nirmata's Jira Change Management integration allows users to change an application and automatically track the change in Jira.

To start, generate a Jira API  token by visiting id.atlassian.com.

Login to your account, select *Security* and then *Create and Manage API token*. Then select *Create API Token*. Copy the API token.

![image](/images/jira-1.png)

From the side bar menu in Nirmata, navigate to *Settings* and then select *Jira Settings*.

Apply a name to the new Jira settings and add the site URL, the Jira users' email and API token and click *Next*.
After the account is validated, click *Finish*.

![image](/images/jira-2.png)

The new configuration credentials are displayed in the *Jira Settings* list.

To make changes trackable in the application, set the *Environment Update Policy* to *Notify* and then configure Jira as the Change Tracker. Select the appropriate Jira setting, enter a *Project Key*, and select a *Priority*.

![image](/images/jira-3.png)

When a change is made to the application, a Change Request is generated in Nirmata. When the request is accepted, a Jira ticket is created in the configured account.

![image](/images/jira-4.png)

The Jira ticket is assigned to the project lead. The difference YAML and change ID are noted in the description. The ticket is labeled with the kind of YAML, the type of operation, the application name, and the environment name.

A note in the Comments section captures the status of the change.

![image](/images/jira-5.png)

#### How to Edit Jira Settings

The Jira Project Key and Priority Type can be modified from the Environment.

![image](/images/jira-6.png)

New credentials and API tokens must be modified from the global Jira Settings. When a global Jira Setting is modified, every Environment that contains the setting is updated with the new information.

![image](/images/jira-7.png)

{{%/excerpt%}}
