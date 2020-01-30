+++
title = "Get the UUID of an Application named 'helloworld' in YAML format"
description = ""
weight=50
+++
{{%excerpt%}}
Request:

    GET /catalog/api/applications?query={"name": "helloworld"}&fields=id&output=YAML
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    ---
    - id: bdf910d6-f12d-4a9d-84e6-bfbae806c558
{{%/excerpt%}}
