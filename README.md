## Kubernetes

Kubernetes (commonly stylized as k8s[3]) is an open-source container-orchestration system for automating application deployment, scaling, and management. It aims to provide a "platform for automating deployment, scaling, and operations of application containers across clusters of hosts".[3] It works with a range of container tools, including Docker.[5] Many cloud services offer a Kubernetes-based platform or infrastructure as a service (PaaS or IaaS) on which Kubernetes can be deployed as a platform-providing service. 

---

## Tutorials

This tutorial has been prepared for those who want to understand the containerized infrastructure and deployment of application on containers. This tutorial will help in understanding the concepts of container management using Kubernetes.

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
