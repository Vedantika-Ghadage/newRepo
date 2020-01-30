+++
title = "Install Nirmata PE"
description = ""
weight=10
+++

#### Introduction

Nirmata Private Edition (PE) can be easily installed using nadm  tool in single host or high-availability configuration. Nirmata PE uses Kubernetes as orchestration engine to deploy its components.


#### Prerequisites


1. Hosts with internet access to download Nirmata images from Docker Hub and Google Container Repository.
2. For the basic install,  a host with with following spec - 8 vCPU, 32GB memory, 200Gb SSD storage.
3. For HA install, 3 hosts with following spec - 8 vCPU, 32GB memory, 200Gb SSD storage.
4. Disable swap using the Disable Swap command.
```
$sudo swapoff -a
Remove any swap entries from:  /etc/fstab
```
5. Install Docker Engine version 18.09.2. Instructions to install Docker are available [here](https://docs.docker.com/install/).


#### Install and Check Load Balancer


To start, setup a Load Balancer for the Kubernetes API server.

Next, ensure that the Load Balancer is accessible from all hosts. Verify accessibility with nc and curl by using the Check Load Balancer Command. 

Check Load Balancer Command (nc):
```
root@nadmtest30:~# nc -v haproxy0.lab.nirmata.io 6443
```
Check Load Balancer Command (curl):
```
root@nadmtest30:~# curl -k https://haproxy0.lab.nirmata.io:6443
```
If the Load Balancer is accessible the nc and curl commands will return a success message:
```
Connection to nadmtest10.lab.nirmata.io 6443 port [tcp/*] succeeded!
```
If the Load Balancer is not accessible, a Service Unavailable message will return:
```
503 Service Unavailable
No server is available to handle this request.
```

#### Configure Proxy for Docker
Configure proxy for Docker if you are using Proxy in your infrastructure.. The Docker daemon uses the HTTP_PROXY, HTTPS_PROXY, and NO_PROXY environmental variables in its start-up environment to configure HTTP or HTTPS proxy behavior.

To configure proxy for Docker: 
1. Create a systemd drop-in directory for the docker service:
```
$ sudo mkdir -p /etc/systemd/system/docker.service.d
```
2. Create a file called /etc/systemd/system/docker.service.d/http-proxy.conf that adds the HTTP_PROXY environment variable:

```
[Service]
	Environment="HTTP_PROXY=http://nibr1:3128/"  "NO_PROXY=localhost,127.0.0.1,nibr1,nibr2.nibr3"
Environment="HTTPS_PROXY=http://nibr1:3128/" "NO_PROXY=localhost,127.0.0.1,nibr1,nibr2,nibr3"
```

1. Flush changes using the Flush Changes command.
Flush Changes Command:
```
$ sudo systemctl daemon-reload
```

4. Restart Docker using the Restart Docker command.
Restart Docker Command:
```
$ sudo systemctl restart docker
```
5. After Docker restarts, verify that the configuration loaded using the Verify Configuration command.
Verify Configuration Command:
```
$ systemctl show --property=Environment docker
Environment=HTTPS_PROXY=https://proxy.example.com:443/
```

#### Install Nirmata 

Nirmata uses nadm tool to install the base Kubernetes cluster and deploys Nirmata on it. nadm toolset simplifies Nirmata deployment by provisioning both base and Nirmata with few simple parameters for the deployment. 

Download the Nirmata install binary and run the appropriate version.



##### Nirmata Release 2.8.2 
Curl -LO https://nadm-release.s3-us-west-1.amazonaws.com/nadm-2.8.2.tar.gz


To install Nirmata, run nadm install on any one of the Kubernetes master-nodes. To configure the base cluster and nirmata properly following parameters will be requested - 

1. Image registry for Nirmata images - use default unless you have downloaded Nirmata images to your local repository.
2. username/password for repository access - Use Nirmata provided credentials or use your own if using private repository.
3. Nirmata URL - Provide URL for Nirmata services. You can use default HTTPS port (443) or 31443.
4. Certificates - Provide your own CA certs or let Nirmata create self-signed certificates.
5. The volume used by Nirmata services requires a minimum of 80G of storage.
6. Option to install Kubernetes cluster for Nirmata - If installing on hosts with no existing Kubernetes cluster, choose “yes”.
7. High Availability install - choose yes if installing for HA configuration.
8. Nirmata will install Kubernetes cluster (HA if HA configuration chosen), will configure the storage class, connect with load balancer and setup ports for optimal clusters op].
9. Nirmata install  - Type “yes” to proceed with Nirmata installation;


The installation process will look as shown below  - 
```
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
Install a Kubernetes Cluster for Nirmata? (y/n: n):n
Install for high-availability (requires 3 nodes)? (y/n: n): n
Nirmata volumes require 80 GB to be available, mount path for Nirmata volumes [/var/nirmata]. Proceed? (y/n: y): y

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

		https://10.10.1.193





```

Nirmata deploys Kubernetes v1.15.1 as the base cluster.

Check the status of the install from another term window with command using the Check Status command.

Check Status Command:
```
./nadm status -w -n <namespace>
```
#### Uninstall
To uninstall, delete the cluster. 

To delete a cluster, run the kubeadm Reset command on all master nodes.

Nirmata uninstall Command:
```
$ nadm uninstall
```
Next, run the Nirmata Agent Cleanup on the hostgroup using the Nirmata Cleanup command.

#### Nirmata Backup, Restore and Upgrade 
Nirmata database can be easily backed up using nadm toolset and the same can be used to restore Nirmata if required.
```
$ nadm backup
```
This will backup the database in the /.../.nirmata-nadm/backup/nirmata-database-yyyy-mm-dd-xx-xx-xx/nirmata-database.gz
 file.


To restore the Nirmata database, use following nadm command - 
```
$ nadm restore -d /.../.nirmata-nadm/backup/nirmata-database-yyyy-mm-dd-xx-xx-xx/nirmata-database.gz
```

To upgrade Nirmata, download the latest nadm tool for the new release and in that directtory use following nadm command - 
```
$ ./nadm generate
```
This will create necessary necessary yaml files for Nirmata with latest release in yamls directory under .nirmata-nadm folder. Yon can upgrade Nirmata by simply running the command below - 

```
$ kubectl apply -f /root/.nirmata-nadm/yamls-nirmata/yamls-2019-10-15-14-14-40/services/ (yaml files directory) -n nirmata
```
