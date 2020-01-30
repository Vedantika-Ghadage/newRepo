+++
title = "VMWare vCloud Director Kubernetes extension"
description = ""
weight=150
+++


### Introduction

The Nirmata Kubernetes Extension for vCloud Director (VCD) enables Service Providers and Tenants to manage Kubernetes clusters using VCD Web UI.

### Prerequisites

1. vCloud Director (version 9.0+).
2. Rabbit MQ.
3. Container Services Extension (CSE v2.5.0) (https://vmware.github.io/container-service-extension).
4. Nirmata Kubernetes Extension (client and server extensions).


#### Nirmata Cloud Edition (nirmata.io) Installation

##### Prerequisites

Follow the instructions to install the Container Services Extension and verify that it is working. Download the Nirmata Kubernetes Extension UI plugin and the container image.

##### Nirmata.io Account Creation

A Nirmata integration account is required to to integrate with the VMWare CSE with Nirmata. Please send an email to customersuccess@nirmata.com with your email id to get a tenant created. Nirmata shall get back to you within a few hours with your tenant and account information. Use this account information in the next steps to set up the integration with vCD and VMWare CSE.   

##### Nirmata Extension installation

Nirmata Kubernetes Extension can be installed on any node that has docker engine running. It can be installed on the same node as RabbitMQ or CSE.

Before starting the extension, create the following folders:
```
/nirmata-ext                           (parent folder)
/nirmata-ext/vcd-ext-db         (stores db)
/nirmata-ext/vcd-config          (stores config file)
```

In /nirmata-ext/vcd-config, create a config file: nirmata-vcd-ext.yaml with the following:
vcd:
```

 host: <vcd-address>
 username: <vcd-username>
 password: <vcd-password>
rabbitmq:
 host: <rabbitmq-host>
 username: <rabbitmq-username>
 password: <rabbitmq-password>
nirmata:
 url: <nirmata-host:port>
 defaultPassword: <default-tenant-password>
```

Update the file with information about VCD, RabbitMQ and Nirmata URL and save it (in /nirmata-ext/vcd-config)

Next, run the Nirmata server extension using the command:
```
docker run -d -v /nirmata-ext/vcd-ext-db:/vcd-ext-db -v /nirmata-ext/vcd-config:/config -e CONFIG_FILE=/config/nirmata-vcd-ext.yaml nirmata/nirmata-vcd-ext:v0.2.5
```

Note: You can change the path in the docker run command based on the directories you created earlier.

Check the container logs for any errors.

#### VCD Client UI Plugin

Install the UI plugin by downloading the plugin.zip file and install it using the ‘Customize Portal’ option. You will need to be a Service Provider admin for this operation.



Once the plugin is installed, you can Publish it to the Tenants



Next, configure the nirmata extension in VCD using CLI:

vcd system extension create nirmata nirmata nirmata nirmataext '/api/nirmata, /api/nirmata/.*, /api/nirmata/.*/.*'

##### Service Provider Settings

Now you can log in as a Service Provider admin and select Kubernetes from the menu to update the Service Provider Settings.

Settings
```
  - Use the Service Provider admin user id (provided to you)
  - Enter the URL for Nirmata (e.g. www.nirmata.io)
  - Enter the username and password for service provider admin (provided to you)
```


If the 'Add Existing Tenants' box is checked, VCD tenants will be automatically provisioned in Nirmata.

Next, you should be able to log in as Tenant Admin and register your Kubernetes clusters to manage in VCD.


#### Register Clusters

To register new cluster, you can go to the Kubernetes->Clusters panel and click on the Register button



Once the cluster is registered, you can view the details and perform other operations




### Nirmata Private Edition (on-prem) Installation

#### Prerequisites

Host resource requirements - 

   * 32GB memory + 8 vCPUs + 120GB storage
1. Operating System
2. Ubuntu 18.04 or Centos7
3. Container Engine - Docker 18.06.2  is recommended, but 1.11, 1.12, 1.13 and 18.09 are known to work as well. (docker installation: https://kubernetes.io/docs/setup/cri/#docker)
4. Disable swap on the host
```sudo swapoff -a```
6. Remove any swap entries from:  ```/etc/fstab```
7. Become root - ```sudo su -```
8. Internet access to repos like Docker Hub and gcr.io


#### Nirmata PE Installation Steps

Import the OVF template into center and launch a VM using this OVF template.
Power-on the VM and access the VM with following credentials with credentials that were shared with you.

In order to run nadm you will need to "sudo -i" to become root. With root privilege, run "nadm install" to install Nirmata.

Below are steps for Nirmata install - 

To install Nirmata, run command - 
```
root#nadm install
During installation, you will be asked for following  - 
root@ciops1# ./nadm install
*** Setup for your Nirmata install. Hit enter to use default values ***
No network proxy settings found. Proceed without a proxy? (y/n: y):y
Registry for Nirmata images [index.docker.io]: [Press Enter]
Registry (index.docker.io) username: nirmatainstaller
Registry (index.docker.io) password: NirmataPE
Registry (index.docker.io) confirm password: 
Kubernetes namespace for Nirmata [nirmata]:
URL for Nirmata (e.g. https://nirmata.company.com):https://<your-ip>:31443 (URL for Nirmata)
[ Generate a self-signed certificate for Nirmata? (y/n: y):y
Generating default certificate and key...Generating a 2048 bit RSA private key
...................................................+++
.........................................................................................................................................+++
writing new private key to '/root/.nirmata-nadm/ssl/server.key'
-----
Default volume capacity of Elasticsearch is 50Gi. Proceed? (y/n: y): y
Install a Kubernetes Cluster for Nirmata? (y/n: n):y
Install for high-availability (requires 3 nodes)? (y/n: n): n
Nirmata volumes require 80 GB to be available, mount path for Nirmata volumes [/var/nirmata]. Proceed? (y/n: y): y

Nirmata will install Kubernetes Cluster for you. You should see the following output - 
[cluster-init] Provisioning master node
[cluster-init] Installing cluster
[init] Using Kubernetes version: v1.15.1
[preflight] Running pre-flight checks
	[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Activating the kubelet service
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [ciops1 localhost] and IPs [10.10.1.193 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [ciops1 localhost] and IPs [10.10.1.193 127.0.0.1 ::1]
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [ciops1 kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 10.10.1.193]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[kubelet-check] Initial timeout of 40s passed.
[apiclient] All control plane components are healthy after 40.506321 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.15" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Storing the certificates in Secret "kubeadm-certs" in the "kube-system" Namespace
[upload-certs] Using certificate key:
e60088ed4df72bf3ec7222b676828dcdb438449ce806566b46418101b2e223c0
[mark-control-plane] Marking the node ciops1 as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node ciops1 as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: vslj4v.czd4gy5edpyy32wy
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy
[cluster-init] Starting cluster
node/ciops1 untainted

Your Kubernetes cluster has initialized successfully!
NAME     STATUS   ROLES    AGE   VERSION
ciops1   Ready    master   37s   v1.15.1

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /root/.nirmata-nadm/.kube/config $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


Once cluster is up, the installer will ask to proceed with Nirmata installation. Press y and proceed - 
```
Proceed to install Nirmata? (y/n: y):y
[validation-checks] Found cluster:
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   
[validation-checks] Using cluster context [kubernetes-admin@kubernetes], proceed (y/n: y):y
namespace/nirmata created
storageclass hostpath created
provisioner hostpath created
secret/nirmata-registry created
serviceaccount/default configured
priorityclass.scheduling.k8s.io/nirmata-data-critical created
priorityclass.scheduling.k8s.io/nirmata-data-lower created
priorityclass.scheduling.k8s.io/nirmata-app-critical created
priorityclass.scheduling.k8s.io/nirmata-app-lower created
zk created, waiting for pod to run...done
mongodb created, waiting for pod to run...done
elasticsearch created, waiting for pod to run...done
kafka created, waiting for pod to run...done
Volumes patched
Creating Nirmata services (This might take a few minutes or longer if the Nirmata images have to be pulled)
activity created, waiting for pod to run...done
analytics created, waiting for pod to run...done
catalog created, waiting for pod to run...done
client-gateway created, waiting for pod to run...done
cluster created, waiting for pod to run...done
config created, waiting for pod to run...done
environments created, waiting for pod to run...done
host-gateway created, waiting for pod to run...done
orchestrator created, waiting for pod to run...done
security created, waiting for pod to run...done
static-files created, waiting for pod to run...done
tunnel created, waiting for pod to run...done
users created, waiting for pod to run...done
webclient created, waiting for pod to run...done
haproxy created, waiting for pod to run...done
Checking connection...


	Nirmata is running! You can now login to Nirmata via:

		https://10.10.1.193:31443

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /root/.nirmata-nadm/.kube/config $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  
```



Configure Cluster Access for the Regular User
Setup kubectl

```
   	

 mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

```

#### Post Nirmata PE Installation Steps

1. Once Nirmata install is completed, access the Nirmata UI at https://<your-ipaddress-for-nirmata:31443 and create the admin user.
2. Next, create a Service Provider Admin by editing the nirmata-vcd-ext/bin/create-sp.sh script with Nirmata URL, super admin username and password and running the script. 
3. Save the Service Provider admin user id generated by the script.

#### Nirmata PE Extension Installation

Follow the same steps as described in the Nirmata Extension Installation section.


Nirmata PE vCD Client UI Plugin Installation
Follow the same steps as described in the vCD Client UI Plugin Installation section.


### Clean Up
Uninstall Nirmata
nadm uninstall 

Uninstall from a directory:
nadm uninstall -f $PATH

Clean up cluster
nadm reset

Remove download binary
Centos7
yum remove -y kubeadm kubelet kubectl docker-ce
Ubuntu
apt-get remove kubeadm kubelet kubectl docker-ce
