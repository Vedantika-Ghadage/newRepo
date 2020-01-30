+++
title = "query"
description = ""
weight=20
+++
{{%excerpt%}}
The query parameter is used to control which objects are included in a
JSON response. The query data is specified as a JSON object. The query
parameter can be applied to any GET request that returns multiple
objects. For example the following query returns the application named
'helloworld':

    GET  http://www.nirmata.io/environments/api/applications?query={"name":"helloworld"}
    Accept: application/json

Multiple attributes can be specified for a logical AND operation:

    GET  http://www.nirmata.io/environments/api/applications?query={"name":"helloworld", "run" : "hello1"}
    Accept: application/json
{{%/excerpt%}}
