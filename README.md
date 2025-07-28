# 🏠 Homelab Infrastructure

Welcome to my homelab documentation. This repository contains all configurations, automations, and documentation for my complete homelab setup. This is a work-in-progress project.

## 📚 Table of Contents

1. [Overview & Architecture](#1-overview--architecture)
2. [Hardware Infrastructure](#2-hardware-infrastructure)
3. [Network Configuration](#3-network-configuration)
4. [Virtualization Platform](#4-virtualization-platform)
5. [Container Orchestration](#5-container-orchestration)
6. [Automation & Configuration Management](#6-automation--configuration-management)
7. [Monitoring & Observability](#7-monitoring--observability)
8. [Security & Certificates](#8-security--certificates)
9. [Backup & Disaster Recovery](#9-backup--disaster-recovery)
10. [CI/CD & GitOps](#10-cicd--gitops)

---

## 1. Overview & Architecture

### 🎯 Homelab Goals
- **Learning**: Hands-on experience with Ansible, Home Assistant, VMs, Linux, Kubernetes
- **Automation**: Infrastructure as Code principles
- **Self-hosting**: Running my own services for privacy and control

---

## 2. Hardware Infrastructure

### 🖥️ Server Specifications

| Server  | CPU                    | RAM  | Storage | Role |
|---------|------------------------|------|---------|------|
| Proxmox | NUC Mini PC - Intel N100 | 16GB | 1TB SSD | Main |

---

## 3. Network Configuration

### 📡 VLAN Layout
planned

### 🔒 Firewall Rules
planned

---

## 4. Virtualization Platform

### 🖥️ Proxmox VE Setup
- **Version**: Proxmox VE 8.4.1
Currently, I have a standard installation on my NUC Mini PC.

#### Key VMs:
- [**Home Assistant**](./home_assistant/README.md): Smart home automation 
- **Kubernetes Nodes**: K8s cluster
- **Linux Arch**: To gain more hands-on Linux experience, I want to install a VM from scratch with Arch Linux. *planned*

---

## 5. Container Orchestration

### ☸️ Kubernetes Cluster
- **Distribution**: K3s (lightweight)
- **Nodes**: 1 master node + 1 worker node
- **Storage**: planned
- **Networking**: planned
- **Load Balancer**: planned

#### Core Services:
- **Ingress**: planned
- **DNS**: planned 
- **Secrets**: planned
- **Monitoring**: planned

---

## 6. Automation & Configuration Management

### 🤖 Ansible 
**Location**: [`/ansible/`](./ansible/)

**Current Playbooks:**
- **SSL Certificate Management**: Self-signed CA for homelab services

**Planned Additions:**
- ArgoCD deployment automation

---

## 7. Monitoring & Observability

### 📊 Monitoring Stack
- **Metrics**: Prometheus + Grafana (planned)
- **Logging**: planned
- **Tracing**: planned
- **Alerting**: AlertManager + Discord webhooks (planned)

### 📈 Key Dashboards
Planned

---

## 8. Security & Certificates

### 🔐 PKI Infrastructure
- **Root CA**: Home-CA for internal services
- **Automated deployment**: Via Ansible automation
- **Certificate rotation**: planned

### 🛡️ Security Measures
- **Access control**: SSH Hardening & 2FA
- planned

---

## 9. Backup & Disaster Recovery

### 💾 Backup Strategy
- **3-2-1 Rule**: 3 copies, 2 different media, 1 offsite
- **VM Backups**: Proxmox Backup Server (planned)
- **Application Data**: Home Assistant backup to personal cloud, rest is planned

---

## 10. CI/CD & GitOps

### 🚀 GitOps Workflow
- **FluxCD**: Kubernetes application deployment (planned)
- **Git**: Source of truth for all configurations
- **Testing**: Automated testing pipeline (planned)
- **Rollback**: One-click rollback capability (planned)

---

## 🤝 Contributing

This is my personal homelab project, but suggestions and improvements are always welcome via issues or pull requests.

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

> **Maintained by**: Kim