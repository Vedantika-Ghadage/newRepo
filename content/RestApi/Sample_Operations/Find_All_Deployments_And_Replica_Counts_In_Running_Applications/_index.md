+++
title = "Find all Deployments and replica counts in running Applications"
description = ""
weight=90
+++
{{%excerpt%}}
Request:

    GET /environments/api/applications?mode=exportDetails&fields=id,name,deployments,spec,replicas
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "76e72cd9-01dd-490e-be8b-a36951a21881",
            "name": "nginx"
        },
        {
            "id": "97a1352d-4a0c-44b7-8ca6-0e264a203a59",
            "name": "shopme",
            "deployments": [
                {
                    "id": "f23fb091-ec86-4b1c-aff9-744132d218b5",
                    "name": "payment",
                    "spec": [
                        {
                            "id": "8497448a-8cb0-4a38-9aac-ea941e226bce",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "00979b37-05be-4b09-b5c7-7af68cb7d0c6",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "1d6ef0d7-91df-452c-b8af-ebf91f3e6b09",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "a01d5c5d-d5ae-4fc2-9fe9-6ee57ded98b0",
                    "name": "ratings",
                    "spec": [
                        {
                            "id": "8e0ed849-282a-40b0-8e7c-26ed7f4d8f26",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "6a863004-02d7-4a64-85e6-004a140a5823",
            "name": "aqua-csp",
            "deployments": [
                {
                    "id": "62a4ff2f-ad59-4479-9ba0-ee4104a13ce4",
                    "name": "aqua-all-in-one",
                    "spec": [
                        {
                            "id": "3ae07e78-0ae2-4672-b1df-56330a0c8b47",
                            "replicas": 1
                        }
                    ]
                }
            ]
        },
        {
            "id": "bbab3d4f-17d7-45df-883a-e96d5a35def0",
            "name": "shopmek8s",
            "deployments": [
                {
                    "id": "ec383532-8659-4a34-8d76-7eb5d85ffda3",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "2da3cf04-2cee-4166-9491-566f5c9b3e27",
                            "replicas": 3
                        }
                    ]
                }
            ]
        },
        {
            "id": "9b559b77-4d88-42ca-8280-5145ac3fe9f3",
            "name": "shopmek8s",
            "deployments": [
                {
                    "id": "a9313032-1b82-40dd-b45a-4dabd0689102",
                    "name": "deals",
                    "spec": [
                        {
                            "id": "f9f861e8-defc-433c-b8f0-32c58d2a2fb1",
                            "replicas": 3
                        }
                    ]
                }
            ]
        },
        {
            "id": "252cdc4b-69f2-4bb4-a688-170b95e516cc",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "27d56ae0-c58f-46a0-8b59-ca752f2fa109",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "ad1dcaf3-46fe-4c7d-8891-adfeadc1dc95",
                            "replicas": 3
                        }
                    ]
                },
                {
                    "id": "0b4f6d2e-28ac-4411-b98b-c9fe4875fc7d",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "6f5659de-0a4c-4dbb-8baa-62a690d8538f",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "6d58b6cd-3179-4cdf-97f6-a273970540bf",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "7a01d526-0aaf-47ee-885d-b695a8ac8d2b",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "829e362c-cde2-4d06-b1c2-96bef10faed9",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "1f539cf6-41cd-4739-8872-13409bba612d",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "32c81a2d-145f-4858-8be9-6669c2044079",
                            "replicas": 5
                        }
                    ]
                },
                {
                    "id": "8cd3b93e-2994-4f11-acef-5b4e830e252c",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "87986a72-c250-4002-b4b6-c95cdada3b42",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "003bf3e2-065c-4a32-ac7b-fd2802e49a55",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "2069f1fd-1410-4569-9968-60cbabd140e1",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "343b46f2-6b93-45ac-b38b-bdbc2d133f1e",
            "name": "guestbook",
            "deployments": [
                {
                    "id": "50a1ed10-0167-4c8e-b8b1-a6319bef3cfb",
                    "name": "frontend",
                    "spec": [
                        {
                            "id": "576d2453-b139-4b38-a973-bda0afd9fa6c",
                            "replicas": 6
                        }
                    ]
                },
                {
                    "id": "cad14b31-7d14-46c1-81db-bb1430adb300",
                    "name": "redis-master",
                    "spec": [
                        {
                            "id": "de9d4e5e-f044-46b6-b147-2e9009c07f1b",
                            "replicas": 1
                        }
                    ]
                },
                {
                    "id": "0ef0caf9-b6ad-4a56-9f35-0e4c47a85627",
                    "name": "redis-slave",
                    "spec": [
                        {
                            "id": "1e487ab6-509a-4906-9717-49a2beb59cab",
                            "replicas": 2
                        }
                    ]
                }
            ]
        },
        {
            "id": "40d39730-ea05-4b0c-b78b-5d2d0008606b",
            "name": "dev-test2"
        }
    ]

{{%/excerpt%}}
