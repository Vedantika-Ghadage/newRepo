+++
title = "Apply YAML updates to a running Application"
description = ""
weight=140
+++
{{%excerpt%}}
Request:

    curl -X POST -H "Content-type: text/yaml" -H "Authorization: NIRMATA-API $APIKEY" "https://nirmata.io/environments/api/applications/829e362c-cde2-4d06-b1c2-96bef10faed9/import" --data-binary @redis-slave.yml

Response:

    {
        "status" : 200,
        "message" : "Success",
        "changes" : {
            "user" : "jim@nirmata.com",
            "createdIds" : [ ],
            "modifiedIds" : [ {
            "modelIndex" : "Container",
            "uuid" : "1dff2449-a4f3-46a8-9b85-ad97eb0926d3",
            "service" : "Environments"
            } ],
            "deletedIds" : [ ],
            "sequenceId" : "dbe828e0-c079-4cc5-9562-f8c680fd8529",
            "timestamp" : 1526888853548,
            "empty" : false,
            "id" : "38c87ee5-0585-406e-82ac-5840551a8bef"
        }
    }

{{%/excerpt%}}
