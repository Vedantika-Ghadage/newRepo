+++
title = "count"
description = ""
weight=50
+++
{{%excerpt%}}
The count parameter is used to specify the maximum number of resources
to be returned. It can be used when querying a relation, a list of
resources, or using a query parameter. A positive value is expected.
When not specified, all matching resources are returned. For example the
following query returns the podIP and state fields for up to 10
instances of the resource *podStatus*:

    GET  http://www.nirmata.io/environments/api/podStatus?count=10&fields=podIP,state
    Accept: application/json
{{%/excerpt%}}
