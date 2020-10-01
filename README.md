# vagrant-k8s
Deploy a local vm-based Kubernetes cluster using Vagrant, VirtualBox and Ansible.

This branch is specifically made to work with ***Debian 10*** and it will create a ***HA Kubernetes cluster with 3 nodes***

## Requirements
- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Python](https://www.python.org/downloads/)

## Setup
- Clone the repo:
```
git clone https://github.com/iul1an/vagrant-k8s.git
```

- Update the ***Vagrantfile*** file according to your needs:
  - Hardware resources: CPU, memory
  - Network:
    - IP addresses
    - MetalLB network segment
```
cd vagrant-k8s
$EDITOR Vagrantfile
```
- Install Ansible (***skip*** this step if you already have Ansible)

```
pip install -r requirements.txt
```


- Deploy
```
vagrant up
```

## Usage
```
vagrant ssh k8s-master
kubectl <action> <object>
```
OR
```
export KUBECONFIG=tmp/kubectl/config
kubectl <action> <object>
```
