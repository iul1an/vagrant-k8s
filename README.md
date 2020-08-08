# vagrant-k8s
Deploy a local vm-based Kubernetes cluster using Vagrant, VirtualBox and Ansible.

## Requirements
- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Python](https://www.python.org/downloads/)

## Setup
- Clone the repo:
```
git clone https://github.com/iul1an/vagrant-k8s.git
```

- Update the ***Vagrantfile*** file according to you needs:
  - Number of worker nodes
  - Network:
    - IP addresses
    - MetalLB network segment
```
cd vagrant-k8s
$EDITOR Vagrantfile
```
- Install Ansible (skip this step if you already have Ansible)

```
pip install -r requirements.txt
```


- Deploy
```
vagrant up
```

##
