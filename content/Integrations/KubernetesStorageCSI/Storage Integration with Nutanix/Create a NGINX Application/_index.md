+++
title = "Create a NGINX Application"
description = ""
weight=60
+++
{{%excerpt%}}

First, create a secret for the connection to and from Nutanix and the cluster. 

To Create a SSH into the Kubernetes Master Node, open a text editor to create the file for the secret.
Copy and paste the following code into the file:

```
apiVersion: v1
kind: Secret
metadata:
 name: ntnx-secret
 namespace: default
data:
 # base64 encoded prism-ip:prism-port:admin:password.
 # E.g.: echo -n "10.6.47.155:9440:admin:mypassword" | base64
 key: MTAuNS42NS4xNTU6OTQ0MDphZG1pbjpOdXRhbml4LjEyMw==
```

Make the following replacements in the code:

1. Replace prism-ip with the Cluster Virtual IP Address. If a Cluster Virtual IP Address is not configured replace prism-ip with the virtual IP address of any Controller VM in the cluster.  
2. Replace prism-port with the corresponding port.  
3. Replace admin_name with the name used for the admin role.  
4. Replace password with the password for the admin role.  
 
Next, create a Nutanix ACS-ABS storage class.

To create a Nutanix ACS-ABS storage class, open the cluster and select *Storage Class* from the Resources window. 

![image](/images/nutanix-6.png)

Then, click the gear in the top right corner and select *+Add Storage Class*.

![image](/images/nutanix-7.png)

Complete the information in the pop-up window and click *Add*.

![image](/images/nutanix-8.png)

To create and configure the NGINX application, add the NGINX YAML to the *Application Catalog*.  

Select on *Catalog* in the sidebar menu and then select *Application Catalog*. From the main Application Catalog screen, click *Add Application*. 

Drop the NGINX YAML file into the upload  box or select the file from the directory. 

**NGINX YAML:**

```
apiVersion: apps/v1
kind: Deployment
metadata:
 name: server
spec:
 replicas: 1
 selector:
   role: server
 template:
   metadata:
     labels:
       role: server
   spec:
     containers:
     - name: server
       image: nginx
       volumeMounts:
         - mountPath: /var/lib/www/html
           name: mypvc
     volumes:
       - name: mypvc
         persistentVolumeClaim:
           claimName: claim1
```

Next, configure the PVC information on the application by selecting the application, and then *Config & Storage*.  

![image](/images/nutanix-9.png)

Select the Persistent Volume Claim and make the necessary edits.

![image](/images/nutanix-10.png)

Finally, deploy and view the PVC on the Kubernetes cluster and the Nutanix cluster.

{{%/excerpt%}}