+++
title = "Storage Integration with Nutanix"
description = ""
weight=20
+++
{{%excerpt%}}
##### Introduction

Nutanix provides an external volume plug-in for Kubernetes. Kubernetes is an open source platform for automating deployment, scaling, and operation of application containers across a cluster of hosts. This cluster of hosts can be made up of cloud provider VM instances, Nutanix-hosted VMs, or bare metal servers. Kubernetes is formed with multiple VMs and a master node.

This plug-in runs in a pod and dynamically provisions requested persistent volume that is compatible with the Kubernetes iSCSI volume. Nutanix then provides persistent storage for the provisioned volume.

Storage classes also have provisioners which determine which volume plugin should be used for provisioning Persistent Volumes.
Read more about Nutanix with Kubernetes (here)[https://portal.nutanix.com/#/page/docs/details?targetId=Kubernetes-Volume-Plug-In-v10:Kubernetes-Volume-Plug-In-v10].

##### Prerequesisites

1. Nirmata Cluster with Kubernetes 1.10+, minimum 1 node in a cluster ( We are using Kubernetes version 1.10.8 with 6 nodes). 
2. Nutanix CE version 5.5 and later  
3. iSCSI OS plugin  
••1. Centos: iscsi-initiator-utils  
••2. Ubuntu: open-iscsi  
••3. All worker nodes must have the same iSCSI initiator in /etc/iscsi/initiatorname.iscsi

##### Goal and Key Steps for Integration

The goal of integrating Nutanix with Nirmata is to provide an option for dynamically provisioned persistent volumes with the Kubernetes iSCSI volumes.

1. Register at Nutanix for CE edition or use try now to deploy Nutanix. 
•• 1. Using their own instance’s for integration
2. Deploy StatefulSet and DaemonSet using YAML files
3. Manage storage
4. Create a sample application and create a persistent volume claim

##### Deploy RBAC YAML to Cluster

To deploy the RBAC YAML to a cluster, open the cluster and then select *Apply YAML* from the Cluster Settings menu.  

![image](/images/nutanix-1.png)

Drop the RBAC YAML file into the upload  box or select the file from the directory. 

![image](/images/nutanix-2.png)  

**RBAC YAML:**  

```
---
apiVersion: v1
kind: ServiceAccount
metadata:
 name: csi-attacher
 namespace: kube-system
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: external-attacher-runner
 namespace: kube-system
rules:
 - apiGroups: [""]
   resources: ["secrets"]
   verbs: ["get", "list"]
 - apiGroups: [""]
   resources: ["events"]
   verbs: ["get", "list", "watch", "update"]
 - apiGroups: [""]
   resources: ["persistentvolumes"]
   verbs: ["get", "list", "watch", "update"]
 - apiGroups: [""]
   resources: ["nodes"]
   verbs: ["get", "list", "watch"]
 - apiGroups: ["storage.k8s.io"]
   resources: ["volumeattachments"]
   verbs: ["get", "list", "watch", "update"]

---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: csi-attacher-role
 namespace: kube-system
subjects:
 - kind: ServiceAccount
   name: csi-attacher
   namespace: kube-system
roleRef:
 kind: ClusterRole
 name: external-attacher-runner
 apiGroup: rbac.authorization.k8s.io

---
# needed for StatefulSet
kind: Service
apiVersion: v1
metadata:
 name: csi-attacher-ntnx-plugin
 namespace: kube-system
 labels:
   app: csi-attacher-ntnx-plugin
spec:
 selector:
   app: csi-attacher-ntnx-plugin
 ports:
   - name: dummy
     port: 12345
---
apiVersion: v1
kind: ServiceAccount
metadata:
 name: csi-provisioner
 namespace: kube-system
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: external-provisioner-runner
 namespace: kube-system
rules:
 - apiGroups: [""]
   resources: ["secrets"]
   verbs: ["get", "list"]
 - apiGroups: [""]
   resources: ["persistentvolumes"]
   verbs: ["get", "list", "watch", "create", "delete"]
 - apiGroups: [""]
   resources: ["persistentvolumeclaims"]
   verbs: ["get", "list", "watch", "update"]
 - apiGroups: ["storage.k8s.io"]
   resources: ["storageclasses"]
   verbs: ["get", "list", "watch"]
 - apiGroups: [""]
   resources: ["events"]
   verbs: ["list", "watch", "create", "update", "patch"]
  
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: csi-provisioner-role
 namespace: kube-system
subjects:
 - kind: ServiceAccount
   name: csi-provisioner
   namespace: kube-system
roleRef:
 kind: ClusterRole
 name: external-provisioner-runner
 apiGroup: rbac.authorization.k8s.io
---
# needed for StatefulSet
kind: Service
apiVersion: v1
metadata:
 name: csi-provisioner-ntnx-plugin
 namespace: kube-system
 labels:
   app: csi-provisioner-ntnx-plugin
spec:
 selector:
   app: csi-provisioner-ntnx-plugin
 ports:
   - name: dummy
     port: 12345
---
apiVersion: v1
kind: ServiceAccount
metadata:
 name: csi-ntnx-plugin
 namespace: kube-system
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: csi-ntnx-plugin
 namespace: kube-system
rules:
 - apiGroups: [""]
   resources: ["secrets"]
   verbs: ["get", "list"]
 - apiGroups: [""]
   resources: ["nodes"]
   verbs: ["get", "list", "update"]
 - apiGroups: [""]
   resources: ["namespaces"]
   verbs: ["get", "list"]
 - apiGroups: [""]
   resources: ["persistentvolumes"]
   verbs: ["get", "list", "watch", "update"]
 - apiGroups: ["storage.k8s.io"]
   resources: ["volumeattachments"]
   verbs: ["get", "list", "watch", "update"]
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: csi-ntnx-plugin
 namespace: kube-system
subjects:
 - kind: ServiceAccount
   name: csi-ntnx-plugin
   namespace: kube-system
roleRef:
 kind: ClusterRole
 name: csi-ntnx-plugin
 apiGroup: rbac.authorization.k8s.io    

```

##### Deploy the Attacher, Node, and Provisioner YAMLs

To deploy the each YAML to a cluster, open the cluster and then select Apply YAML from the Cluster Settings menu.

![image](/images/nutanix-3.png)

Drop the YAML file into the upload  box or select the file from the directory. 

![image](/images/nutanix-4.png)

**Attacher YAML:**  

```

kind: StatefulSet
apiVersion: apps/v1beta1
metadata:
 name: csi-attacher-ntnx-plugin
 namespace: kube-system
spec:
 serviceName: "csi-attacher-ntnx-plugin"
 replicas: 1
 template:
   metadata:
     labels:
       app: csi-attacher-ntnx-plugin
   spec:
     serviceAccount: csi-attacher
     containers:
       - name: csi-attacher
         image: quay.io/k8scsi/csi-attacher:v0.2.0
         args:
           - "--v=5"
           - "--csi-address=$(ADDRESS)"
         env:
           - name: ADDRESS
             value: /var/lib/csi/sockets/pluginproxy/csi.sock
         imagePullPolicy: "IfNotPresent"
         volumeMounts:
           - name: socket-dir
             mountPath: /var/lib/csi/sockets/pluginproxy/
       - name: nutanix-csi-plugin
         image: ntnx/ntnx-csi:beta2
         args :
           - "--nodeid=$(NODE_ID)"
           - "--endpoint=$(CSI_ENDPOINT)"
         env:
           - name: CSI_ENDPOINT
             value: unix:///var/lib/csi/sockets/pluginproxy/csi.sock
           - name: NODE_ID
             valueFrom:
               fieldRef:
                 fieldPath: spec.nodeName
         volumeMounts:
           - name: socket-dir
             mountPath: /var/lib/csi/sockets/pluginproxy/
     volumes:
       - name: socket-dir
         emptyDir: {}
```

**Node YAML:**

```
kind: DaemonSet
apiVersion: apps/v1beta2
metadata:
 name: csi-ntnx-plugin
 namespace: kube-system
spec:
 selector:
   matchLabels:
     app: csi-ntnx-plugin
 template:
   metadata:
     labels:
       app: csi-ntnx-plugin
   spec:
     serviceAccount: csi-ntnx-plugin
     hostNetwork: true
     containers:
       - name: driver-registrar
         image: quay.io/k8scsi/driver-registrar:v0.2.0
         args:
           - "--v=5"
           - "--csi-address=$(ADDRESS)"
         env:
           - name: ADDRESS
             value: /csi/csi.sock
           - name: KUBE_NODE_NAME
             valueFrom:
               fieldRef:
                 fieldPath: spec.nodeName
         volumeMounts:
           - name: plugin-dir
             mountPath: /csi/
             # TODO: the registrar is not implemented yet
             # - name: registrar-socket-dir
             #   mountPath: /var/lib/csi/sockets/
       - name: csi-ntnx-plugin
         securityContext:
           privileged: true
           allowPrivilegeEscalation: true
         image: ntnx/ntnx-csi:beta2
         args :
           - "--endpoint=$(CSI_ENDPOINT)"
           - "--nodeid=$(NODE_ID)"
         env:
           - name: CSI_ENDPOINT
             value: unix:///csi/csi.sock
           - name: NODE_ID
             valueFrom:
               fieldRef:
                 fieldPath: spec.nodeName
         volumeMounts:
           - name: plugin-dir
             mountPath: /csi
           - name: pods-mount-dir
             mountPath: /var/lib/kubelet
             # needed so that any mounts setup inside this container are
             # propagated back to the host machine.
             mountPropagation: "Bidirectional"
           - mountPath: /dev
             name: device-dir
           - mountPath: /etc/iscsi
             name: iscsi-dir
           - mountPath: /sbin/iscsiadm
             name: iscsiadm
           - mountPath: /lib/modules
             name: lib-dir
     volumes:
       # TODO: the registar is not implemented yet
       #- name: registrar-socket-dir
       #  hostPath:
       #    path: /var/lib/kubelet/device-plugins/
       #    type: DirectoryOrCreate
       - name: plugin-dir
         hostPath:
           path: /var/lib/kubelet/plugins/com.nutanix.csi
           type: DirectoryOrCreate
       - name: pods-mount-dir
         hostPath:
           path: /var/lib/kubelet
           type: Directory
       - name: device-dir
         hostPath:
           path: /dev
       - name: iscsi-dir
         hostPath:
           path: /etc/iscsi
       - name: iscsiadm
         hostPath:
           path: /sbin/iscsiadm
       - name: lib-dir
         hostPath:
           path: /lib/modules

```

**Provisioner YAML:**

```
kind: StatefulSet
apiVersion: apps/v1beta1
metadata:
 name: csi-provisioner-ntnx-plugin
 namespace: kube-system
spec:
 serviceName: "csi-provisioner-ntnx-plugin"
 replicas: 1
 template:
   metadata:
     labels:
       app: csi-provisioner-ntnx-plugin
   spec:
     serviceAccount: csi-provisioner
     containers:
       - name: csi-provisioner
         image: quay.io/k8scsi/csi-provisioner:v0.2.0
         args:
           - "--provisioner=com.nutanix.csi"
           - "--csi-address=$(ADDRESS)"
           - "--v=5"
         env:
           - name: ADDRESS
             value: /var/lib/csi/sockets/pluginproxy/csi.sock
         imagePullPolicy: "IfNotPresent"
         volumeMounts:
           - name: socket-dir
             mountPath: /var/lib/csi/sockets/pluginproxy/
       - name: nutanix-csi-plugin
         image: ntnx/ntnx-csi:beta2
         securityContext:
           privileged: true
           allowPrivilegeEscalation: true
         args :
           - "--endpoint=$(CSI_ENDPOINT)"
           - "--nodeid=$(NODE_ID)"
         env:
           - name: CSI_ENDPOINT
             value: unix:///var/lib/csi/sockets/pluginproxy/csi.sock
           - name: NODE_ID
             valueFrom:
               fieldRef:
                 fieldPath: spec.nodeName
         volumeMounts:
           - name: socket-dir
             mountPath: /var/lib/csi/sockets/pluginproxy/
     volumes:
       - name: socket-dir
         emptyDir: {}
```

##### Verify RABC, Attacher, Node, and Provisioner YAMLs are Deployed

To verify that the YAMLs are deployed, run a Kubectl command from the cluster shell. 

To run a Kubectl command, open the Cluster Settings menu and select Launch Terminal. 

If all YAMLs are deployed, the Kubectl report will be similar to the one shown below.

![image](/images/nutanix-5.png)


##### Create a NGINX Application


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
