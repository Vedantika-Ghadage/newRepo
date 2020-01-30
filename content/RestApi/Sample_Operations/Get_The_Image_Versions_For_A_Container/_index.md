+++
title = "Get the image versions for a container"
description = ""
weight=110
+++
{{%excerpt%}}
Request:

    GET https://nirmata.io/environments/api/containers?fields=name,id,image&query={"name" : "php-redis"}
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "04c9ada6-8e62-408e-8bb7-4c5bc5e1db3b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "1ca543fd-f406-4591-b786-382f8d34cac1",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "9f70e9b5-7aa0-4056-ac0a-1c4c6edb0c6b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "53ac22ae-5d32-4341-bf19-fc2e3a27b4f4",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v4"
        },
        {
            "id": "24ae386e-ecc3-4b66-aab0-6e5364f06491",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "c4a11f29-48f1-4184-a05d-4f8d1a1760ab",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "e7f753f1-9ab6-458d-a743-3bf4f9b3e44e",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "40e95708-5bac-4b70-8591-7543aea01c6b",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "8cf514ca-f969-49f3-acc1-8d3dfbeef323",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "cd429f72-356e-41f6-b481-7c3cb1218b79",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "f33d7bb0-ecf3-403e-9d6f-5715bbe6cee4",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "97ca084f-e7cb-42c5-9b8b-f3d7f4c6914c",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "f4b0cb92-8aa6-4b5a-81a1-c51b7d0e3234",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "ffe03a27-be3f-4e81-b3f3-068bae378451",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "6b37a537-fce8-41f0-a5c1-bce980f23391",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "dbc0f31c-bc02-4a08-adb1-f994e9e130df",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        },
        {
            "id": "9bb53549-572c-499b-9bad-1d51079e13f2",
            "name": "php-redis",
            "image": "gcr.io/google-samples/gb-frontend:v5"
        }
    ]

{{%/excerpt%}}
