+++
title = "Get all running Applications' IDs, names, and states"
description = ""
weight=60
+++
{{%excerpt%}}
Request:

    GET /environments/api/applications?fields=id,name,state
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [ {
    "id" : "76e72cd9-01dd-490e-be8b-a36951a21881",
    "name" : "nginx",
    "state" : "running",
    "run" : "nginx"
    }, {
    "id" : "97a1352d-4a0c-44b7-8ca6-0e264a203a59",
    "name" : "shopme",
    "state" : "running",
    "run" : "shopme"
    }, {
    "id" : "6a863004-02d7-4a64-85e6-004a140a5823",
    "name" : "aqua-csp",
    "state" : "running",
    "run" : "aqua-csp"
    }, {
    "id" : "bbab3d4f-17d7-45df-883a-e96d5a35def0",
    "name" : "shopmek8s",
    "state" : "running",
    "run" : "dealsapp"
    }, {
    "id" : "9b559b77-4d88-42ca-8280-5145ac3fe9f3",
    "name" : "shopmek8s",
    "state" : "running",
    "run" : "dealsapp"
    }, {
    "id" : "252cdc4b-69f2-4bb4-a688-170b95e516cc",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook"
    }, {
    "id" : "829e362c-cde2-4d06-b1c2-96bef10faed9",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook"
    }, {
    "id" : "343b46f2-6b93-45ac-b38b-bdbc2d133f1e",
    "name" : "guestbook",
    "state" : "running",
    "run" : "guestbook-2"
    } ]
{{%/excerpt%}}
