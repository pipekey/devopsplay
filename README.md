# DevOps Playground

## Table of Contents

- [Overview](#overview)
- [Infrastructure](#infrastructure)

---

## Overview

This devops playground is about building infrastructure for cluster nodes and training devops techniques and technologies like ansible, kubernetes, github actions for ci/cd pipelines and so on and more ...

---

## Infrastructure

The infrastructure is built with existing VPS resources, if they will not be sufficient during testing, an scale up is possible.  
SRV2 will serve as a bridge to the world and a controller for nodes on a private network

---
Infrastructure sketch:
![infrastructure](/docs/images/vpsinfra.jpg)

---

**Allocable resources:**  
CPU cores: 16 shared  
RAM: 8GB  
Disk space: 240GB

**Allocated resources:**  
SRV2 and each node has been allocated the same resources so far ...  
CPU cores: 2  
RAM: 1GB  
Disk space: 30GB  
