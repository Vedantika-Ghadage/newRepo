+++
title = "Authentication"
description = ""
weight=10
+++
{{%excerpt%}}
To authenticate your account, you can use HTTP BASIC authentication or
an API Key:

    Authorization BASIC <Bas64 user:password>

or:

    Authorization NIRMATA-API <your api key>

Since the Nirmata API is only accessible via HTTPS, your credentials are
sent over an encrypted connection.

To manage your API Key, login to Nirmata and navigate to *Settings ->
Account -> Generate API Key*. An API key is associated with a User
account. When you authenticate an application using the API key, it will
get the role and privileges associated with the account.

A best practice recommendation is to create separate accounts for each
application, and provide the minimum required role and privileges to the
account.
{{%/excerpt%}}
