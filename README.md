# DevOps & Kubernetes Engineering Portfolio

## Overview

Experienced DevOps Engineer with hands-on expertise in Kubernetes, AWS cloud infrastructure, CI/CD automation, Infrastructure as Code (IaC), container orchestration, monitoring, and configuration management.

Skilled in building production-style Kubernetes environments using Terraform, kubeadm, Auto Scaling Groups, Launch Templates, cloud-init automation, and AWS services. Strong experience with CI/CD pipelines, Docker, Jenkins, GitHub Actions, Ansible, and observability stacks.

---

# Core Skills

## Cloud & Infrastructure

* AWS (EC2, IAM, VPC, Route Tables, Security Groups, ASG, EKS, SSM)
* Terraform
* Infrastructure as Code (IaC)
* Auto Scaling & Immutable Infrastructure
* Launch Templates
* cloud-init Automation

## Kubernetes & Containers

* Kubernetes (kubeadm & EKS)
* Docker & containerd
* kubelet / kube-proxy
* Flannel CNI
* Helm
* NGINX Ingress
* AWS Load Balancer Controller
* EBS CSI Driver

## CI/CD & Automation

* Jenkins
* GitHub Actions
* Bitbucket Pipelines
* Maven & Gradle
* Docker Image Automation
* Rolling Deployments & Rollbacks
* Bash & Python Scripting

## Configuration Management

* Ansible
* Linux Server Automation
* Environment Standardization
* Package & Application Provisioning

## Monitoring & Logging

* Prometheus
* Grafana
* AlertManager
* Loki
* EFK Stack
* kube-state-metrics
* node-exporter

---

# Kubernetes Troubleshooting

## CrashLoopBackOff Troubleshooting

### Step 1 — Inspect Pod Status & Events

```bash
kubectl describe pod <pod-name>
```

Checks:

* Failed mounts
* Probe failures
* Restart reasons
* Image pull issues
* Event logs

---

### Step 2 — Check Container Logs

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> --previous
```

`--previous` is important because containers may already have restarted.

---

### Step 3 — Verify Resource Issues

Common checks:

* `OOMKilled`
* CPU throttling
* Resource limits
* Node resource pressure

---

### Step 4 — Validate Configuration

Verify:

* Environment variables
* ConfigMaps
* Secrets
* Volume mounts
* Image tags
* External dependencies (DB/APIs)

---

### Step 5 — Fix Root Cause

Examples:

* Correct application bugs
* Increase memory limits
* Update incorrect image
* Fix missing secrets/configurations

---

### Step 6 — Redeploy & Monitor

```bash
kubectl rollout restart deployment <deployment-name>
kubectl get pods -w
```

Also verify:

* Readiness probes
* Liveness probes
* Restart count
* Dependency availability

---

# Deployment Rollout Troubleshooting

## Rollout Status

```bash
kubectl rollout status deployment/<deployment-name>
```

## Inspect Pods

```bash
kubectl get pods
kubectl get pods -o wide
```

### Common Pod States

| Status               | Possible Cause              |
| -------------------- | --------------------------- |
| Pending              | Scheduling/resource issue   |
| ImagePullBackOff     | Bad image/tag/auth          |
| CrashLoopBackOff     | Application startup failure |
| Running but NotReady | Readiness/dependency issue  |

---

## Describe Failing Pod

```bash
kubectl describe pod <pod-name>
```

Checks:

* Scheduling failures
* CPU/memory shortage
* Probe failures
* Config/mount issues

---

## Check Logs

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> --previous
```

---

# Monitoring & Alerting Architecture

## Monitoring Stack

Implemented monitoring using:

* kube-prometheus-stack
* Prometheus
* Grafana
* AlertManager
* node-exporter
* kube-state-metrics

## Logging Stack

* Loki
* EFK Stack

## Alerting

Configured alerts for:

* CPU & Memory usage
* Pod restarts
* Node health
* Ingress failures
* Application response metrics

---

# Production Kubernetes Architecture

## Infrastructure Provisioning with Terraform

Terraform provisions:

* VPC
* Subnets
* Route Tables
* Security Groups
* IAM Roles
* Launch Templates
* Auto Scaling Groups
* EC2 Instances
* SSM Permissions

---

## Node Configuration with cloud-init

cloud-init handles:

* OS setup
* containerd installation
* kubeadm/kubelet installation
* Networking configuration
* Kubernetes bootstrap

---

## Kubernetes Cluster Automation

### Master Flow

```text
Install kubeadm
↓
kubeadm init
↓
Generate join token
↓
Store token in SSM Parameter Store
```

### Worker Flow

```text
Install kubeadm
↓
Read join token from SSM
↓
Automatically join cluster
```

---

# Immutable Infrastructure Design

## Why Launch Templates + ASG

Benefits:

* Self-healing nodes
* Rolling updates
* Auto scaling
* Immutable infrastructure
* Automatic node replacement

---

# Recommended Project Structure

```text
terraform-k8s/
│
├── modules/
│   ├── vpc/
│   ├── security-group/
│   ├── iam/
│   ├── launch-template/
│   ├── asg/
│   ├── ssm/
│   └── master/
│
├── userdata/
│   ├── master.sh
│   └── worker.sh
│
├── environments/
│   └── dev/
```

---

# CI/CD Workflow

```text
Developer Push Code
        ↓
GitHub / Bitbucket
        ↓
Jenkins / GitHub Actions
        ↓
Maven / Gradle Build
        ↓
Docker Image Build
        ↓
Push to ECR / DockerHub
        ↓
Deploy to Kubernetes
        ↓
Terraform / Ansible manage infrastructure
```

---

# Build & Release Management

## CI/CD Experience

* Automated builds and deployments
* Docker image creation & registry management
* Kubernetes rolling deployments
* Rollback strategies
* Multi-environment deployment management

## Tools Used

* Jenkins
* GitHub Actions
* Bitbucket Pipelines
* Maven
* Gradle
* Docker
* Kubernetes

---

# Configuration Management

## Ansible Automation

Used Ansible for:

* Server provisioning
* Linux configuration management
* Package installation
* Environment standardization

## Scripting

* Bash scripting
* Python automation scripts

---

# Kubernetes Internal Architecture

```text
kubectl
   ↓
API Server
   ↓
Scheduler
   ↓
kubelet on worker
   ↓
containerd
   ↓
Pod created
```

---

# AWS Load Balancer Integration

## How Kubernetes Creates AWS Load Balancers

Kubernetes itself does not directly create AWS load balancers.

Components like:

* AWS Cloud Controller Manager
* AWS Load Balancer Controller

watch Kubernetes Services and Ingress resources and then call AWS APIs using IAM permissions.

### Flow

```text
kubectl apply
      ↓
Kubernetes API Server
      ↓
Service created (type=LoadBalancer)
      ↓
Cloud Controller Manager notices event
      ↓
AWS API called
      ↓
ELB/NLB created
      ↓
DNS returned to Service
```

---

# Dynamic EBS Provisioning

## Kubernetes + EBS CSI Driver

Kubernetes dynamically provisions EBS volumes using the EBS CSI Driver.

### Flow

```text
PVC Created
    ↓
Storage Controller detects request
    ↓
EBS CSI Driver calls AWS API
    ↓
EBS Volume created
    ↓
PV automatically bound
    ↓
Pod mounts volume
```

---

# Future Production Enhancements

Planned production upgrades:

* Multi-master HA cluster
* Private subnets
* NAT Gateway
* Bastion host
* Route53
* TLS certificates
* Helm
* ArgoCD
* Cluster Autoscaler
* AWS Load Balancer Controller
* ExternalDNS
* Prometheus/Grafana Stack

---

# Key Learnings

Implemented:

* Kubernetes provisioning
* kubeadm automation
* containerd runtime
* Terraform IaC
* Environment isolation
* Remote state management
* Worker node automation
* cloud-init bootstrap
* Flannel networking
* Production-style infrastructure patterns

---

# Interview Highlights

### Example Experience Statement

> “I have worked on CI/CD pipelines where source code from GitHub/Bitbucket was automatically built using Maven/Gradle, Docker images were created, and artifacts were pushed to repositories like ECR.”

> “I handled automated deployments using Jenkins and GitHub Actions pipelines for Kubernetes and AWS environments with rollback and production release validation.”

> “I used Ansible for configuration management and Terraform for infrastructure provisioning to maintain scalable and consistent cloud environments.”

---

# Contact

* Kubernetes
* AWS
* Terraform
* DevOps
* CI/CD
* SRE
* Platform Engineering

---
