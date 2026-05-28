# Senior DevOps / Cloud Platform Engineer

## About Me

I am a **Senior DevOps / Cloud Platform Engineer** with **18+ years of experience** in:

* AWS Cloud
* Kubernetes
* Terraform
* CI/CD Automation
* Infrastructure Modernization
* Production Platform Engineering

In recent years, my primary focus has been on:

* Designing and managing scalable AWS and Kubernetes-based platforms
* Implementing Infrastructure as Code (IaC) using Terraform
* Automating deployment pipelines using Jenkins and GitHub Actions
* Supporting highly available production environments

I have strong experience in:

* DevSecOps
* Observability
* Incident Management
* Security Remediation
* Certificate Rotation
* Cloud-native Infrastructure

Currently, I am also exploring **AI/GenAI infrastructure patterns on AWS** using:

* Amazon Bedrock
* Amazon EKS
* Scalable inference workloads

---

# AWS Architecture Experience

I have extensive hands-on experience with AWS services including:

* EC2
* IAM
* VPC
* Route53
* EKS
* ECS
* Lambda
* CloudWatch
* S3
* ALB/NLB
* AWS Security Services

## Typical AWS Architecture Design

* Multi-AZ highly available environments
* Public and private subnets
* NAT Gateways
* Internet Gateways
* Route Tables
* Security Groups
* IAM least-privilege access

## Kubernetes on AWS (EKS)

Integrated services include:

* AWS Load Balancer Controller
* EBS CSI Driver
* Route53
* CloudWatch
* Prometheus/Grafana

Infrastructure provisioning is fully automated using:

* Terraform modules
* CI/CD pipelines

Focus areas:

* Scalability
* Monitoring
* Disaster Recovery
* Security Hardening

---

# Highly Available Multi-AZ AWS Environment

## VPC Design

* One VPC
* Public and private subnets across multiple AZs

### Public Subnets

* ALB/NLB
* NAT Gateway

### Private Subnets

* Application Servers
* EKS Worker Nodes
* Databases

## Networking

* Internet Gateway
* Route Tables
* NAT Gateway for outbound internet access

### Traffic Flow

```text
Internet → ALB → Application/EKS Nodes
```

## Best Practices

* Keep workloads in private subnets
* Least privilege security groups
* Separate Dev/UAT/Prod environments
* Use VPC endpoints where possible
* Enable VPC Flow Logs

## Security

* Restrict inbound traffic
* Use private internal communication
* Separate database subnet groups

---

# Compute Layer

* Auto Scaling Groups
* Multi-AZ deployment
* Health checks and self-healing

# Load Balancer

* ALB distributes traffic across healthy targets
* SSL termination at ALB

# Database Layer

* RDS Multi-AZ
* Automated backups
* Read replicas when needed

---

# Kubernetes / EKS Experience

## Core Responsibilities

* Cluster provisioning
* Node group management
* Helm deployments
* Ingress configuration
* Storage integration
* Monitoring setup
* Production troubleshooting

## Kubernetes Resources

* Deployments
* StatefulSets
* DaemonSets
* Services
* Ingress
* ConfigMaps
* Secrets
* HPA
* Taints/Tolerations
* Affinity Rules

## AWS Integrations

* AWS Load Balancer Controller
* EBS CSI Driver
* IAM Roles for Service Accounts (IRSA)

## Production Troubleshooting

* Pod failures
* OOM issues
* CrashLoopBackOff
* Networking issues
* DNS resolution
* Storage problems
* Node pressure conditions

---

# Kubernetes Networking

## Key Concepts

### Pod-to-Pod Communication

Each pod receives its own IP address.

### AWS VPC CNI

Provides pod networking for EKS.

### Kubernetes Services

* ClusterIP
* NodePort
* LoadBalancer
* Headless Services

### Ingress

Handles HTTP/HTTPS routing.

### kube-proxy

Manages service routing using iptables/ipvs.

### CoreDNS

Provides service discovery.

## Troubleshooting Areas

* DNS resolution
* Network policies
* Security groups
* CNI issues
* kube-proxy issues

---

# CI/CD Pipeline Experience

Implemented CI/CD pipelines using:

* Jenkins
* GitHub Actions

## Typical Workflow

1. Code checkout from GitHub
2. Build process
3. Unit testing
4. Security scanning
5. Docker image creation
6. Push image to registry
7. Kubernetes deployment

## Deployment Methods

* Helm Charts
* kubectl apply
* GitOps workflows

## CI/CD Best Practices

* Environment-based deployments
* Approval gates
* Rollback strategy
* Secret management
* Zero-downtime deployments
* Monitoring validation

---

# Terraform Experience

## Workflow

* terraform init
* terraform plan
* approval process
* terraform apply

## Features

* Reusable modules
* Remote state management
* S3 backend
* DynamoDB locking
* Environment separation
* CI/CD integration

## Common Modules

* VPC
* EKS
* IAM
* ALB

---

# ECS vs EKS

## ECS

* AWS-native orchestration
* Easier AWS integration
* Simpler operational model
* Supports EC2 and Fargate

## EKS

* Kubernetes standard platform
* Better portability
* Larger ecosystem
* Advanced orchestration capabilities

Primary expertise is focused on Kubernetes/EKS platforms.

---

# DevSecOps Experience

* Vulnerability remediation
* Secrets management
* Certificate rotation
* IAM controls
* Security scanning
* Least privilege access
* Audit compliance
* Container security

## Security Best Practices

* MFA enforcement
* CloudTrail logging
* KMS encryption
* IRSA for Kubernetes
* Container image scanning

---

# Monitoring & Observability

## Monitoring Stack

* Prometheus
* Grafana
* AlertManager
* CloudWatch
* ELK / Splunk
* Loki

## Monitoring Areas

### Infrastructure

* CPU
* Memory
* Disk
* Network

### Kubernetes

* Pod restarts
* Pending pods
* Node health
* API latency

### Applications

* Response time
* Error rate
* Throughput

## Alerting

Integrated with:

* Slack
* Email
* PagerDuty
* Webhooks

---

# Monitoring Architecture

```text
Applications / Nodes / Kubernetes
                ↓
           Prometheus
                ↓
          AlertManager
                ↓
   Slack / Email / PagerDuty

Grafana ← Prometheus
```

---

# Production Incident Management

## Responsibilities

* Incident triage
* Severity assessment
* Stakeholder communication
* Log analysis
* Rollback/fix implementation
* RCA documentation
* Preventive actions

## Typical Troubleshooting Commands

```bash
kubectl get pods -A
kubectl describe pod
kubectl logs
kubectl top pod
kubectl get events
kubectl describe node
```

---

# Blue-Green & Canary Deployments

## Blue-Green

* Two environments
* Traffic switching
* Fast rollback

## Canary

* Gradual traffic shifting
* Reduced deployment risk
* Progressive rollout

---

# AWS Load Balancer Controller

## Purpose

Automatically provisions ALB/NLB for Kubernetes ingress/services.

## Workflow

```text
Ingress → ALB Controller → AWS API → Create ALB
```

## Benefits

* Dynamic routing
* SSL support
* Path-based routing
* Automated target groups

---

# EBS CSI Driver

## Purpose

Provides persistent storage for Kubernetes workloads.

## Workflow

```text
PVC → StorageClass → EBS CSI Driver → EBS Volume
```

## Common Use Cases

* StatefulSets
* Databases
* Persistent applications

---

# Helm Charts

## Components

* values.yaml
* templates/
* Chart.yaml

## Benefits

* Reusability
* Parameterization
* Easy upgrades
* Rollbacks

## Common Commands

```bash
helm install
helm upgrade
helm rollback
```

---

# Docker Best Practices

* Multi-stage builds
* Small base images
* Minimize layers
* Non-root users
* .dockerignore
* Image scanning

## Example

```dockerfile
FROM golang:1.22 AS builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM alpine:latest
COPY --from=builder /app/app .
CMD ["./app"]
```

---

# Node Affinity / Taints / Tolerations

## Taint Example

```bash
kubectl taint nodes node1 dedicated=prod:NoSchedule
```

## Toleration Example

```yaml
tolerations:
- key: "dedicated"
  operator: "Equal"
  value: "prod"
  effect: "NoSchedule"
```

## Node Affinity Example

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: environment
          operator: In
          values:
          - production
```

---

# IAM Design Best Practices

* Least privilege access
* Role-based access control
* No hardcoded credentials
* MFA enforcement
* IRSA for EKS
* Separate roles per environment

## Example Roles

* EC2 Role
* EKS Node Role
* Pod IAM Role
* CI/CD Role

---

# Production RCA Example

## Scenario

Application downtime after deployment.

## Investigation

* Alert received
* CrashLoopBackOff observed
* Logs showed DB connection failure
* Incorrect secret identified

## Resolution

* Rolled back deployment
* Restored service

## Preventive Actions

* Secret validation
* Pre-deployment checks
* Better monitoring alerts
* Deployment approvals

---

# Why Hire Me?
* AWS & Kubernetes expertise
* Strong production support background
* Automation-first mindset
* Infrastructure architecture experience
* Reliability engineering focus
* DevSecOps exposure
* Enterprise platform engineering experience
* Proven ability to handle critical production environments
