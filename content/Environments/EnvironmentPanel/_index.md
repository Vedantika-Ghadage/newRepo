+++
title = "Environments Panel"
description = ""
weight=10
+++
{{%excerpt%}}

To view the Deployment status for a component, navigate to the Environment and then select the component.

Quickly navigate between Component, Service, Pod, Container Template, and Running Container from within each view.

#### Component View

Each component view provides access to Deployment Status, Deployment Spec, Pod Template, and Related Resources. Click on any link within a category to quickly navigate to the detail page.

From the Related Resources panel, view Services, Persistent Volume Claims, and Horizontal Pod Autoscalers.

![image](/images/epanel-1.png)

Click on the links within the Related Resources panel to perform component-specific actions or to view component-specific service details.

**Services:**

* Delete a service
* View service details

**Persistent Volume Claims (PVC):**

* Delete PVC
* Edit PVC
* View PVC details

[Click here for detailed information on adding a Resource Quota or Limit Range.](https://docs.nirmata.io/environments/resource_quota__limit_range/)

**Horizontal Pod Autoscalers (HPA):**

* Add HPA
* Edit HPA
* Delete HPA
* View HPA details

NOTE: HPA is associated with a component by the Target field in the HPA creation form.

#### Service View

From within the Related Resources panel, click on a service name to view the service metrics and access service-specific Resources.

![image](/images/epanel-2.png)

The Related Resources Panel displays the Workload Controller and Ingresses for the specified service.

![image](/images/epanel-3.png)

#### Pod View

To access the Pod View, click on pod name in the Service View. The Pod view displays pod metrics and pod-specific Resources.

![image](/images/epanel-4.png)

The Related Resources panel displays the Workload Controller and Services for the specified pod.

#### Container Template View

To access the Container Template View, click on container name in the Pod View. The Container Template view displays container template metrics.

![image](/images/epanel-5.png)

All Running Containers that use the specified template are displayed near the bottom of the page.

#### Running Container View

To view a Running Container, click on the container name in the Running Containers panel. The Container detail page displays the Workload Controller, Pod, and Volumes for the specified Container in the Related Resources Panel.

![image](/images/epanel-6.png)
