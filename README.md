# 🏠 Homelab Infrastructure

Welkom bij mijn homelab documentatie. Dit repository bevat alle configuraties, automatiseringen en documentatie voor mijn complete homelab setup.

## 📚 Table of Contents

1. [Overview & Architecture](#1-overview--architecture)
2. [Hardware Infrastructur](#2-hardware-infrastructure)
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
- **Learning**: Hands-on ervaring met Ansible, Home-Assistant, VM's, Linux, Kubernetes
- **Automation**: Infrastructure as Code principes
- **Self-hosting**: Eigen services draaien voor privacy en controle

---

## 2. Hardware Infrastructure

### 🖥️ Server Specifications

| Server | CPU | RAM | Storage | Role |
|--------|-----|-----|---------|------|
| Proxmox | NUC Mini PC - Intel N100 | 16GB | 1TB SDD | Main |

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


#### Key VMs:
- **Home Assistant**: Smart home automation
- **Kubernetes Nodes**: K8s cluster members

---

## 5. Container Orchestration

### ☸️ Kubernetes Cluster
- **Distribution**: K3s (lightweight)
- **Nodes**: 1 master nodes + 1 worker nodes
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

### 🤖 Ansible Automation
**Location**: [`/ansible/`](./ansible/)

**Current Playbooks:**
- **SSL Certificate Management**: Self-signed CA voor homelab services


**Planned Additions:**
- ArgoCD deployment automation


#### Quick Start:
```bash
cd ansible/
ansible-playbook ssl-certificate-management.yml
```

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
- **Root CA**: Home-CA voor internal services
- **Automated deployment**: Via Ansible automation
- **Certificate rotation**: planned

### 🛡️ Security Measures
- **Access control**: SSH Harderning & 2FA
- planned

---

## 9. Backup & Disaster Recovery

### 💾 Backup Strategy
- **3-2-1 Rule**: 3 copies, 2 different media, 1 offsite
- **VM Backups**: Proxmox Backup Server (planned)
- **Application Data**: Home-Asssistant back-up to personal cloud, rest is planned

---

## 10. CI/CD & GitOps

### 🚀 GitOps Workflow
- **ArgoCD**: Kubernetes application deployment (planned)
- **Git**: Source of truth voor alle configuraties
- **Testing**: Automated testing pipeline (planned)
- **Rollback**: One-click rollback capability (planned)

---


## 🤝 Bijdragen

Dit is mijn persoonlijke homelab project, maar suggesties en verbeteringen zijn altijd welkom via issues of pull requests.




## 📄 License

MIT License - zie [LICENSE](LICENSE) voor details.

---

> **Maintained by**: Kim007dus