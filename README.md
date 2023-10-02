# DevOps Playground

## Table of Contents

- [Overview](#overview)
- [Infrastructure](#infrastructure)
  - [SRV2, controller & gateway](#srv2-controller--gateway)
  - [Nodes](#nodes)
- [Ansible](#ansible)

---

## Overview

This devops playground is about building infrastructure for cluster nodes and training devops techniques and technologies like ansible, kubernetes, github actions for ci/cd pipelines and so on and more ...

---

## Infrastructure

The infrastructure is built with existing VPS resources, if they will not be sufficient during testing, an scale up is possible.  
SRV2 will serve as a bridge to the world and a controller for nodes on a private network.
Ubuntu 22.04 LTS is used on all VPS.

Infrastructure sketch:
![infrastructure](/docs/images/vpsinfra.jpg)

**Allocable resources:**  
CPU cores: 16 shared  
RAM: 8GB  
Disk space: 240GB

**Allocated resources:**  
SRV2 and each node has been allocated the same resources so far ...  
CPU cores: 2  
RAM: 1GB  
Disk space: 30GB  

---

### SRV2, controller & gateway

SRV2 is configured and administered locally/manually for now. The nodes are administered from srv2 using ansible.  

[SRV2 configuration procedure](/docs/srv2_config.md)  

This configuration is sufficient from the security point of view for now, if necessary further configuration will be made on the basis of the results and recommendations of the lynis audit system.

---

### Nodes

Nodes are created manually with basic configuration, then they are managed using ansible from SRV2.  

[Nodes configuration procedure](/docs/nodes_config.md)  

Now is ansible used for further configuration.

## Ansible

Ansible related files are located in the directory [Ansible](/ansible).

- Run initial configuration  
playbook [initial.yaml](ansible/initial.yaml)

```bash
ansible-playbook --ask-become-pass initial.yaml
```

- Upgrade system  
playbook [upgrade.yaml](ansible/upgrade.yaml)

```bash
ansible-playbook upgrade.yaml
```

- Create sudo user (optional)  
playbook [user_sudo.yaml](ansible/user_sudo.yaml)

```bash
ansible-playbook user_sudo.yaml
```
