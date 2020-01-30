+++
title = "Configuring Cluster Policies"
description = ""
weight=20
+++

To update an existing cluster policy:

1. Select Cluster Polices from the Policies menu.
2. Find and click the name of the policy you wish to edit in the Cluster Policies list.

	<img src="/images/select_cluster_policy.png" style="max-width:50%; height: auto;">
	
After configuring the policy, you can use it when deploying a Kubernetes cluster.

## Policy Details Page
Configure the policy from the Policy Details page.

<img src="/images/cluster_policy_details_page.png" style="max-width:80%; height: auto;">

The Policy Details page contains the following sections:

* [Summary](#summary)
* [Add-ons](#add-ons)
* [Components](#components)
* [Controller Settings](#controller-settings)
* [Ingress Controller](#ingress-controller)
* [Network Plugins](#network-plugins)
* [Proxy Settings](#proxy-settings)
* [Storage](#storage)

### Summary

The Summary section enables users to change the Version, Cloud Provider, and Master Node Scheduling Flag for a policy. 

<img src="/images/cluster_policy_summary.png" style="max-width:50%; height: auto;">

Edit the Summary settings by clicking the Edit icon in the upper right corner of the Summary section.

<img src="/images/edit_cluster_policy_overlay.png" style="max-width:50%; height: auto;">

From the Edit Policy Details overlay, users can:

1. Change the policy Name.
2. Enter a policy Description.
3. Choose a different service Version from the drop-down list.
4. Choose a different Cloud provider from the drop-down list.
5. Check the box for the Disable Schedule On Master Nodes setting. Checking the box enables this setting.
6. Click the Save button to save your changes or click the Cancel button to return to the Policy Details page.

**Note:** users should check the Disable Schedule On Master Nodes box to enable this setting for their cluster policies. Users should turn on Disable Schedule to avoid having the control-plane and applications running on the same nodes.

### Add-ons

The Add-ons section lists all Cluster Add-ons selected when creating the cluster policy.

<img src="/images/cluster_policy_add_ons.png" style="max-width:50%; height: auto;">

The DNS add-on is a default add-on for new cluster policies. You can choose a different add-on if you like.

Some available add-ons include:

* Prometheus monitoring
* Vault authentication agent
* Velero backup and restore

#### Adding More Add-ons
To add more add-ons to a cluster policy:

1. Click the + in the upper right corner of the Add-ons section.

	<img src="/images/cluster_policy_add_on_add.png" style="max-width:50%; height: auto;">
	
	The Add Add-on overlay appears.
	
	<img src="/images/cluster_add_add_on_overlay.png" style="max-width:50%; height: auto;">
	
2. Choose an add-on from the Select Add-on drop-down list. Available options are Prometheus monitoring and the Vault authentication agent.
	
	<img src="/images/cluster_select_add_on.png" style="max-width:50%; height: auto;">
	
3. Enter a Name to identify the add-on instance. The default is the name of the selected add-on.
4. Click the Add button add the add-on instance or click Cancel to return to the Police Details page.

#### Removing Add-ons

To remove add-ons:

1. Click the red X to the right of the add-on name.

	<img src="/images/cluster_remove_add_on.png" style="max-width:50%; height: auto;">
	
	A confirmation overlay appears.
	
	<img src="/images/policy_confirm_add_on_delete.png" style="max-width:50%; height: auto;">
	
2. Click the Delete button to delete the add-on from the cluster policy. Click the Cancel button to return to the Policy Details page.

### Components

The Components section displays all default [Application Components](/introduction/core_concepts/application_components/) configured for a cluster policy. You may add, edit, or delete arguments for cluster components.

<img src="/images/cluster_components.png" style="max-width:80%; height: auto;">

Each application component displayed includes the Name, Image, and Arguments for the component. You may edit a Component Specification to add, edit, or delete its Arguments.

#### Adding a Component Specification Argument

1. To add a component specification argument, click the Edit icon on the right side of the Component section. Be sure to click the icon next to the component you wish to change.

	<img src="/images/cluster_add_component_spec_arg.png" style="max-width:80%; height: auto;">
	
	The Edit Component Spec overlay appears. There are two sections in this overlay: Image and Args.

	The Image field specifies the component image used. Args is the list of key-value pairs (arguments) used by the component.

2. Click + Add Item at the bottom of the Args table.
3. Enter the Key name.
4. Select a Type from the drop-down list. Options are String, Number, and Object.

	<img src="/images/cluster_component_spec_type.png" style="max-width:80%; height: auto;">
	
5. Enter the value for the new key-value pair.
6. Click the Save button to save the new key-value pair or click Cancel to return to the Policy Details page.

#### Editing Component Specification Arguments

To edit a component specification argument, click the Edit icon on the right side of the Component section. Be sure to click the icon next to the component you wish to change.

1. Click inside the field containing the value you wish to modify.

	<img src="/images/cluster_edit_component_spec.png" style="max-width:80%; height: auto;">
	
2. Enter the new value for the key.
3. Click the Save button to save your changes, or click Cancel to return to the Policy Details page without saving your changes.

#### Deleting Component Specification Arguments

To delete a component specification argument, click the Edit icon on the right side of the Component section. Be sure to click the icon next to the component you wish to change.

1. Click the X on the right side of the argument you wish to delete.
2. Click the Save button to save your changes, or click Cancel to return to the Policy Details page without saving.

<img src="/images/cluster_delete_component_spec.png" style="max-width:80%; height: auto;">

### Controller Settings

The Controller Settings Panel allows you to enable or disable these cluster policy settings:

* Is Insecure 
* Use HTTP Proxy

<img src="/images/cluster_controller_settings.png" style="max-width:50%; height: auto;">

#### Editing Controller Settings

1. To change Controller Settings, click the Edit icon on the right side of the Controller Settings section.

	The Edit Controller Spec overlay appears.

	<img src="/images/controller_edit_settings.png" style="max-width:50%; height: auto;">
	
2. To enable insecure HTTP connections, check the box next to Is Insecure.
3. To use an HTTP proxy, check the box next to Use Http Proxy.
4. Click the Save button, or click Cancel to return to the Policy Details page without saving.

To disable either or both controller settings, uncheck the box and save the updated settings.

**Note:** you must enable the Is Insecure setting if you are using a self-signed SSL certificate for your application.

### Network

The Network panel allows you to manage ingress controllers and network plugins for the cluster. From the Policy Details page, you may view, download, and add ingress controller specifications for a cluster policy. The default Nirmata ingress controller is for HAProxy.

**Note:** you may only have one Ingress controller spec at a time for a Cluster Policy. Uploading a new one replaces the existing default spec.

<img src="/images/cluster_policy_network_panel.png" style="max-width: 50%; height: auto;">

#### Viewing or Downloading an Existing Ingress Controller Specification

1. To view or download an existing ingress controller specification, click on the name of the specification in the Name column of the Ingress Controller section of the Network panel.

	The YAML file viewer for the selected Ingress controller appears.
	
	<img src="/images/download_ingress_controller_yaml.png" style="max-width: 80%; height: auto;">
	
2. Scroll to view the entire file.
3. Click the Download button to download a zip file containing the YAML controller specification.
4. Click the Cancel button to close the overlay and return to the Policy Details page.

You may use the downloaded YAML controller specification file as a template for creating a new one.

#### Adding Ingress Controller Specifications

1. First, create a YAML controller specification file with the desired settings.
2. Click the + button on the right in the Ingress Controller section of the Network panel.

The Add Ingress Controller Spec appears.

<img src="/images/add_ingress_controller_spec.png" style="max-width: 50%; height: auto;">

2. Enter a Name for the new ingress controller spec.
3. Upload your YAML controller specification file. Click inside the dotted line field to select and upload your file, or drag the file inside the dotted line field.
4. Click the Add button to add the ingress controller spec, or click Cancel to return to the Policy Details page.

**Note:** you may only have one ingress controller spec at a time for a Cluster Policy. Uploading a new one replaces the existing default spec.

#### Deleting Ingress Controller Specifications

1. Click the red X to the right of the Ingress controller specification.

<img src="/images/cluster_delete_ingress_controller.png" style="max-width: 50%; height: auto;">

### Network Plugins

Nirmata packages Flannel by default, and uses the CNIs provided by cloud providers for Kubernetes networking. Customers wishing to use a different CNI  can add the plugin YAML using the Network panel.

#### Adding Network Plugins

1. To add a network plugin, you must first get a plugin YAML file.
2. Click Add Network (CNI) Plugin in the Network panel.

	<img src="/images/cluster_add_network_plugin.png" style="max-width: 50%; height: auto;">

	The Add a Network (CNI) Plugin overlay appears.

	<img src="/images/cluster_add_network_plugin_overlay.png" style="max-width: 50%; height: auto;">
	
3. Enter a Name for the network plugin.
4. Upload your plugin YAML file. Click inside the dotted line field to select and upload your file, or drag the file inside the dotted line field.
5. Click the Add button to add the new network plugin spec or click Cancel to return to the Policy Details page.

### Proxy Settings

Proxy settings allow you to specify the IP addresses Kubernetes uses for proxies for your cluster policy.

<img src="/images/cluster_proxy_settings.png" style="max-width: 50%; height: auto;">

#### Adding Proxy Settings

1. To add proxy settings, click the edit icon on the upper right of the Proxy Settings section of Policy Details.

	The Edit Proxy Settings Spec overlay appears.
	
	<img src="/images/cluster_edit_proxy_settings.png" style="max-width: 50%; height: auto;">
	
2. Enter the IP address for an HTTP proxy in the HTTP Proxy field.
3. Enter the IP address for an HTTPS proxy in the HTTPS Proxy field.
4. Enter the IP address used when there is no proxy.
5. Click the Save button to save your changes or click Cancel to return to the Policy Details page.

#### Editing Proxy Settings

1. To edit proxy settings, click the edit icon on the upper right of the Proxy Settings section of Policy Details.
2. Change the IP address values.
3. Click the Save button to save your changes or click Cancel to return to the Policy Details page.


#### Deleting Proxy Settings

1. To delete proxy settings, click the edit icon on the upper right of the Proxy Settings section of Policy Details.
2. Delete the IP address values.
3. Click the Save button to save your changes or click Cancel to return to the Policy Details Page.

### Storage
You can add, view, download, or delete storage class plugins from your cluster policy. By default, Nirmata picks a storage class based on infrastructure type. For public clouds, it uses default block storage class available for respective public clouds.

<img src="/images/cluster_storage_class.png" style="max-width: 50%; height: auto;">

#### Viewing and Downloading Storage Class Plugin

1. To view and download the storage plugin YAML file click on the name of the storage class in the Name column of the Storage panel.

	The YAML file viewer for the selected storage class appears.
	
	<img src="/images/cluster_storage_class_yaml.png" style="max-width: 80%; height: auto;">
	
2. Click the Download button to download a zipped copy of the YAML file or click Cancel to return to Policy Details.

You may use the downloaded YAML storage class plugin file as a template for creating a new plugin YAML file.

#### Adding a Storage Class Plugin

1. To add a storage class plugin, you must supply a plugin YAML file.
2. Click Add Storage (CSI) Plugin in the Storage panel.

	<img src="/images/cluster_storage_class_add_plugin.png" style="max-width: 50%; height: auto;">
	
	The Add Storage Class Spec overlay appears.
	
	<img src="/images/cluster_add_storage_class_spec_overlay.png" style="max-width: 50%; height: auto;">

3. Enter a Name for the storage plugin spec.
4. Upload your plugin YAML file. Click inside the dotted line field to select and upload your file, or drag the file inside the dotted line field.
5. Click the Add button to add the new storage class plugin spec or click Cancel to return to Policy Details.

The newly added storage class plugin appears in the Storage Plugins section of the Storage panel.

<img src="/images/cluster_storage_plugin.png" style="max-width: 50%; height: auto;">

#### Deleting a Storage Class Plugin

1. Click the red X to the right of the storage class plugin spec you wish to remove.

	<img src="/images/cluster_delete_storage_class_plugin.png" style="max-width: 50%; height: auto;">
	
	A confirmation Overlay appears.
	
	<img src="/images/cluster_delete_storage_plugin_confirm.png" style="max-width: 50%; height: auto;">
	
2. Click the Delete button to delete the storage class plugin spec, or click Cancel to return to Policy Details.
