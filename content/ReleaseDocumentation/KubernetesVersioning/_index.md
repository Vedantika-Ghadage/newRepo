+++
title = "Kubernetes Versioning"
description = ""
weight=10
+++

#### Kubernetes API Version Support

Nirmata supports the current release of Kubernetes plus three prior releases. The current default Kubernetes version in Nirmata is 1.12.

Users can install and deploy unsupported versions; however, Nirmata has only tested and validated those versions listed below.

|               | Kubernetes 1.12 | Kubernetes 1.13 | Kubernetes 1.14 | Kubernetes 1.15 |
|---------------|-----------------|-----------------|-----------------|-----------------|
| Nirmata 2.5.0 | Yes             | No              | No              | No              |
| Nirmata 2.6.0 | Yes             | Yes             | No              | No              |
| Nirmata 2.7.0 | Yes             | Yes             | Yes             | No              |
| Nirmata 2.8.0 | Yes             | Yes             | Yes             | Yes             |

##### How to Use Other Kubernetes Versions

Other versions of Kubernetes may be deployed with Nirmata. However, it is recommended that non-supported versions be deployed only outside of production environments.