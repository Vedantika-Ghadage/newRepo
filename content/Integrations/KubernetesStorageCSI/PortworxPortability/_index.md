+++
title = "Application Portability with PortWorx"
description = ""
weight=30
+++
{{%excerpt%}}

#### Introduction

Portworx is a tool to leverage persistent data in containers. It is multi-cloud ready and manages persistent volumes, high availability, and data security. 

Click here to learn more about [Portworx](https://portworx.com).

#### Prerequisites

##### Key-Value Store
Portworx uses a key-value store for clustering metadata. This integration example utilizes the default etcd.

##### Storage
Ensure that at least one of the Portworx nodes has extra storage available. Use an unformatted partition or a disk-drive.

Storage devices explicitly given to Portworx are automatically formatted by Portworx. Before integrating Nirmata with Portworx, add an unused disk on each worker node of the same size and confirm that the mount point is /dev/sd*).

##### Shared Mounts
If running Docker v1.12, Docker must be configured to allow shared mounts propagation. If not, Portworx will fail to start.

[Click here for instructions on configuring Docker v1.12 to allow shared mounts propagation](https://docs.portworx.com/knowledgebase/shared-mount-propagation.html).

##### Firewall
Ensure that ports 9001-9015 are open between the nodes that will run Portworx.

##### NTP
Ensure that all nodes running Portworx are time-synchronized and that an NTP service is configured and running.

#### Goal and Key Steps for Integration

The goal of integrating Nirmata with Portworx is to provide complete application portability across clusters in multi-cloud environments.

#### Create a Kubernetes DaemonSet

Before integrating Portworx with Nirmata, deploy Portworx in the Kubernetes Cluster. 

[Click here for instructions on deploying Portworx in a Kubernetes Cluster.](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

#### Setup the Kubernetes Cluster through Nirmata

To begin the integration with Nirmata, setup a Cloud Provider, Host Group, and Cluster in Nirmata.

1. [Click here for instructions on setting up a Cloud Provider.](https://docs.nirmata.io/en/latest/CloudProviders.html)
2. [Click here for instructions on setting up a container Host Group.](https://docs.nirmata.io/en/latest/HostGroups.html)
3. [Click here for instructions on setting up a Kubernetes Cluster.](https://docs.nirmata.io/en/latest/Clusters.html)

Note: This example utilizes Microsoft Azure as Cloud Provider.

When setup is complete, the Kubernetes cluster will display:

![image](/images/portworx-1.png)

#### Generate and Download a Portworx Spec File

To create a Portworx Spec File, use the Portworx Spec Generator for the appropriate Portworx version.

[Click here to access all available Portworx Spec Generators.](https://docs.portworx.com/scheduler/kubernetes/install.html#install)

The Portworx Spec Generator steps through the process and requests information at each step. 

Start by entering the Kubernetes version, selecting an etcd, and a region. 

![image](/images/portworx-2.png)

Then select a Cloud Provider and cloud-provider specific details.

![image](/images/portworx-3.png)

Next, complete the network data based on the appropriate interface devices. 

![image](/images/portworx-4.png)

Finally, select customization options and click *Finish*.

![image](/images/portworx-5.png)

![image](/images/portworx-6.png)

The Portworx Spec Generator creates a spec URL. Download the spec file. The spec file downloads a YAML.

![image](/images/portworx-7.png)

#### Deploy the Portworx Spec File in Nirmata

Deploy the Portworx Spec File within Nirmata. 

Note that each configuration is different and that the devices used and network and management interfaces will vary based on the configuration.

To deploy the  Portworx Spec File via Nirmata, open the Nirmata terminal and enter the  Create YAML File command.

**Create YAML File Command:**
```
vi spec.yaml.
```

Save the contents of the  Portworx Spec File into the new file and deploy the YAML using a Deploy Kubectl Command.

**Deploy Kubectl Command:**
```
kubectl apply -f spec.yaml 
```

Allow a few minutes for the Portworx Spec File to setup. Then, SSH into any one of the worker nodes and run a Status Command.

**Status Command:**
```
 sudo /opt/pwx/bin/pxctl status
```

When properly configured in a two-disk setup, the following results will display: 

![image](/images/portworx-8.png)

#### Deploy a Wordpress & MySQL Database Using Kubernetes in Portworx

This example explains how to deploy a WordPress site and a MySQL database using Kubernetes. 

Portworx solves two critical issues for running WordPress in containers:
1. Running a high performance, HA MySQL database 
2. Using shared volumes for file uploads

By combining these two Portworx features with a Kubernetes cluster, the WordPress instance:

* automatically replicates the MySQL data for HA
* horizontally scales the WordPress PHP container using multi-writer semantics for the file-uploads directory
* automatically repairs itself in the event of a node failure

*This example utilizes Kubernetes storage primitives PersistentVolumes (PV) and PersistentVolumeClaims (PVC).*

*The spec files provided in this example are based on beta deployment APIs and are specific to Kubernetes versions 1.8 and above. To adapt this example to an earlier version of Kubernetes, update the beta API appropriately or reference earlier versions of Kubernetes.*

##### Create a Nirmata Environment

To begin, create an Environment in Nirmata.

Select  Environment from the sidebar menu. Then click, *+Add Environment* and complete the information in the pop-up window. Click *Add*. 

![image](/images/portworx-9.png)

The new environment appears in the *Environments* list. 

The MySQL/WordPress services will deploy in this Environment.

##### Create Storage Classes

Next, setup a storage class and replica pool based on the Environment.

Open the cluster and select *Storage Class* from the Resources menu.

![image](/images/portworx-10.png)

Select *+Add Storage Class*.

![image](/images/portworx-11.png)

Set the repl level from one to three, based on the Environment. 
Name the Storage Class, select a Provisioner and set the Reclaim Policy to *Delete*.

Note that there is no volume mount.

Click *Save*.

![image](/images/portworx-12.png)

##### Create a MySQL Application

To create a new MySQL Application, utilize the MySQL YAML template. Adjust the template as needed. Remember to replace �password� with a secure keyref.

**MySQL YAML Template:**
```
apiVersion: v1
kind: Service
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  clusterIP: None
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: mysql
    spec:
      # Use the stork scheduler to enable more efficient placement of the pods
      schedulerName: stork
      containers:
      - image: mysql:5.6
        imagePullPolicy: 
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pvc-1
```

To add the MySQL YAML to the Application Catalog, click on *Catalog* in the sidebar menu and then select *Application Catalog*. From the main Application Catalog screen, click *Add Application*. 

![image](/images/portworx-13.png)

Drop the MySQL YAML file into the upload  box or select the file from the directory. 

![image](/images/portworx-14.png)

Click *Create*. Once created, the MySQL application is listed in the Nirmata Application Catalog.

##### Add Persistent Volume Claims to the MySQL Application

Next, add the Persistent Volume Claims (PVC) to the MySQL Application. 

Open the newly created MySQL Application in Nirmata by selecting *Catalog* from the sidebar menu and then Applications. 

Click on the MySQL application in the Application List. Then open the *Config & Storage* dashboard.

Click + in the Persistent Volume Claims window to add a new PVC.

![image](/images/portworx-15.png)

Complete the information in the Edit Persistent Volume Claim setup box.

![image](/images/portworx-16.png)

##### Deploy the MySQL Application to the Environment

To run the MySQL Application in the Nirmata Environment, click on Environments in the sidebar menu. 

Then open the newly created Environment. Click the gear in the top right corner of the Environments window and select the *+Run an Application* option. 

Choose the MySQL Application and click *+Run an Application*.

![image](/images/portworx-17.png)

##### Create a Wordpress Application

To create a new WordPress Application, utilize the WordPress YAML template. Adjust the template as needed. Remember to replace �password� with a secure keyref.

**WordPress YAML Template:**

```
apiVersion: v1
kind: Service
metadata:
 name: wordpress
 labels:
   app: wordpress
spec:
 ports:
   - port: 80
     nodePort: 30303
 selector:
   app: wordpress
   tier: frontend
 type: NodePort
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
 name: wordpress
 labels:
   app: wordpress
spec:
 replicas: 3
 strategy:
   type: Recreate
 template:
   metadata:
     labels:
       app: wordpress
       tier: frontend
   spec:
     # Use the stork scheduler to enable more efficient placement of the pods
     schedulerName: stork
     containers:
     - image: wordpress:4.8-apache
       name: wordpress
       imagePullPolicy:
       env:
       - name: WORDPRESS_DB_HOST
         value: wordpress-mysql
       - name: WORDPRESS_DB_PASSWORD
         value: password
       ports:
       - containerPort: 80
         name: wordpress
       volumeMounts:
       - name: wordpress-persistent-storage
         mountPath: /var/www/html
     volumes:
     - name: wordpress-persistent-storage
       persistentVolumeClaim:
         claimName: wp-pv-claim
```

To add the WordPress YAML to the Application Catalog, click on *Catalog* in the sidebar menu and then select Application Catalog. From the main *Application Catalog* screen, click *Add Application*. 

![image](/images/portworx-18.png)

Drop the WordPress YAML file into the upload  box or select the file from the directory.

![image](/images/portworx-19.png)

Click *Create*. Once created, the WordPress application is listed in the Nirmata Application Catalog.

##### Add Persistent Volume Claims to the WordPress Application

Next, add the Persistent Volume Claims (PVC) to the WordPress Application. 

Open the newly created WordPress Application in Nirmata by selecting *Catalog* from the sidebar menu and the Applications. 

Click on the WordPress application in the Application List. Then open the *Config & Storage* dashboard.

Click + in the Persistent Volume Claims window to add a new PVC.

![image](/images/portworx-20.png)

##### Deploy the WordPress Application

To run the WordPress Application in the Nirmata Environment, click on Environments in the sidebar menu. 

Then open the newly created Environment. Click the gear in the top right corner of the Environments window and select the *+Run an Application* option. 

Choose the WordPress Application and click *+Run an Application*.

![image](/images/portworx-21.png)

#### Verify the Application is Running in the Terminal and on the Nirmata Dashboard

To verify that the application is running in the terminal, open the Environment and select the the environment name, then the application name, and finally, the pod name.

From the *Running Containers* list, select the container name (mysql). Click the gear in the top right corner of the window and select the *Launch Terminal* option.

The displayed command is *sh*. Do not change the command. Select *Connect Terminal*.

In the terminal window, enter the Verify Status Commands in the Nirmata Terminal.

**Verify Status Commands:**
```
kubectl get pods
kubectl get services wordpress
```

![image](/images/portworx-22.png)

To verify the application is running from the Nirmata dashboard, select *Clusters* from the sidebar menu.

The WordPress application and the MySQL application will display as green and *Running*.

![image](/images/portworx-23.png)

#### Clean Up Integration

Delete the secret for MySQL by entering the Delete Secret for MySQL command in the terminal window.

**Delete Secret for MySQL Command:**

```
kubectl delete secret mysql-pass
```

Delete WordPress by entering the Delete WordPress command in the terminal window.

**Delete WordPress Command:**

```
kubectl delete -f wordpress-deployment.yaml
kubectl delete -f wordpress-vol.yaml
```

Delete MySQL for WordPress by entering the Delete MySQL for WordPress command in the terminal window.

**Delete MySQL for WordPress Command:**

```
kubectl delete -f mysql.yaml
kubectl delete -f mysql-vol.yaml
```

Note: Portworx PersistentVolume allows for the creation of the Deployments and Services at this point without losing data. However, the hostPath will lose the data as soon as the Pod stops running.

#### Application Portability Steps

The use case for application portability between Nirmata and Portworx requires the following:

1. Demonstrate an application created in a shared Nirmata environment (namespace) tied to an infrastructure (private cloud) using dynamically provisioned PVCs for a sample application (MySQL).
2. Demonstrate single-click application migration using Nirmata *clone application button*.
3. This action triggers migration of application YAML to a different environment tied to different infrastructure (public cloud) with an associated namespace.
4. On the storage side, this triggers a backup of associated PVCs and volumes to an S3 object-store in the destination cloud.
5. The logic recreates persistent volumes.
6. The application clone logic statically configures the PVCs and PVs based on data from the application deployed in the first cluster.

{{%/excerpt%}}
