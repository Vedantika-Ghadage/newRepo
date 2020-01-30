+++
title = "Query a cluster's state"
description = ""
weight=180
+++
{{%excerpt%}}
Request:

    GET https://nirmata.io/cluster/api/hostClusters?fields=id,state&query={"name" : "devtest-aks-us-east"}
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "49202821-a458-45c8-8799-1a79e012471b",
            "state": "ready"
        }
    ]

{{%/excerpt%}}
