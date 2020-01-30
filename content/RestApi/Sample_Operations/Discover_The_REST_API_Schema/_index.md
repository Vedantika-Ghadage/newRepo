+++
title = "Discover the REST API schema"
description = ""
weight=190
+++
{{%excerpt%}}
The Nirmata REST API schema can be queried using the HTTP OPTIONS
method. Here is a query and JQ filter to obtain all endpoints (model
classes):

Request:

    curl -X OPTIONS -H "Accept: application/json" -H "Authorization: NIRMATA-API <key>" https://nirmata.io/config/api | jq ".modelClasses | .[] .modelIndex"

Response:

    "Root"
    "Application"
    "EnvironmentType"
    "ContainerType"
    "ResourceSelectionPolicy"
    "ResourceSelectionRule"
    "CloudProvider"
    "HostGroup"
    "Host"
    "Container"
    "Service"
    "Environment"
    "ServiceInstance"
    "ServicePort"
    "ServiceSpec"
    "Registry"
    "LaunchConfiguration"
    "PortRange"
    "VSphereConfig"
    "OpenStackConfig"
    "WebHook"
    "ScalingPolicy"
    "DesiredService"
    "ScalingRule"
    "VCloudConfig"
    "ServiceInstanceAction"
    "ServiceAffinityRule"
    "ServiceScalingRule"
    "RoutingPolicy"
    "RoutingRule"
    "GatewayRoute"
    "GatewayPolicy"
    "GatewayRule"
    "AzureConfig"
    "DesiredServiceAction"
    "PrivateCloud"
    "CiscoIcfConfig"
    "CiscoUcsdConfig"
    "HealthCheck"
    "ClusterNode"
    "Cluster"
    "UpdatePolicy"
    "ImageUpdateEvent"
    "GatewayConfig"
    "ContainerAction"
    "DesiredServiceLabelSelector"
    "LabelSelectorItem"
    "EnvironmentVariable"
    "HostAction"
    "DigitalOceanConfig"
    "ProfitBricksConfig"
    "AwsConfig"
    "HostScalingRule"
{{%/excerpt%}}
