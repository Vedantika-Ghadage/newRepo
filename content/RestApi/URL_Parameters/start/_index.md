+++
title = "start"
description = ""
weight=60
+++
{{%excerpt%}}
The start parameter is used to specify the start index in a list of
resources. It can be used when querying a relation, a list of resources,
or using a query parameter. A positive value is expected. When not
specified a value of 0 is assumed. For example the following query
returns *podStatus* instances 10-20 (or less) that have attribute state
with the *state* of *running*:

    GET  http://www.nirmata.io/environments/api/podStatus?start=10&count=10&query={"state" : "running"}&fields=id
    Accept: application/json
{{%/excerpt%}}
