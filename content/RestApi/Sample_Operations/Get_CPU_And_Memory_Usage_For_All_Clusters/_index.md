+++
title = "Get CPU and memory usage for all Clusters"
description = ""
weight=150
+++
{{%excerpt%}}
Request:

    GET /cluster/api/hostClusters?mode=exportDetails&fields=id,name,kubernetesCluster,clusterStats,cpuUsagePercent,memoryUsagePercent
    Accept: application/json
    Authorization: NIRMATA-API <key>

Response Headers:

    HTTP/1.1 200 OK
    ...

Response Body:

    [
        {
            "id": "b33efdd1-7c10-4ca9-9c7d-a6e6baf65c4e",
            "name": "prod-cluster",
            "kubernetesCluster": [
                {
                    "id": "a6795f23-0801-4023-849c-9a7595e1e921",
                    "clusterStats": [
                        {
                            "id": "eafb354f-5c7e-4c6b-a6b7-e2ea0053c00f",
                            "cpuUsagePercent": 15.6,
                            "memoryUsagePercent": 59.060432
                        }
                    ]
                }
            ]
        },
        {
            "id": "fc91f1f5-6bb8-49d0-a506-cb770515a141",
            "name": "test-centos",
            "kubernetesCluster": [
                {
                    "id": "6619ae16-a8a0-4374-9ad7-baf5d0590f7d",
                    "clusterStats": [
                        {
                            "id": "6118e6dd-2536-43f7-9a79-1d2885a1aa7a",
                            "cpuUsagePercent": 8.175,
                            "memoryUsagePercent": 55.651302
                        }
                    ]
                }
            ]
        },
        {
            "id": "49202821-a458-45c8-8799-1a79e012471b",
            "name": "devtest-aks-us-east",
            "kubernetesCluster": [
                {
                    "id": "22259547-fd15-4a66-ba42-ae24ccb82563",
                    "clusterStats": [
                        {
                            "id": "286912b7-70ce-439e-8a59-0f51d9d2c0f4",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "f8aa846f-9c2d-4b2c-838f-23a8132ba78e",
            "name": "prod-azure-cluster",
            "kubernetesCluster": [
                {
                    "id": "3b026363-7f11-4ef7-a418-c8f73a34f6da",
                    "clusterStats": [
                        {
                            "id": "dbcea04b-7263-49b8-b9cd-f610782da5f0",
                            "cpuUsagePercent": 3.975,
                            "memoryUsagePercent": 13.631612
                        }
                    ]
                }
            ]
        },
        {
            "id": "cde8bdd5-37f4-445c-bf67-399fc22fffde",
            "name": "prod-aks-us-east2",
            "kubernetesCluster": [
                {
                    "id": "e8535a60-122a-41cc-9aac-b619dc3a3b8b",
                    "clusterStats": [
                        {
                            "id": "3ca358c1-c21a-43e1-a24a-770438515d57",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "933951fe-da2e-4bb1-a7d5-8dd092ff4ca2",
            "name": "aks-demo",
            "kubernetesCluster": [
                {
                    "id": "b4d8884d-e4c9-4881-8997-74b9a1bffa39",
                    "clusterStats": [
                        {
                            "id": "0dd79692-4ded-442d-a3a2-6519ee114901",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        },
        {
            "id": "c9bc4e81-4140-4120-afd1-4c8dc4b88574",
            "name": "diamanti-cluster-1",
            "kubernetesCluster": [
                {
                    "id": "c2d32dce-9e7b-4f03-9f2c-93936635c793",
                    "clusterStats": [
                        {
                            "id": "f21799b0-0ad7-40e3-a999-9c61fe022b00",
                            "cpuUsagePercent": 0,
                            "memoryUsagePercent": 0
                        }
                    ]
                }
            ]
        }
    ]
{{%/excerpt%}}
