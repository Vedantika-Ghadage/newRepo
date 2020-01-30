+++
title = "Velero Installation"
description = ""
weight=20
+++

Applications deployed in Kubernetes can be fairly complex and are typically composed of several resources such as - Deployments, Statefulsets, ConfigMaps, Secrets, volumes etc. All of these resources need to be saved so that the application can be completely restored when needed.

Velero (previously known as ARK) is an open source tool that helps automate backup and restore of Kubernetes clusters, including any application and its data.

Velero, has become the de-facto number tool for Kubernetes backup and recovery. Velero is also an incubator project in CNCF and has a vibrant community. To learn more about features and use cases supported by Velero, check out the latest release documentation.

Velero enables the following use cases:

* Disaster recovery - backup of cluster and restore in case of a disaster.
* Application migration - migrate application along with its data from one cluster to another.
* Application cloning - replicating production environments for testing and debugging.

Also, Velero is fully integrated into the Nirmata Kubernetes management plane and available as add-on for every cluster in Nirmata, so that backups can be easily scheduled, and applications can be quickly recovered when needed. 

Nirmata supports Amazon Web Services (AWS), Azure, and Google Cloud Platform (GCP). The next section describes how to create an S3 Bucket on AWS.

## Create AWS Bucket
1. Log in to your AWS account.

2. Click on Amazon S3.

3. Click the Create bucket button. The Create Bucket overlay appears.

	<img src="/images/aws_create_bucket_overlay.png" style="max-width:80%;
  height: auto;">
  
4. Enter a unique Bucket Name.

5. Select the closet Region to your location from the drop down list.

6. To copy settings from an existing bucket:

	1. Click the Select Bucket drop down list.

	2. Click inside the search widget and type the first few letters of an existing bucket. Matching buckets will appear in the list below.

	3. Select an existing bucket from the list to copy its settings.

7. Click the Next button. The overlay transitions to the Configure Options panel.

	<img src="/images/aws_create_bucket_options.png" style="max-width:80%;
  height: auto;">

8. Modify any of the configuration options as required, then click the Next button. The overlay transitions to the Set Permissions panel.

	<img src="/images/aws_create_bucket_permissions.png" style="max-width:80%;
  height: auto;">

9. Do not block any access. Click the Next button. The overlay transitions to the Review panel.

	<img src="/images/aws_create_bucket_review.png" style="max-width:80%;
  height: auto;">
  
10. Review the settings for the new bucket. Click the Previous button to go back and make any changes.

11. Click the Create bucket button to continue.

## Installing Velero

1. To install Velero on a cluster go to the Clusters panel and click on the cluster you wish to configure.

2. Click Add-ons.

	<img src="/images/cluster_addon.png" style="max-width:80%;
  height: auto;">

3. Click the Add button on the right and select Add Velero from the menu.

	<img src="/images/cluster_add_velero.png" style="max-width:50%;
  height: auto;">

4. To create the Velero add-on using AWS:
	1. Select the provider from the drop-down list (AWS in this instance).
	2. Enter an AWS Access key.
	3. Enter an AWS Secret.

	<img src="/images/create_velero_addon.png" style="max-width:80%;
  height: auto;">
  
5. Click Create Add-on to continue or click Cancel to return to the previous page. 

	Kubernetes provides a status for the Velero installation and indicates when it’s complete.
	
6. Click the Close button on the overlay when the installation is completed.

After deploying the Velero add-on you will return to the Add-ons page. You can view Velero's run status from here.

<img src="/images/velero_run_status.png" style="max-width:80%;
  height: auto;">

## Velero Configuration and Setup
Configure Velero by setting up and configuring a Backup Storage Location and setting up a Backup.

### Configure Backup and Storage Location

1. Click velero in the Add-on list.

2. Click Configure Backup and Snapshot Location in the Backup Storage Location section.

	<img src="/images/velero_add_backup_location.png" style="max-width:80%; height: auto;">

	The Add Backup Storage Location overlay appears.

	<img src="/images/velero_add_backup_location_overlay.png" style="max-width:100%; height: auto;">

3. Enter the Name of the Backup Storage and Location. 
4. Select another Region if you wish to change the default selection. 
5. Enter the name of the AWS S3 bucket created earlier in Bucket Name. 
6. Enter a Prefix for the directory that will store your backups. 

	For example, using `prod` as a prefix will place all namespace and cluster backups below the prod directory.

7. Click Add when completed or click Cancel to return to the previous page.

Nirmata displays the newly added Backup Storage and Volume Snapshot Location on the Add-ons page.

<img src="/images/velero_backup_location.png" style="max-width:80%; height: auto;">

You can verify the configuration is correct by reviewing the Backup storage location manifest. 

1. Click the name of the newly created Backup Storage Location under Name. The Storage Location Manifest overlay appears.

	<img src="/images/storage_location_manifest.png" style="max-width:80%; height: auto;">

2. Note the Status section and the `lastSyncedTime`. The presence of a status and timestamp indicates the backup location setup and configuration were completed successfully.

### Create Backup

1. To create backups for the cluster or a cluster namespace click Create Backups on the Backup/Restore Details page.

	<img src="/images/velero_add_backup.png" style="max-width:80%; height: auto;">
	
	The Add Backup overlay appears.
	
	<img src="/images/velero_add_backup_overlay.png" style="max-width:80%; height: auto;">
	
2. Enter a Name for the backup. 
3. Select a Type of backup from the drop down menu: Cluster or Namespace.
4. Click Included Namespaces. 
5. Select default from the Included Namespaces drop down list, or choose a specific namespace as required. 

	**Note:** the Kubernetes and Nirmata namespaces are automatically excluded. Click the x next to a namespace you wish to include in backups.

	Storage Location should be automatically populated using the location created in the previous step (see [Configure Backup and Storage Location](http://docs.nirmata.io/integrations/backup-and-dr/velero/#configure-backup-and-storage-location)). 
	
6. Check Snapshot Volumes if you wish to enable the volume snapshot capability. 
	1. Select your Volume Snapshot Location from the drop-down list. 
	2. Enter key/value pairs for Label Selector. 
	3. Choose the type (String, Number, or Object) from the drop-down list for the key/value pair. 

7. Click Add Item if you wish to enter more key/value pairs. 
8. Enter the number of Hours To Keep or leave the default of 168h0m0s. Use the notation provided in the default if you change this value. 

9. Click Add to complete or click cancel to return to the Back/Restore Details page. 

	The backup should automatically begin, indicated by the Status column of the Backups in the Backup & Restore section of the Add-ons page.

	<img src="/images/new_backup_status.png" style="max-width:80%; height: auto;">

	You will see the status of the newly created backup in the Backup & Restore section of the page. The Status changes to Completed when the backup has finished.

10. Click the name of your backup to open the backup details overlay.

	<img src="/images/backup_details_overlay.png" style="max-width:80%; height: auto;">
	
	Note the Status section indicates a successfully completed backup.
	
11. Click the Close button to return to the Backup/Restore page.

### Schedule Backup

1. To schedule a backup for a cluster or namespace click Schedules on the Backup/Restore Details page.

	<img src="/images/velero_schedule_backup.png" style="max-width:60%; height: auto;">
	
	The Add Schedule overlay appears.
	
	<img src="/images/backup_add_schedule_overlay.png" style="max-width:100%; height: auto;">
	
2. Enter a Name for the scheduled backup.
3. Select a Type of scheduled backup from the drop down menu: Cluster or Namespace.
4. Schedule uses standard [cron notation](https://en.wikipedia.org/wiki/Cron#Overview). Set your backup schedule to occur at the time and on the days of your choosing.
5. Select default from the Included Namespaces drop down list, or choose a specific namespace as required. 

	**Note:** the Kubernetes and Nirmata namespaces are automatically excluded. Click the x next to a namespace you wish to include in backups.

	Storage Location should be automatically populated using the location created in the previous step (see [Configure Backup and Storage Location](http://docs.nirmata.io/integrations/backup-and-dr/velero/#configure-backup-and-storage-location)).
	
6. Check Snapshot Volumes if you wish to enable the volume snapshot capability. 
7. Select your Volume Snapshot Location from the drop-down list. It should be the same as Storage Location. 
8. Enter the number of Hours To Keep or leave the default of 168h0m0s. Use the notation provided in the default if you change this value. 
9. Click Add to complete or click Cancel to return to the Backup/Restore Details page.

	The newly added backup schedule appears in the Backup section of the Backup/Restore Details page.

	<img src="/images/scheduled_backup.png" style="max-width:80%; height: auto;">

	Note the scheduled backup's attributes listed on the screen: 

	* Schedule
	* Last Backup	
	* Status

	Status should indicate *Enabled*.	
	
10. Click the name of your scheduled backup to open the scheduled backup details overlay.

	<img src="/images/scheduled_backup_details_overlay.png" style="max-width:80%; height: auto;">

	Note the Status section at the bottom indicating the time of last backup and state of the schedule, which should be *Enabled.*