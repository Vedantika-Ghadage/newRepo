+++
title = "Users and Roles"
description = ""
weight=10
+++
{{%excerpt%}}
An account can have multiple users, and each user has a role that
defines what they can see and do. When a new account is created, the
first user has an *admin* role which allows that user to create and
manage additional users for the account.

The following user roles are available:

  Role | Description
  -----|--------
  **admin** | *admin* users have full access to the account and can also manage other users and their access.
  **platform** | *platform* users can all other resorces including Cloud Providers, Host Groups, Policies, Applications, and Environments, but cannot manage users.
  **devops** | *devops* users can manage Applications and Environments. They do not have access to Cloud Providers, Host Groups, and Policies, and cannot manage users.
  **readonly** | *readonly* users can view all data, but create, edit, or delete anything. This role is ideal for system accounts that collect and report data.
{{%/excerpt%}}
