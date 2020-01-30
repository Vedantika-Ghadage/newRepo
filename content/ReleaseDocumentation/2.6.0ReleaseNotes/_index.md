+++
title = "2.6.0 Release Notes"
description = ""
weight=50
+++

#### What's New in Nirmata 2.6.0

* [Environmental Management Enhancements](https://docs.nirmata.io/environments/addnewenvironment/)
* [Cluster Resource Viewing](https://docs.nirmata.io/clusters/view_cluster_resources/)
* [Cluster Level Add-ons](https://docs.nirmata.io/clusters/cluster_level_addon/)
* [Cluster Level Prometheus](https://docs.nirmata.io/clusters/cluster_level_prometheus/)
* [Add-on Enhancements](https://docs.nirmata.io/clusters/cluster_policies/apply_addon/)
* [Network Policies](https://docs.nirmata.io/policies/network_policy/)
* [Environment Panel Organization](https://docs.nirmata.io/environments/environmentalpanel/)
* [Cluster Panel Organization](https://docs.nirmata.io/clusters/cluster_panel/)
* [Alarm Panel Organization](https://docs.nirmata.io/alarms/alarm_panel/)
* [Jira Change Management Integration](https://docs.nirmata.io/integrations/jirachangemanagement/)
* [High Availability Cluster Enhancement](https://docs.nirmata.io/clusters/high_availability_ha_clusters/)
* [Synchronize Unmanaged Namespaces](https://docs.nirmata.io/settings/synch_unmanaged_namespaces/)

#### Fixes

* Show activity around this time' link does not display activity data's for 5hrs and above old activities.
* Alarm clear not discernible from web hook notification
* Duplicate alarms are created sometimes
* scope information not available in web hook notification
* Add HPA form doesn't show Stateful Sets in the Target drop-down menu
* Add support for dynamic tunnels
* After rebooting devtest2 host, nirmata-kube-controller keeps connecting/disconnecting
* Agent cannot reconnect after wss timeout
* AKS cluster is not getting created in production
* AKS Kubernetes Version is hard coded
* AKS regions are hard coded
* Alarm notification emails contain incorrect user in Last Modified by field
* Application clone does not work
* Backend allows Duplicate alarms to be added.
* Cannot delete an environment in devtest
* Cannot scale activity service
* check if cert/key directories are correct
* Check the content of cert/key, needs to be base64 encoded
* Cluster & Environments services failed to connect to ProSoft qa-cluster
* Cluster activity is showing global activity also.(in devtest2)
* ContainerVMSizeTypes is hardcoded in a class
* Creation of AKS provider managed cluster was failed.(in production account)
* Crumbs don't render in the container template view (Uncaught TypeError)
* Deployment in "Unknown" state when pods are running
* EKS cluster created but not connected.
* Email notifications are sent for disabled alarms
* Enable alarm option is Blocked
* Endpoint label mismatch
* Environment name should allow "-"
* Environment name should not allow space.
* Environment shows Cluster Connect Status for a Disabled cluster
* Existing logic for selecting a workload controller doesn't work properly in case of Jobs
* HA testing causes SaaS deployment to hangup when bringing back 2 nodes out of 3
* If we try to retrieve more activity data same data's are being repeated.
* Improve events viewer
* Inconsistent arrangement of cards
* incorrect validation error for EnVars using configmap keys or secrets
* Informational alarms are emails but filter was set to Critical
* Invalid configuration is generated for EKS cluster
* Invalid DNS name is shown on the Pod
* Jira settings must be visible only in GA2 accounts, not in GA accounts
* Jobs that has been created by a Cron Job are showing as Active in the UI, even though they're completed
* Links in the drop-down menu for Jobs and Cron Jobs (in crumbs) are not working
* Login to Nirmata intermittently fails
* nadm - add a "local-storage" command or use a dynamic hostpath provisioner
* nadm config path incorrect
* nadm scale orchestrater scaled down all services
* nadm should reserve resources for kubernetes components when deploying nirmata
* namespace discovery does works for the shopme deals deployment
* nirmata agent crash on startup
* Not able to add aws Hostgroup in devtest2.
* NullPointerException when applying ResourcePatch
* One task fails during the creation of a managed cluster on aws: failed to apply ingress controller yaml
* Pod template labels are not rendering in the Cron Job view
* Pod yaml is not loaded and the dialog just shows Fetching..
* Possible multi-tenancy issue
* Progress bar is showing only 10% while creating discovered cluster.(devtest)
* registrycreation in pending state
* Render a Workload Controller info for job pods and cron job pods in PodSummaryTabview
* Reserve resources for kubernetes containers and system services when deploying cluster
* Rest api call to fetch the AKS maximum node count associated with VM size
* Retain more logs and events (for prod environments)
* Service versions are incorrect
* signing up with google account using an already existing email doesn't work
* Some tunnel connections were down
* State of applications takes long to update in Catalog view after adding or deleting an application (in production)
* the new buildnotify API doesn't work
* Tunnel Client - add support for dynamic tunnels
* UI - Pods appear in the application that it doesn't belong to
* Unable to generate API key in devtest2,getting 401 error.
* Uncaught type error in the Running Cron Job view (active crumb doesn't show up)
* Update curator to 4.2.0 to potentially solve the problem of locks piling up.
* Use Kustomize for YAML customizations
* User is able to Delete cloud provider with connected HostGroup and Cluster
* Vault secrets should work when put in root directory
* When nirmata pods are edited, anti-affinity of required v/s preferred stops pods from running
* When running two applications in a shared namespace, failure notification of one application show in another.
* Duplicate aarm types are allowed - causing processing errors
* Failed to deploy Rook - Ceph
* addRelationList function adds an extra line that shouldn't be added
* An asterisk sign is required for 'Amazon Machine Image (AMI) Id' field in the Settings-tab of Host Group.
* An asterisk sign is required for 'Instance Type' field in the Settings-tab of Host-Group.
* An error message displayed as "An Image is required" rather than 'Amazon Machine Image (AMI) Id is required' in the UserData-tab of the Host Groups.
* Application catalog should not allow application run name to have space
* Do not allow spaces in application run name
* environments service on master branch doesn't start after changing the model
* Issue with etcd components on Dev server again
* Patch policy is not applied when a change is made in the catalog
* Pods created by Prometheus operator are not discovered
* Application catalog should not allow application run name to have space
* Issue with etcd components on Dev server again
* Deployment in "Unknown" state when pods are running
* Endpoint label mismatch
* Retain more logs and events (for prod environments)
* signing up with google account using an already existing email doesn't work
* Vault secrets should work when put in root directory
* When nirmata pods are edited, anti-affinity of required v/s preferred stops pods from running
* Nirmata not coming up - after kubelet shutdown
* Nirmata UI having issue while bringing up controller service
* "Host not connected" on Nirmata while server looks good
* Cluster Service throw error - failing to create/update the node
* Vault Integration: Data not populated when Vault is enabled for the cluster
* kubectl commands sometimes fail
* Controller yaml issue
* 90 days of audit history
* NIBR aqua scan - fix file permissions
* Check when deleting catalog application
* Environment Services did not come up properly after bringing down 2 out of 3 master nodes in base cluster
* For a deployed application registry always points to dockerhub
* Nadm Restore Logic
* direct connect nodes in unknown status
* Vault secrets should use EmptyDir instead of hostpath
* Vault secrets should work when put in root directory
* Changes to catalog are not reflecting after push
* Issue with etcd components on Dev server again

#### Known Issues

* Security & webclient status servlets are throwing exception (sometimes)
* Login for SAML login is broken in 2.6.1
