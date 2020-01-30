+++
title = "HAProxy Setup"
description = ""
weight=20
+++

Nirmata uses HAProxy, an open source load balancer proxy, for TCP and HTTP applications.

* [Installing HAProxy](https://docs.nirmata.io/integrations/ingress-controllers/haproxy-setup/#installing-haproxy)
* [Checking HAProxy Deployment Status](https://docs.nirmata.io/integrations/ingress-controllers/haproxy-setup/#checking-haproxy-deployment-status)
* [Installing Multiple Instances of HAProxy](https://docs.nirmata.io/integrations/ingress-controllers/haproxy-setup/#installing-multiple-instances-of-haproxy)

## Installing HAProxy

1. Click Environments in the left navigation.  

1. Click the target environment to install HAProxy.  

1. Click the + to Run an Application.  

	The Run Application setup overlay appears.
	
	<img src="/images/run_app_overlay.png" style="max-width: 80%; height: auto;">

4. Enter a unique Run name for the application that includes *haproxy.*

	Example: `my-env-haproxy`

5. Use the default selection Catalog for Upstream Type.
6. Select HAProxy from the Catalog Application drop-down menu.
7. Click the Run Application button to save your changes and run HAProxy on the environment. Click Cancel to return to the Environment Details page.

	<img src="/images/ha_proxy_app_page.png" style="max-width: 100%; height: auto;">

**Notes:**

* There will be a short delay while the application is deployed and launched. Note the *Executing* state of the deployment(s).
* If successfully executed, the Status column indicates the application is Running.

### Checking HAProxy Deployment Status
1. Click the arrow next to the Search box.

	<img src="/images/haproxy_ingress_deployment.png" style="max-width: 100%; height: auto;">
	
2. Note the newly deploying instance of haproxy-ingress.

	<img src="/images/haproxy_deploy_exec.png" style="max-width: 100%; height: auto;">
	
	
On completion, the Application Details page shows the State as *Running* if the HAProxy installation was completed successfully.

If the HAProxy resources are running, the HAProxy installation is complete.

## Installing Multiple Instances of HAProxy
To install mulitple instances of HAProxy, you must do the following for each new instance:

1. Create a unique Cluster Role Binding.
2. Create a unique Ingress Class.

### Creating a Unique Cluster Role Binding
The new instance of HAProxy requires a unique Cluster Role Binding with a unique name. To create a unique Cluster Role Binding:

1. Click on the HAProxy instance installed in your environment.

	<img src="/images/environment_details.png" style="max-width: 80%; height: auto;">
	
2. The Application Details page appears. Click on Storage & Configuration.
	
	<img src="/images/application_details.png" style="max-width: 100%; height: auto;">
	
3. Scroll down to the Other Resources section. Note the resources identified as *ClusterRoleBinding* in the Kind column. Use an existing cluster role binding as a template to create a unique instance.

4.  Click on an existing cluster role binding.

	<img src="/images/select_crb.png" style="max-width: 80%; height: auto;">
		
	The Cluster Role Binding Detail page is displayed.
	
	<img src="/images/crb_details.png" style="max-width: 100%; height: auto;">
	
5. Click the Download button to download a copy of the cluster role binding YAML file.

	<img src="/images/crb_yaml_download.png" style="max-width: 80%; height: auto;">
	
6. Open the downloaded YAML file and give the cluster role binding a unique name by modifying *name* under *metadata.*

	<img src="/images/edit_crb_yaml.png" style="max-width: 60%; height: auto;">
	
7. Rename the new cluster role binding YAML file using the same unique name specified when editing the file in the previous step.

	Example: `hap-appscorpent1-crb3.yaml`

8. Click the browser Back button to return to the Application Details page.

9. Click the gear icon on the right side of the Application Details page and select Import to Application from the menu.

	<img src="/images/import_crb_yaml.png" style="max-width: 35%; height: auto;">
	
	The Import YAML to Application HAProxy overlay appears.
	
	<img src="/images/import_haproxy_yaml.png" style="max-width: 75%; height: auto;">

10. Click inside the gray box to open a file selector, or drag your file inside the gray box to upload the new cluster role binding.

11. Click the Import button or click cancel to return to the previous page.

	Note the presence of the new cluster role binding in the Other Resources section of Application Details. 
	
	<img src="/images/new_crb_resource.png" style="max-width: 75%; height: auto;">
	
12. Delete the existing cluster role binding used when creating the new cluster role binding.

	<img src="/images/delete_crb.png" style="max-width: 75%; height: auto;">
	
13. A confirmation overlay appears. Click Delete to continue or click Cancel to return to the previous page.

	<img src="/images/confirm_delete_crb.png" style="max-width: 60%; height: auto;">
	
Next step: create a unique ingress class for HAProxy.

### Creating a Unique Ingress Class

The new instance of HAProxy requires an ingress class with a unique name. To create a unique ingress class:

1. Click on the HAProxy instance installed in your environment.

	<img src="/images/environment_details.png" style="max-width: 80%; height: auto;">
	
2. The Application Details page appears. Click the gray arrow button under Workloads to expand the service details.

	<img src="/images/haproxy_ingress_deployment.png" style="max-width: 100%; height: auto;">
	
3. Click the pod instance for HAProxy.

	<img src="/images/select_haproxy_pod.png" style="max-width: 80%; height: auto;">
	
4. The Pod Details page appears. Click haproxy-ingress under Containers.

	<img src="/images/select_haproxy_ingress_container.png" style="max-width: 100%; height: auto;">
	
5. The Container Detail page appears. Scroll down to the Container Spec section and click View Container in Pod Template on the right.

	<img src="/images/container_detail_spec.png" style="max-width: 100%; height: auto;">
	
6. The Container Template page appears. Scroll to the top and click the edit icon in the Container Template section on the right.

	<img src="/images/edit_haproxy_template.png" style="max-width: 100%; height: auto;">
	
7. The Edit Container overlay appears.

	<img src="/images/edit_container_overlay.png" style="max-width: 80%; height: auto;">
	
8. In the Args section, click inside the field containing the `--ingress-class` argument.

	<img src="/images/ingress_class_args.png" style="max-width: 65%; height: auto;">
	
9. Modify the value of the key value-pair to be a unique instance for the ingress class. 

	Example: `--ingress-class=ingress10`

10. Click Save to continue. Click Cancel to return to the previous page.

**Note:** upon saving there will be a short delay during the pod redeployment using the new ingress class.

[Check HAProxy deployment status](https://docs.nirmata.io/integrations/ingress-controllers/haproxy-setup/#checking-haproxy-deployment-status) after adding or modifying a cluster role binding or ingress class. 