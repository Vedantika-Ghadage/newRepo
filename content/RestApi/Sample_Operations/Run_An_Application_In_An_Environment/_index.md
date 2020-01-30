+++
title = "Run an Application in an Environment"
description = ""
weight=80
+++
{{%excerpt%}}
Request Headers:

    POST /catalog/api/applications/248ea469-50f2-4b8c-af55-f13a5527a356/run
    Accept: application/json
    Authorization: NIRMATA-API <key>

Request Body:

    {
      "run": "hello1",
      "environment": "dev-test"
    }
{{%/excerpt%}}
