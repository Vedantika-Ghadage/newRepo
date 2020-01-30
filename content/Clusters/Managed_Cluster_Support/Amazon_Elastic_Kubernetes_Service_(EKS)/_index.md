+++
title = "Amazon Elastic Kubernetes Service (EKS)"
description = ""
weight=20
+++

EKS is Amazon Web Services Managed Kubernetes Cluster service that allows customers to run their containerized applications on AWS cloud.  Nirmata significantly simplifies EKS cluster deployment and management and takes away undifferentiated heavy lifting required to bring your AWS EKS cluster up. Nirmata provides significant constructs that helps customer leverage EKS deployments to their fullest. Some of those features include:

1. **Policy Management:** Nirmata provides easy means to centrally manage policies for your clusters, namespaces, and applications.

2. **Application Catalog:** Nirmata Kubernetes compliant application catalog that can help you easily model, deploy and manage your applications.

3. **Governance:** Nirmata provides easy ways to offer virtual clusters from your EKS setup to  different teams and optimize the resource utilization of your cluster.

4. **CI/CD Integration:** Nirmata integrates with your approach and toolsets for CI/CD. Whether you want to use Jenkins, Bamboo, or Kustomize or want to   use GitOps style management or push based change management; even manage your applications through Jenkins or directly through Nirmata. The choice is yours, Nirmata just makes it easy.

5. **Full Application Lifecycle Management:** Nirmata provides full application lifecycle management with visibility, operations, and troubleshooting capabilities right from single screen, across all of your clusters. This includes, logging, analytics across applications, cluster and namespaces, Dashboards and the ability to log into containers and pods to troubleshoot an application. All from a single place.


Nirmata provides easy integration both with Private and Cloud Edition. While Cloud Edition requires Nirmata Role configuration with necessary policies, Nirmata Private Edition uses an AWS user to provide the necessary permissions to nirmata to create EKS cluster control plane and associated workder nodes.

[Cloud Edition](./cloud_edition/)

[Private Edition](./private_edition/)
