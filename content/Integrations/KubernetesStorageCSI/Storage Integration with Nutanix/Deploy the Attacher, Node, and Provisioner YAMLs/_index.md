+++
title = "Deploy the Attacher, Node, and Provisioner YAMLs"
description = ""
weight=50
+++

{{%excerpt%}}

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

{{%excerpt%}}