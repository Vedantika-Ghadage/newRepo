+++
title = "Cluster Policies"
description = ""
weight=20
+++

Users must create and configure a cluster policy before creating a Kubernetes cluster.  Cluster policies are reusable, and may be to multiple clusters. Cluster policy reuse simplifies cluster configuration.
 
Nirmata provides default cluster policies for all major cloud providers. Use the default polices as-is, or customize them to suit your needs.

## Create Cluster Policy

To create a Cluster Policy:

1. Click Policies in the left navigation and select Cluster Policies.

	<img src="/images/cluster_menu.png" style="max-width:30%;
  height: auto;">

2. Click on Add Cluster Policy.

	<img src="/images/add_cluster_policy.png" style="max-width:50%;
  height: auto;">

	The add cluster policy overlay appears.

	<img src="/images/add_cluster_policy_overlay.png" style="max-width:80%;
  height: auto;">

3. Enter a Name for the new cluster policy.
4. Enter a Description for the new cluster policy.
5. Select Cluster Type from the drop down menu. Options include:

	* Existing Clusters
	* Installed Clusters
	* Managed Clusters (EKS, AKS, GKE)

	Select the cluster type most applicable to the policy you are creating.
	
7. Choose a Cloud Provider from the drop-down list.

	<img src="/images/add_cluster_policy_overlay_edits.png" style="max-width: 80%; height: auto;">
	
8.	Click the Next button. 

9. Select a Kubernetes version for the new cluster policy from the drop down list.
10. Check the box if you wish to Disable Scheduling on Master Nodes.

	<img src="/images/add_cluster_policy_k8version.png" style="max-width:80%; height: auto;">

11. Click the Next button.


12. Choose the cluster add-ons you want applied to the cluster policy by checking the box to the right for each add-on selected.

	<img src="/images/add_cluster_policy_addons.png" style="max-width:80%; height: auto;">
	
13. Click the Finish button to continue.

Nirmata creates the new cluster policy and returns the user to the Cluster Policy Details page.

<img src="/images/new_cluster_policy.png" style="max-width:80%; height: auto;">

**Note:** if Cloud Provider is not specified, Nirmata creates the policy using AWS as the default provider.

**Next steps:** configure the new cluster policy. See [Configuring Cluster Policies](/policies/cluster_policies/configure_policy/) for additional details.
