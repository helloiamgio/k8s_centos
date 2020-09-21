## Kubernetes

Kubernetes (commonly stylized as k8s[3]) is an open-source container-orchestration system for automating application deployment, scaling, and management. It aims to provide a "platform for automating deployment, scaling, and operations of application containers across clusters of hosts".[3] It works with a range of container tools, including Docker.[5] Many cloud services offer a Kubernetes-based platform or infrastructure as a service (PaaS or IaaS) on which Kubernetes can be deployed as a platform-providing service. 

---
### VAGRANT IMAGES is BASED ON CENTOS 7.8

## Command :
- cd kubernetes/vagrant-provisioning
- ls -ltr

Vagrantfile: The primary function of the Vagrantfile is to describe the type of machine required for a project, and how to configure and provision these machines. In this file, you will have settings such as operating system type, hostnames of your VMs in the cluster, node count for a few examples. The file also specifies the bootstrap scripts.
bootstrap.sh: This file is a basic set of initial instructions that will generally be applied to both the master Kubernetes node and the worker nodes as well. It does things such as update the /etc/hosts file to include all the nodes, installs docker, disable selling and firewalld. It also installed Kubernetes 

bootstrap_kmaster.sh: This file Initialize Kubernetes, create the flannel network

bootstrap_kworker: This script will join the worker nodes to the cluster

- vagrant up
- vagrant status
- vagrant ssh kmaster
- kubectl get all --all-namespaces

## Install the Kubernetes Dashboard ##

To deploy the Web UI (Dashboard) or Kubernetes Dashboard run the following command:
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml

The deployment file will publish the Kubernetes Dashboard using a ClusterIP service as shown below using TargetPort 8443:

$ kubectl -n kubernetes-dashboard describe service kubernetes-dashboard

In order to access the Kubernetes Dashboard from our workstation, a NodePort will be created to publish the kubernetes-dashboard following the Publish an Application Outside Kubernetes Cluster instructions.

The file kubernetes-dashboard-service-np.yaml is available in the repo

- Apply the changes
$ kubectl apply -f kubernetes-dashboard-service-np.yaml 

Obtain an authentication token to use on the Kubernetes Dashboard authentication realm
$ kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

Access the Kubernetes Dashboard using the URL https://<MASTER_IP>:30002/#/login using the token printed before:

## BONUS ##
## Please read other ways to publish the Kubernetes Dashboard on the Kubernetes Dashboard documentation.
Useful Vagrant commands
#Create the cluster or start the cluster after a host reboot
vagrant up
#Execute again the Ansible playlist in all the vagrant boxes, useful during development of Ansible playbooks
vagrant provision 
#Execute again the Ansible playlist in the Kubernetes node 1
vagrant provision k8s-n-1
#Poweroff the Kubernetes Cluster
vagrant halt
#Open an ssh connection to the Kubernetes master
vagrant ssh k8s-m-1
#Open an ssh connection to the Kubernetes node 1
vagrant ssh k8s-n-1
#Open an ssh connection to the Kubernetes node 2
vagrant ssh k8s-n-2
#Stop all Vagrant machines (use vagrant up to start)
vagrant halt
