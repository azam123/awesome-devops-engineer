# 🚀 Terraform + Docker + Kubernetes + Azure DevOps — Beginner-to-Production Guide

[![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC?logo=terraform&logoColor=white)](https://developer.hashicorp.com/terraform/docs)
[![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?logo=docker&logoColor=white)](https://docs.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?logo=kubernetes&logoColor=white)](https://kubernetes.io/docs/)
[![Azure](https://img.shields.io/badge/Microsoft%20Azure-Cloud-0078D4?logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Azure DevOps](https://img.shields.io/badge/Azure%20DevOps-CI%2FCD-0078D7?logo=azuredevops&logoColor=white)](https://learn.microsoft.com/azure/devops/)
[![AKS](https://img.shields.io/badge/Azure%20Kubernetes%20Service-AKS-0078D4?logo=microsoftazure&logoColor=white)](https://learn.microsoft.com/azure/aks/)
[![HCL](https://img.shields.io/badge/HCL-Configuration-623CE4?logo=hashicorp&logoColor=white)](https://developer.hashicorp.com/terraform/language)
[![YAML](https://img.shields.io/badge/YAML-Pipelines%20%26%20Manifests-CB171E?logo=yaml&logoColor=white)](https://yaml.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Learn the complete cloud-native delivery chain:**  
> **Code → Docker → Container Registry → Kubernetes → Azure → Terraform → Azure DevOps CI/CD**

This guide explains **Terraform, Docker, Kubernetes and Azure DevOps** from the ground up using real-world analogies and progressively more realistic examples.

It is intentionally written for **beginners**, but the final sections introduce the concepts expected from a **Cloud Engineer, DevOps Engineer, .NET Architect, Solution Architect or Principal Engineer**.

---

## 🏷️ Topics / Keywords

`terraform` `terraform-azure` `docker` `dockerfile` `containers` `kubernetes` `k8s` `aks` `azure-kubernetes-service` `azure` `azure-devops` `azure-pipelines` `devops` `cicd` `iac` `infrastructure-as-code` `microservices` `cloud-native` `containerization` `orchestration` `helm` `acr` `azure-container-registry` `deployment` `service` `ingress` `hpa` `autoscaling` `service-principal` `managed-identity` `yaml` `hcl` `dotnet` `dotnet-core` `devsecops` `platform-engineering`

---

# 📚 Table of Contents

1. [The Big Picture](#-1-the-big-picture)
2. [Real-World Analogy](#-2-real-world-analogy)
3. [What Is Docker?](#-3-what-is-docker)
4. [What Is Kubernetes?](#-4-what-is-kubernetes)
5. [What Is Terraform?](#-5-what-is-terraform)
6. [What Is Azure DevOps?](#-6-what-is-azure-devops)
7. [How They Work Together](#-7-how-they-work-together)
8. [Prerequisites](#-8-prerequisites)
9. [Install the Tools](#-9-install-the-tools)
10. [Docker — First Container](#-10-docker--first-container)
11. [Dockerfile Explained](#-11-dockerfile-explained)
12. [Docker Compose](#-12-docker-compose)
13. [Kubernetes Fundamentals](#-13-kubernetes-fundamentals)
14. [Your First Kubernetes Deployment](#-14-your-first-kubernetes-deployment)
15. [Kubernetes Service](#-15-kubernetes-service)
16. [ConfigMaps and Secrets](#-16-configmaps-and-secrets)
17. [Health Checks](#-17-health-checks)
18. [Scaling with Kubernetes](#-18-scaling-with-kubernetes)
19. [Terraform Fundamentals](#-19-terraform-fundamentals)
20. [Terraform with Azure](#-20-terraform-with-azure)
21. [Terraform Variables, Outputs and Modules](#-21-terraform-variables-outputs-and-modules)
22. [Terraform State](#-22-terraform-state)
23. [Provisioning AKS with Terraform](#-23-provisioning-aks-with-terraform)
24. [Azure Container Registry](#-24-azure-container-registry)
25. [Azure DevOps CI/CD](#-25-azure-devops-cicd)
26. [Complete End-to-End Architecture](#-26-complete-end-to-end-architecture)
27. [Production-Ready Improvements](#-27-production-ready-improvements)
28. [Security Checklist](#-28-security-checklist)
29. [Troubleshooting](#-29-troubleshooting)
30. [Interview Questions](#-30-interview-questions)
31. [Learning Roadmap](#-31-learning-roadmap)
32. [Official Documentation](#-32-official-documentation)

---

# 🌎 1. The Big Picture

Imagine you are opening a **large restaurant chain**.

You need:

- A building
- Electricity
- Water
- Kitchen equipment
- Refrigerators
- Staff
- Menus
- Food
- A system for receiving orders
- A system for preparing orders
- A system for delivering orders
- Monitoring
- Automated processes

Now map that to a cloud application:

| Real World | Cloud / DevOps |
|---|---|
| Restaurant building | Azure infrastructure |
| Kitchen | Application runtime |
| Packed food box | Docker container |
| Kitchen manager | Kubernetes |
| Recipe/infrastructure blueprint | Terraform |
| Food delivery pipeline | Azure DevOps |
| Warehouse | Container Registry |
| Kitchen workers | Kubernetes Pods |
| Customer-facing counter | Kubernetes Service / Ingress |
| Ingredient configuration | ConfigMap |
| Passwords / keys | Secret |
| More workers during rush hour | Horizontal Pod Autoscaler |
| Building blueprint | Terraform configuration |
| Daily operating process | CI/CD pipeline |

The important idea is:

```text
                    ☁️ AZURE CLOUD
                         │
                         ▼
                ┌──────────────────┐
                │    TERRAFORM      │
                │ Infrastructure    │
                │      as Code      │
                └────────┬─────────┘
                         │
                         ▼
                ┌──────────────────┐
                │       AKS        │
                │   Kubernetes     │
                └────────┬─────────┘
                         │
                 ┌───────┴────────┐
                 ▼                ▼
              Pod A             Pod B
                 │                │
                 └───────┬────────┘
                         ▼
                    🐳 Docker
                    Container
                         │
                         ▼
                 Application Code

        ┌─────────────────────────────────┐
        │         Azure DevOps            │
        │  Build → Test → Image → Deploy │
        └─────────────────────────────────┘
```

---

# 🧠 2. Real-World Analogy

## 🐳 Docker = Packaging

Suppose your application requires:

- .NET 8
- specific libraries
- environment variables
- configuration
- system dependencies

Without containers, a developer might say:

> "It works on my machine."

Docker solves this by packaging the application and its runtime dependencies into a **container image**.

Think of it as a standardized shipping container.

```text
Application
    +
Runtime
    +
Dependencies
    +
Configuration
    ↓
┌────────────────────────┐
│    📦 Docker Image     │
└────────────────────────┘
    ↓
Runs consistently
on different machines
```

---

## ☸️ Kubernetes = Container Manager

Imagine you have:

```text
1 container
```

Easy.

But now you have:

```text
100 containers
10 services
5 environments
3 regions
automatic scaling
failed containers
rolling deployments
networking
secrets
configuration
```

Managing them manually becomes difficult.

Kubernetes acts like a **smart operations manager**.

It continuously asks:

> "What should the application look like?"

and works to make reality match that desired state.

---

## 🏗️ Terraform = Infrastructure Blueprint

Instead of manually creating:

- Resource Groups
- VNets
- Subnets
- AKS
- ACR
- Key Vault
- Storage
- PostgreSQL
- Application Gateway

you write code describing what you want.

```hcl
resource "azurerm_resource_group" "app" {
  name     = "rg-cloud-native-demo"
  location = "East US"
}
```

Terraform then creates the infrastructure.

Think of Terraform as the **architect + construction blueprint + construction automation**.

---

## 🔄 Azure DevOps = Automated Factory

Azure DevOps can automate:

```text
Developer
   ↓
Git Commit
   ↓
Build
   ↓
Unit Tests
   ↓
Docker Build
   ↓
Security Scan
   ↓
Push Image → ACR
   ↓
Deploy → AKS
   ↓
Smoke Test
   ↓
Production
```

This is **CI/CD — Continuous Integration and Continuous Delivery/Deployment**.

---

# 🔗 3. How Everything Fits Together

The simplest mental model:

```text
                  👨‍💻 Developer
                       │
                       │ git push
                       ▼
               ┌───────────────┐
               │ Azure Repos / │
               │    GitHub     │
               └───────┬───────┘
                       │
                       ▼
              ┌──────────────────┐
              │  Azure Pipelines │
              │     CI/CD        │
              └────────┬─────────┘
                       │
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
       🧪 Build/Test        🐳 Docker Build
                                 │
                                 ▼
                         ┌───────────────┐
                         │      ACR      │
                         │ Container Reg │
                         └───────┬───────┘
                                 │
                                 ▼
                           ☸️ AKS
                         Kubernetes
                                 │
                     ┌───────────┼───────────┐
                     ▼           ▼           ▼
                   Pod         Pod         Pod
                     │           │           │
                     └───────────┼───────────┘
                                 ▼
                              Users
```

Terraform operates mainly on the **infrastructure layer**:

```text
Terraform
   │
   ├── Resource Group
   ├── Networking
   ├── ACR
   ├── AKS
   ├── Key Vault
   ├── Managed Identity
   └── Monitoring
```

Azure DevOps operates mainly on the **delivery layer**:

```text
Source Code
   ↓
Build
   ↓
Test
   ↓
Package
   ↓
Docker Image
   ↓
Registry
   ↓
Kubernetes Deployment
```

---

# 🐳 4. What Is Docker?

Docker is a platform for building, packaging, distributing and running applications in **containers**.

## Container vs Virtual Machine

### Virtual Machine

```text
Physical Server
└── Hypervisor
    ├── VM 1
    │   └── Guest OS
    │       └── Application
    ├── VM 2
    │   └── Guest OS
    │       └── Application
    └── VM 3
        └── Guest OS
            └── Application
```

### Containers

```text
Physical Server
└── Container Runtime
    ├── Container 1
    │   └── Application
    ├── Container 2
    │   └── Application
    └── Container 3
        └── Application
```

Containers usually share the host kernel, making them lighter than full VMs.

---

# 🐳 5. Docker Core Concepts

| Concept | Simple Explanation |
|---|---|
| Image | Immutable application package/template |
| Container | Running instance of an image |
| Dockerfile | Instructions for building an image |
| Registry | Repository for images |
| Volume | Persistent storage |
| Network | Communication between containers |
| Tag | Version/name associated with an image |

### Image → Container

```text
Dockerfile
    │
    │ docker build
    ▼
┌──────────────┐
│ Docker Image │
│   v1.0       │
└──────┬───────┘
       │
       │ docker run
       ▼
┌──────────────┐
│  Container   │
│   Running    │
└──────────────┘
```

---

# 🛠️ 6. Docker Installation

Official documentation:

- [Docker Documentation](https://docs.docker.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Docker Get Started](https://docs.docker.com/get-started/)

Verify installation:

```bash
docker --version
```

Check Docker Engine:

```bash
docker info
```

Run your first container:

```bash
docker run hello-world
```

Expected result:

```text
Hello from Docker!
Your installation appears to be working correctly.
```

---

# 🧪 7. First Docker Application

Create:

```text
docker-demo/
├── Dockerfile
└── app/
    └── ...
```

For a .NET application:

```bash
dotnet new webapi -n CloudNativeApi
cd CloudNativeApi
```

Run locally:

```bash
dotnet run
```

---

# 📄 8. Dockerfile Explained

A production-style multi-stage Dockerfile for a .NET application:

```dockerfile
# -------------------------------
# Stage 1: Build
# -------------------------------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY ["CloudNativeApi.csproj", "./"]

RUN dotnet restore "CloudNativeApi.csproj"

COPY . .

RUN dotnet publish \
    "CloudNativeApi.csproj" \
    -c Release \
    -o /app/publish \
    /p:UseAppHost=false


# -------------------------------
# Stage 2: Runtime
# -------------------------------
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 8080

ENTRYPOINT ["dotnet", "CloudNativeApi.dll"]
```

## Why multi-stage builds?

Instead of shipping the complete SDK inside the production image:

```text
SDK Image
├── Compiler
├── NuGet
├── Build tools
└── Application
```

we build first and copy only the published application:

```text
Build Image
     │
     │ dotnet publish
     ▼
Production Image
├── ASP.NET Runtime
└── Published Application
```

Benefits:

- Smaller images
- Reduced attack surface
- Faster deployment
- Cleaner production image

---

# 🏗️ 9. Build and Run

Build:

```bash
docker build -t cloudnative-api:1.0 .
```

List images:

```bash
docker images
```

Run:

```bash
docker run -d \
  --name cloudnative-api \
  -p 8080:8080 \
  cloudnative-api:1.0
```

Check:

```bash
docker ps
```

Stop:

```bash
docker stop cloudnative-api
```

Remove:

```bash
docker rm cloudnative-api
```

---

# 🏷️ 10. Image Tagging

Avoid relying only on:

```text
latest
```

Prefer immutable version tags:

```text
cloudnative-api:1.0.0
cloudnative-api:1.0.1
cloudnative-api:2026.10.06
cloudnative-api:<git-sha>
```

A strong CI/CD pattern is:

```text
Git Commit
   ↓
Git SHA
   ↓
Docker Tag
   ↓
ACR
   ↓
AKS
```

Example:

```bash
docker build -t myregistry.azurecr.io/cloudnative-api:abc123 .
docker push myregistry.azurecr.io/cloudnative-api:abc123
```

---

# 🧩 11. Docker Compose

Docker Compose is useful for running multiple containers together, especially for local development.

Example:

```yaml
services:

  api:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    environment:
      ASPNETCORE_ENVIRONMENT: Development

  redis:
    image: redis:7
    ports:
      - "6379:6379"
```

Start:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

Think:

```text
Docker
   = One shipping container

Docker Compose
   = Local fleet of containers
```

---

# ☸️ 12. What Is Kubernetes?

Kubernetes is a container orchestration platform.

Its job is to manage containerized workloads across a cluster.

Kubernetes can:

- Schedule containers
- Restart failed workloads
- Scale applications
- Provide networking
- Manage configuration
- Manage secrets
- Perform rolling deployments
- Expose applications
- Support health checks
- Maintain desired state

Official documentation:

https://kubernetes.io/docs/

---

# 🧠 13. Kubernetes Real-World Analogy

Imagine a hotel.

```text
Hotel
│
├── Floor 1
│   ├── Room 101
│   └── Room 102
│
├── Floor 2
│   ├── Room 201
│   └── Room 202
│
└── Reception
```

Kubernetes:

```text
Cluster
│
├── Node
│   ├── Pod
│   │   └── Container
│   └── Pod
│       └── Container
│
├── Node
│   ├── Pod
│   └── Pod
│
└── Node
    └── Pod
```

---

# 🧱 14. Kubernetes Architecture

```text
                    Kubernetes Cluster
                           │
             ┌─────────────┴─────────────┐
             │                           │
       Control Plane                  Worker Nodes
             │                           │
      ┌──────┼──────┐             ┌─────┴─────┐
      │      │      │             │           │
   API     Scheduler  etcd       Node        Node
   Server                       │           │
      │                         Pods        Pods
      │
      └── Desired State
```

Important components:

| Component | Responsibility |
|---|---|
| API Server | Entry point to Kubernetes |
| Scheduler | Chooses nodes for Pods |
| etcd | Stores cluster state |
| Controller Manager | Reconciles desired state |
| Kubelet | Runs on worker nodes |
| Kube-proxy | Networking rules |
| Container Runtime | Runs containers |

---

# 📦 15. Pod

A Pod is the smallest deployable unit in Kubernetes.

Usually:

```text
Pod
└── Container
    └── Application
```

But a Pod can contain multiple tightly coupled containers:

```text
Pod
├── Application Container
└── Sidecar Container
```

Pods are generally **ephemeral**.

Do not design your application around the assumption that a Pod has a permanent identity.

---

# 🚀 16. Kubernetes Deployment

A Deployment manages ReplicaSets and Pods.

Example:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: cloudnative-api

spec:
  replicas: 3

  selector:
    matchLabels:
      app: cloudnative-api

  template:
    metadata:
      labels:
        app: cloudnative-api

    spec:
      containers:
        - name: cloudnative-api

          image: myregistry.azurecr.io/cloudnative-api:1.0.0

          ports:
            - containerPort: 8080

          resources:
            requests:
              cpu: "100m"
              memory: "128Mi"

            limits:
              cpu: "500m"
              memory: "512Mi"
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

Check:

```bash
kubectl get deployments
kubectl get pods
```

---

# 🔄 17. Kubernetes Desired State

This is one of the most important Kubernetes concepts.

You say:

```yaml
replicas: 3
```

Kubernetes tries to maintain:

```text
Desired State
      │
      │ reconciliation
      ▼
┌─────────────────┐
│ 3 running Pods  │
└─────────────────┘
```

If one Pod crashes:

```text
Before:

Pod A   Pod B   Pod C
  ✅      ❌      ✅

Kubernetes
     │
     ▼
creates replacement

After:

Pod A   Pod D   Pod C
  ✅      ✅      ✅
```

This is the **self-healing** behavior of Kubernetes.

---

# 🌐 18. Kubernetes Service

Pods are temporary.

Their IP addresses can change.

A Service provides a stable network endpoint.

```text
              Service
          cloudnative-api
                 │
       ┌─────────┼─────────┐
       ▼         ▼         ▼
     Pod A     Pod B     Pod C
```

Example:

```yaml
apiVersion: v1
kind: Service

metadata:
  name: cloudnative-api

spec:
  selector:
    app: cloudnative-api

  ports:
    - port: 80
      targetPort: 8080

  type: ClusterIP
```

---

# 🌍 19. Service Types

| Type | Use |
|---|---|
| ClusterIP | Internal communication |
| NodePort | Expose through node port |
| LoadBalancer | Cloud load balancer |
| ExternalName | DNS-based external service |

For production AKS workloads, traffic is often exposed through:

```text
Internet
   ↓
Application Gateway / Load Balancer / Ingress
   ↓
Kubernetes Service
   ↓
Pods
```

---

# 🔐 20. ConfigMaps and Secrets

## ConfigMap

Use for non-sensitive configuration.

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: cloudnative-config

data:
  ASPNETCORE_ENVIRONMENT: "Production"
  LOG_LEVEL: "Information"
```

Use:

```yaml
envFrom:
  - configMapRef:
      name: cloudnative-config
```

## Secret

Secrets are intended for sensitive values.

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: database-secret

type: Opaque

stringData:
  connectionString: "REPLACE_ME"
```

For real production systems, prefer a dedicated secret-management solution such as **Azure Key Vault** rather than committing secrets to Git.

---

# ❤️ 21. Health Checks

A production service should tell Kubernetes whether it is healthy.

Two important probes:

### Liveness

> "Is the application still alive?"

### Readiness

> "Can the application receive traffic?"

Example:

```yaml
livenessProbe:
  httpGet:
    path: /health/live
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /health/ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

Flow:

```text
                Kubernetes
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
     Liveness              Readiness
       probe                  probe
          │                   │
          ▼                   ▼
   Restart if bad      Remove from traffic
```

---

# 📈 22. Scaling with Kubernetes

## Manual scaling

```bash
kubectl scale deployment cloudnative-api --replicas=5
```

## Horizontal Pod Autoscaler

Example:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler

metadata:
  name: cloudnative-api

spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: cloudnative-api

  minReplicas: 2
  maxReplicas: 10

  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

Conceptually:

```text
Low traffic
   ↓
2 Pods

Traffic increases
   ↓
CPU > threshold
   ↓
HPA
   ↓
4 Pods

Traffic increases again
   ↓
8 Pods

Traffic decreases
   ↓
Pods scale down
```

---

# 🏗️ 23. What Is Terraform?

Terraform is an **Infrastructure as Code (IaC)** tool.

Instead of manually clicking through a cloud portal, you describe infrastructure using configuration files.

Example:

```hcl
resource "azurerm_resource_group" "app" {
  name     = "rg-cloud-native-demo"
  location = "East US"
}
```

Terraform's common workflow is:

```text
┌──────────┐
│  Write   │
│  .tf     │
└────┬─────┘
     │
     ▼
terraform init
     │
     ▼
terraform validate
     │
     ▼
terraform plan
     │
     ▼
Review
     │
     ▼
terraform apply
     │
     ▼
☁️ Infrastructure
```

Terraform uses providers to interact with APIs, including Azure and Docker.

Official documentation:

https://developer.hashicorp.com/terraform/docs

---

# 🧩 24. Terraform Core Concepts

| Concept | Meaning |
|---|---|
| Provider | Plugin connecting Terraform to an API |
| Resource | Infrastructure object Terraform manages |
| Variable | Input to configuration |
| Output | Value exposed after deployment |
| Module | Reusable Terraform component |
| State | Terraform's record of managed infrastructure |
| Plan | Preview of changes |
| Apply | Execute changes |
| Destroy | Remove managed resources |

---

# 📁 25. Recommended Terraform Structure

```text
terraform/
├── providers.tf
├── main.tf
├── variables.tf
├── outputs.tf
├── versions.tf
├── locals.tf
├── terraform.tfvars
├── modules/
│   ├── network/
│   ├── acr/
│   └── aks/
└── environments/
    ├── dev/
    ├── test/
    └── prod/
```

For larger organizations, separate reusable modules from environment-specific configuration.

---

# ⚙️ 26. Terraform Installation

Official installation:

https://developer.hashicorp.com/terraform/install

Verify:

```bash
terraform version
```

Azure quickstart:

https://learn.microsoft.com/azure/developer/terraform/get-started/quickstart-configure

---

# ☁️ 27. Azure CLI

Install:

https://learn.microsoft.com/cli/azure/install-azure-cli

Verify:

```bash
az version
```

Login:

```bash
az login
```

List subscriptions:

```bash
az account list
```

Select subscription:

```bash
az account set --subscription "<SUBSCRIPTION_ID>"
```

---

# 🧪 28. First Terraform + Azure Example

Create:

```text
terraform-demo/
└── main.tf
```

`main.tf`:

```hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 4.0"
    }
  }

  required_version = ">= 1.0"
}

provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "demo" {
  name     = "rg-terraform-demo"
  location = "East US"
}
```

Initialize:

```bash
terraform init
```

Format:

```bash
terraform fmt
```

Validate:

```bash
terraform validate
```

Plan:

```bash
terraform plan
```

Apply:

```bash
terraform apply
```

Destroy when finished:

```bash
terraform destroy
```

Terraform's Azure tutorials cover this same initialize → plan → apply lifecycle. 

---

# 🔢 29. Terraform Variables

Instead of hard-coding:

```hcl
location = "East US"
```

use:

```hcl
variable "location" {
  type        = string
  description = "Azure deployment region"
  default     = "East US"
}
```

Then:

```hcl
resource "azurerm_resource_group" "demo" {
  name     = "rg-terraform-demo"
  location = var.location
}
```

Set a value:

```bash
terraform apply -var="location=West Europe"
```

Or:

```hcl
# terraform.tfvars

location = "West Europe"
```

---

# 📤 30. Terraform Outputs

```hcl
output "resource_group_name" {
  value = azurerm_resource_group.demo.name
}
```

Then:

```bash
terraform output
```

Specific output:

```bash
terraform output resource_group_name
```

---

# ♻️ 31. Terraform Modules

Imagine creating AKS repeatedly for:

```text
Development
Testing
Staging
Production
```

Instead of copying hundreds of lines, create a reusable module.

```text
modules/
└── aks/
    ├── main.tf
    ├── variables.tf
    └── outputs.tf
```

Use it:

```hcl
module "aks" {
  source = "./modules/aks"

  cluster_name        = "aks-dev"
  resource_group_name = azurerm_resource_group.demo.name
  location            = var.location
}
```

Think:

```text
Module
   =
Reusable Infrastructure Component
```

---

# 💾 32. Terraform State

Terraform needs to remember what it manages.

That information is stored in a **state file**.

Conceptually:

```text
Terraform Configuration
        │
        │ desired state
        ▼
Terraform State
        │
        │ compare
        ▼
Real Azure Infrastructure
```

The state helps Terraform determine what needs to change.

### Never casually commit:

```text
terraform.tfstate
terraform.tfstate.backup
```

to a public repository.

For team environments, use a secure remote backend with locking/versioning appropriate to your organization.

---

# 🗄️ 33. Azure Remote State

A common Azure architecture is:

```text
Azure Storage Account
        │
        └── Blob Container
                │
                └── Terraform State
```

Example backend configuration:

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-terraform-state"
    storage_account_name = "tfstatecloudnative"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

Do not put storage access keys directly into source code.

Use secure authentication appropriate to your CI/CD environment.

---

# ☸️ 34. Provisioning AKS with Terraform

Azure Kubernetes Service (AKS) is Microsoft's managed Kubernetes service.

Official quickstart:

https://learn.microsoft.com/azure/aks/learn/quick-kubernetes-deploy-terraform

Conceptual architecture:

```text
                Terraform
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
      Resource     VNet       ACR
       Group                  │
          │                   │
          └─────────┬─────────┘
                    ▼
                  AKS
             ┌──────┴──────┐
             │             │
          Node Pool     Node Pool
             │             │
            Pods          Pods
```

A simplified example:

```hcl
resource "azurerm_kubernetes_cluster" "aks" {
  name                = "aks-cloud-native"
  location            = azurerm_resource_group.demo.location
  resource_group_name = azurerm_resource_group.demo.name
  dns_prefix          = "aks-cloud-native"

  default_node_pool {
    name       = "system"
    node_count = 2
    vm_size    = "Standard_D2s_v5"
  }

  identity {
    type = "SystemAssigned"
  }
}
```

For production, do not blindly copy a minimal example. Networking, identity, node pools, security, observability, availability and cost requirements should be designed deliberately.

Microsoft also documents production-oriented AKS deployments using **Azure Verified Modules**.

---

# 📦 35. Azure Container Registry

Azure Container Registry (ACR) stores Docker/OCI images.

Think:

```text
Docker Image
     │
     │ docker push
     ▼
┌───────────────────┐
│ Azure Container   │
│ Registry (ACR)    │
└─────────┬─────────┘
          │
          │ image pull
          ▼
        AKS
```

Login:

```bash
az acr login --name <ACR_NAME>
```

Build:

```bash
docker build \
  -t <ACR_NAME>.azurecr.io/cloudnative-api:1.0.0 .
```

Push:

```bash
docker push \
  <ACR_NAME>.azurecr.io/cloudnative-api:1.0.0
```

List repositories:

```bash
az acr repository list \
  --name <ACR_NAME> \
  --output table
```

---

# 🔗 36. Connect AKS to ACR

A common approach is to grant AKS permission to pull images from ACR.

Example:

```bash
az aks update \
  --name <AKS_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --attach-acr <ACR_NAME>
```

Then Kubernetes can use:

```yaml
image: <ACR_NAME>.azurecr.io/cloudnative-api:1.0.0
```

For enterprise environments, evaluate managed identities and least-privilege access rather than embedding registry credentials.

---

# 🚦 37. Kubernetes Deployment + Service

A practical application deployment can look like:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: cloudnative-api

spec:
  replicas: 3

  strategy:
    type: RollingUpdate

  selector:
    matchLabels:
      app: cloudnative-api

  template:
    metadata:
      labels:
        app: cloudnative-api

    spec:
      containers:
        - name: cloudnative-api

          image: myacr.azurecr.io/cloudnative-api:1.0.0

          ports:
            - containerPort: 8080

          resources:
            requests:
              cpu: "100m"
              memory: "128Mi"

            limits:
              cpu: "500m"
              memory: "512Mi"

          readinessProbe:
            httpGet:
              path: /health/ready
              port: 8080

          livenessProbe:
            httpGet:
              path: /health/live
              port: 8080
---
apiVersion: v1
kind: Service

metadata:
  name: cloudnative-api

spec:
  selector:
    app: cloudnative-api

  ports:
    - port: 80
      targetPort: 8080

  type: ClusterIP
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

Verify:

```bash
kubectl get pods
kubectl get deployment
kubectl get service
```

---

# 🔍 38. Essential kubectl Commands

Check cluster:

```bash
kubectl cluster-info
```

Nodes:

```bash
kubectl get nodes
```

Pods:

```bash
kubectl get pods
```

Detailed Pod information:

```bash
kubectl describe pod <POD_NAME>
```

Logs:

```bash
kubectl logs <POD_NAME>
```

Follow logs:

```bash
kubectl logs -f <POD_NAME>
```

Deployments:

```bash
kubectl get deployments
```

Services:

```bash
kubectl get services
```

Namespaces:

```bash
kubectl get namespaces
```

All resources:

```bash
kubectl get all
```

Execute inside a container:

```bash
kubectl exec -it <POD_NAME> -- /bin/sh
```

---

# 🔁 39. Rolling Deployment

Suppose production has:

```text
Version 1
Pod A
Pod B
Pod C
```

You deploy:

```text
Version 2
```

Kubernetes can progressively replace old Pods:

```text
Step 1

V1   V1   V2


Step 2

V1   V2   V2


Step 3

V2   V2   V2
```

This reduces downtime.

---

# 🧭 40. Namespaces

Namespaces logically separate workloads.

```text
AKS Cluster
│
├── dev
│   ├── API
│   └── Worker
│
├── staging
│   ├── API
│   └── Worker
│
└── prod
    ├── API
    └── Worker
```

Create:

```bash
kubectl create namespace dev
```

Deploy:

```bash
kubectl apply -f deployment.yaml -n dev
```

---

# 🔐 41. Kubernetes Security Concepts

Important concepts:

- RBAC
- Service Accounts
- Network Policies
- Pod Security
- Secrets
- Image scanning
- Resource limits
- Least privilege
- Workload identity
- Admission controls

Never treat:

```yaml
stringData:
  password: "MyPassword123"
```

as a safe production secret-management strategy.

---

# 🚀 42. What Is Azure DevOps?

Azure DevOps is a suite of development and delivery services.

Common components:

| Component | Purpose |
|---|---|
| Azure Repos | Git repositories |
| Azure Pipelines | CI/CD |
| Azure Boards | Planning |
| Azure Test Plans | Testing |
| Azure Artifacts | Package management |
| Environments | Deployment governance |

For this guide, the most important component is:

> **Azure Pipelines**

---

# 🔄 43. CI/CD Explained Simply

## Continuous Integration

Developers frequently merge code.

Pipeline:

```text
Commit
  ↓
Build
  ↓
Unit Tests
  ↓
Static Analysis
  ↓
Package
```

## Continuous Delivery / Deployment

```text
Build
  ↓
Docker Image
  ↓
Registry
  ↓
Deploy
  ↓
Smoke Test
  ↓
Production
```

---

# 🏭 44. Azure DevOps Pipeline Architecture

```text
Developer
    │
    ▼
Git Repository
    │
    │ Push
    ▼
Azure Pipeline
    │
    ├── Restore
    ├── Build
    ├── Test
    ├── Security Scan
    ├── Docker Build
    └── Docker Push
             │
             ▼
            ACR
             │
             ▼
            AKS
             │
             ▼
          Production
```

Microsoft documents Azure Pipelines workflows for building Docker images, pushing them to Azure Container Registry and deploying Kubernetes manifests to AKS.

---

# 🧾 45. Azure Pipeline YAML

Example:

```yaml
trigger:
  branches:
    include:
      - main

variables:
  imageRepository: 'cloudnative-api'
  dockerfilePath: '$(Build.SourcesDirectory)/Dockerfile'
  tag: '$(Build.SourceVersion)'
  containerRegistry: 'myacr.azurecr.io'

stages:

# ---------------------------------------
# Build and Test
# ---------------------------------------
- stage: Build
  displayName: Build and Test

  jobs:
  - job: Build

    pool:
      vmImage: ubuntu-latest

    steps:

    - task: UseDotNet@2
      inputs:
        packageType: sdk
        version: '8.x'

    - script: |
        dotnet restore
        dotnet build --configuration Release --no-restore
        dotnet test --configuration Release --no-build
      displayName: Build and Test


# ---------------------------------------
# Docker
# ---------------------------------------
- stage: Docker
  displayName: Build Docker Image
  dependsOn: Build

  jobs:
  - job: Docker

    pool:
      vmImage: ubuntu-latest

    steps:

    - task: Docker@2
      displayName: Build and Push Image
      inputs:
        command: buildAndPush
        repository: $(imageRepository)
        dockerfile: $(dockerfilePath)
        containerRegistry: 'ACR-Service-Connection'
        tags: |
          $(tag)


# ---------------------------------------
# Deploy
# ---------------------------------------
- stage: Deploy
  displayName: Deploy to AKS
  dependsOn: Docker

  jobs:
  - deployment: Deploy
    environment: production

    pool:
      vmImage: ubuntu-latest

    strategy:
      runOnce:

        deploy:
          steps:

          - task: KubernetesManifest@1
            displayName: Deploy Kubernetes Manifest
            inputs:
              action: deploy
              kubernetesServiceConnection: 'AKS-Service-Connection'
              manifests: |
                k8s/deployment.yaml
                k8s/service.yaml
```

---

# 🔐 46. Azure DevOps Service Connections

A pipeline needs permission to communicate with external services.

For example:

```text
Azure DevOps
     │
     ├── Azure Resource Manager
     │
     ├── ACR
     │
     └── AKS
```

A **service connection** provides the authenticated connection.

Use least privilege.

Avoid putting:

```text
Client Secret
Password
Access Key
```

directly into YAML.

Microsoft provides Azure DevOps service connection documentation:

https://learn.microsoft.com/azure/devops/pipelines/library/service-endpoints

---

# 🧪 47. CI/CD Pipeline — Detailed Flow

```text
                 👨‍💻 Developer
                      │
                      │ git push
                      ▼
              ┌───────────────┐
              │ Azure Repos / │
              │    GitHub     │
              └───────┬───────┘
                      │
                      ▼
             ┌──────────────────┐
             │ Azure Pipelines  │
             └────────┬─────────┘
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       Restore      Build       Test
          │           │           │
          └───────────┼───────────┘
                      ▼
              🐳 Docker Build
                      │
                      ▼
                🔍 Scan Image
                      │
                      ▼
                📦 Push to ACR
                      │
                      ▼
              ☸️ Deploy to AKS
                      │
                      ▼
              ❤️ Health Checks
                      │
                      ▼
                Smoke Tests
                      │
                      ▼
                🎉 Production
```

---

# 🏗️ 48. Infrastructure Pipeline vs Application Pipeline

A common architectural distinction:

## Infrastructure Pipeline

```text
Terraform
   ↓
Validate
   ↓
Plan
   ↓
Approval
   ↓
Apply
   ↓
Azure Infrastructure
```

## Application Pipeline

```text
Source Code
   ↓
Build
   ↓
Test
   ↓
Docker
   ↓
ACR
   ↓
AKS
```

Keeping these responsibilities clear helps prevent accidental infrastructure changes during normal application deployments.

---

# 🧱 49. End-to-End Reference Architecture

```text
                                  ☁️ AZURE
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   ┌──────────────┐                                               │
│   │ Azure DevOps │                                               │
│   │  CI / CD     │                                               │
│   └──────┬───────┘                                               │
│          │                                                        │
│          │ Build/Test                                             │
│          ▼                                                        │
│   ┌──────────────┐        Push Image        ┌─────────────────┐   │
│   │ Docker Build │ ──────────────────────► │      ACR        │   │
│   └──────────────┘                          │ Container       │   │
│                                             │ Registry        │   │
│                                             └────────┬────────┘   │
│                                                      │            │
│                                                      │ Pull       │
│                                                      ▼            │
│          ┌──────────────────────────────────────────────────┐     │
│          │                     AKS                          │     │
│          │                                                  │     │
│          │   ┌──────────────┐       ┌──────────────┐        │     │
│          │   │ Deployment   │──────►│    Pods      │        │     │
│          │   └──────────────┘       └──────┬───────┘        │     │
│          │                                  │                │     │
│          │                           ┌──────▼──────┐         │     │
│          │                           │   Service   │         │     │
│          │                           └──────┬──────┘         │     │
│          │                                  │                │     │
│          │                           ┌──────▼──────┐         │     │
│          │                           │   Ingress   │         │     │
│          │                           └──────┬──────┘         │     │
│          └─────────────────────────────────┼────────────────┘     │
│                                            │                      │
│                                            ▼                      │
│                                         Users                     │
│                                                                  │
│   ┌──────────────────────────────────────────────────────────┐   │
│   │                  Terraform                              │   │
│   │                                                          │   │
│   │ Resource Group | VNet | AKS | ACR | Key Vault | Monitor │   │
│   └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

# 🧠 50. One Conceptual Flow to Remember

```text
                 INFRASTRUCTURE
                       │
                    Terraform
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
         VNet         ACR          AKS
                                     │
                                     ▼
APPLICATION                          │
   │                                 │
   ▼                                 │
Dockerfile                           │
   │                                 │
   ▼                                 │
Docker Image                         │
   │                                 │
   ▼                                 │
   ACR ──────────────────────────────┘
                                     │
                                     ▼
                                  Kubernetes
                                     │
                              ┌──────┴──────┐
                              ▼             ▼
                            Pods          Service
                                            │
                                            ▼
                                         Users

AUTOMATION
   │
   ▼
Azure DevOps
   │
   ├── Build
   ├── Test
   ├── Docker
   ├── Push
   └── Deploy
```

---

# 🎯 51. A Beginner-Friendly Project

Build this project:

> **Cloud Native .NET API deployed to AKS using Terraform, Docker and Azure DevOps**

Repository structure:

```text
cloud-native-platform/
│
├── src/
│   └── CloudNativeApi/
│       ├── CloudNativeApi.csproj
│       ├── Program.cs
│       └── ...
│
├── tests/
│   └── CloudNativeApi.Tests/
│
├── docker/
│   └── Dockerfile
│
├── k8s/
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── hpa.yaml
│
├── infra/
│   └── terraform/
│       ├── providers.tf
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       └── modules/
│
├── pipelines/
│   ├── azure-pipelines.yml
│   └── terraform-pipeline.yml
│
└── README.md
```

---

# 🛠️ 52. Recommended Implementation Order

Do not try to learn everything at once.

Follow this order:

```text
1️⃣ Docker Basics
      ↓
2️⃣ Build .NET Container
      ↓
3️⃣ Kubernetes Basics
      ↓
4️⃣ Deploy Container Locally
      ↓
5️⃣ Terraform Basics
      ↓
6️⃣ Provision Azure
      ↓
7️⃣ Create ACR
      ↓
8️⃣ Create AKS
      ↓
9️⃣ Push Image
      ↓
🔟 Deploy to AKS
      ↓
1️⃣1️⃣ Azure DevOps CI
      ↓
1️⃣2️⃣ Azure DevOps CD
      ↓
1️⃣3️⃣ Security
      ↓
1️⃣4️⃣ Monitoring
      ↓
1️⃣5️⃣ Production Hardening
```

---

# 🧪 53. Local Kubernetes Options

You can learn Kubernetes locally using:

- Docker Desktop Kubernetes
- Minikube
- Kind

For beginners:

```text
Docker Desktop
    +
Kubernetes
    ↓
Local learning environment
```

Then move to:

```text
Local Kubernetes
       ↓
Azure Kubernetes Service
```

---

# 🧰 54. kubectl Installation

Official documentation:

https://kubernetes.io/docs/tasks/tools/

On Azure, the Azure CLI can also install the AKS CLI components:

```bash
az aks install-cli
```

Verify:

```bash
kubectl version --client
```

---

# 🔑 55. Connect to AKS

After creating an AKS cluster:

```bash
az aks get-credentials \
  --resource-group <RESOURCE_GROUP> \
  --name <AKS_NAME>
```

Verify:

```bash
kubectl get nodes
```

Expected conceptually:

```text
NAME           STATUS   ROLES
aks-node-001   Ready    <none>
aks-node-002   Ready    <none>
```

---

# 🧭 56. Ingress

A Service exposes an application inside or outside the cluster depending on its type.

Ingress provides HTTP/HTTPS routing.

Example:

```text
                    Internet
                       │
                       ▼
                 ┌───────────┐
                 │  Ingress  │
                 └─────┬─────┘
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
       /api         /orders      /users
          │            │            │
          ▼            ▼            ▼
       API Svc      Order Svc    User Svc
```

In Azure environments, evaluate whether Azure Application Gateway / Application Gateway for Containers or another ingress architecture is appropriate for your requirements.

---

# 🔄 57. GitOps vs Pipeline Deployment

There are multiple ways to deploy Kubernetes applications.

### Pipeline-driven

```text
Azure DevOps
    ↓
kubectl / KubernetesManifest
    ↓
AKS
```

### GitOps

```text
Git Repository
     ↓
Desired Kubernetes State
     ↓
GitOps Controller
     ↓
AKS
```

Popular GitOps tools include:

- Flux
- Argo CD

Do not mix every tool into your first project. Learn the basic deployment model first.

---

# 📦 58. Helm

Helm is a package manager for Kubernetes.

Without templating:

```text
deployment-dev.yaml
deployment-test.yaml
deployment-prod.yaml
```

With Helm:

```text
helm/
├── Chart.yaml
├── values.yaml
├── values-dev.yaml
├── values-prod.yaml
└── templates/
    ├── deployment.yaml
    ├── service.yaml
    └── ingress.yaml
```

Think:

```text
Helm Chart
    =
Reusable Kubernetes Application Package
```

---

# 🔐 59. Production Security Checklist

## Docker

- [ ] Use small runtime images
- [ ] Use multi-stage builds
- [ ] Do not run as root unnecessarily
- [ ] Scan images
- [ ] Pin important dependencies
- [ ] Avoid secrets in Dockerfiles
- [ ] Avoid `latest` for production releases

## Kubernetes

- [ ] Resource requests/limits
- [ ] Readiness probes
- [ ] Liveness probes
- [ ] RBAC
- [ ] Network policies where appropriate
- [ ] Namespace separation
- [ ] Secret management
- [ ] Pod security controls
- [ ] Image scanning
- [ ] Workload identity
- [ ] Audit logging

## Terraform

- [ ] Remote state
- [ ] State locking/versioning where supported
- [ ] Secure backend
- [ ] Modules
- [ ] Code review
- [ ] `terraform plan` before apply
- [ ] No secrets in Git
- [ ] Provider/version constraints
- [ ] Separate environments appropriately

## Azure DevOps

- [ ] Branch policies
- [ ] Pull requests
- [ ] Required approvals
- [ ] Service connections with least privilege
- [ ] Secret variables / secure secret stores
- [ ] Environment approvals
- [ ] Deployment history
- [ ] Artifact/image versioning

---

# 💰 60. Cost Awareness

Kubernetes and cloud infrastructure are not automatically cheap.

Think about:

```text
Cost
 │
 ├── AKS nodes
 ├── ACR
 ├── Load Balancer / Gateway
 ├── Public IP
 ├── Storage
 ├── Monitoring
 ├── Network traffic
 └── Databases / dependencies
```

For learning:

- Destroy resources when finished.
- Use small node sizes where appropriate.
- Avoid leaving development clusters running unnecessarily.
- Set budgets/alerts where appropriate.

Terraform makes cleanup straightforward:

```bash
terraform destroy
```

Use caution in shared environments.

---

# 🐛 61. Troubleshooting Guide

## Problem: Pod is Pending

Run:

```bash
kubectl describe pod <POD_NAME>
```

Look at:

```text
Events:
```

Common causes:

- Insufficient CPU/memory
- Scheduling constraints
- Node problems
- Persistent volume issues

---

## Problem: CrashLoopBackOff

Check:

```bash
kubectl logs <POD_NAME>
```

and:

```bash
kubectl describe pod <POD_NAME>
```

Typical causes:

- Application startup failure
- Missing environment variable
- Incorrect configuration
- Dependency unavailable
- Health probe failure

---

## Problem: ImagePullBackOff

Check:

```bash
kubectl describe pod <POD_NAME>
```

Typical causes:

- Wrong image name
- Wrong tag
- ACR permission problem
- Registry authentication issue
- Image does not exist

---

## Problem: Terraform plan wants to recreate resources

Check:

```bash
terraform plan
```

Investigate:

```text
~ update
-/+ replace
+ create
- destroy
```

Never blindly run:

```bash
terraform apply
```

on a production environment without understanding the plan.

---

# 🧠 62. Terraform vs ARM/Bicep

| Feature | Terraform | Bicep |
|---|---|---|
| IaC | ✅ | ✅ |
| Azure native | ❌ Multi-cloud | ✅ |
| Multi-cloud | ✅ | Limited |
| HCL | ✅ | ❌ |
| Azure Resource Manager | Via provider | Native |
| Modules | ✅ | ✅ |
| Ecosystem | Broad | Azure focused |

Use the tool that fits your organization and architecture.

---

# 🧠 63. Docker vs Kubernetes

| Docker | Kubernetes |
|---|---|
| Builds/runs containers | Orchestrates containers |
| Container runtime ecosystem | Cluster orchestration |
| Dockerfile | Deployment manifests |
| One/few containers | Many workloads |
| Local development | Production orchestration |

Simple rule:

> **Docker packages the application. Kubernetes operates the application at scale.**

---

# 🧠 64. Terraform vs Kubernetes

These tools solve different problems.

```text
Terraform
   ↓
Infrastructure
   ↓
VNet
AKS
ACR
Key Vault
Monitoring
```

Kubernetes:

```text
AKS
 ↓
Deployments
Pods
Services
Ingress
ConfigMaps
Secrets
HPA
```

They complement each other.

---

# 🧠 65. Azure DevOps vs Terraform

Azure DevOps is the **automation platform**.

Terraform is the **infrastructure provisioning tool**.

You can run Terraform from Azure DevOps:

```text
Azure DevOps Pipeline
        │
        ▼
terraform init
        │
        ▼
terraform validate
        │
        ▼
terraform plan
        │
        ▼
Approval
        │
        ▼
terraform apply
        │
        ▼
Azure
```

---

# 🌟 66. Production-Grade Delivery Model

A mature organization might implement:

```text
                         Git
                          │
             ┌────────────┴────────────┐
             ▼                         ▼
       Application                  Infra
             │                         │
             ▼                         ▼
       CI Pipeline               Terraform Plan
             │                         │
       Unit Tests                  Security
             │                         │
       Docker Build               Approval
             │                         │
       Image Scan                     ▼
             │                    Terraform
             ▼                         │
            ACR                        ▼
             │                      Azure
             ▼
          Deploy
             │
             ▼
            AKS
             │
     ┌───────┼────────┐
     ▼       ▼        ▼
    App    Metrics   Logs
             │
             ▼
        Observability
```

---

# 📊 67. Observability

Production systems need more than deployment.

You need:

### Logs

> What happened?

### Metrics

> How much / how often?

### Traces

> Where did the request spend time?

Example:

```text
User Request
     │
     ▼
Ingress
     │
     ▼
API
     │
     ├── Database
     │
     ├── Redis
     │
     └── External API
```

Distributed tracing can show latency across these components.

For Azure workloads, evaluate Azure Monitor, Application Insights, OpenTelemetry and related observability capabilities.

---

# 🧪 68. Testing Strategy

A strong pipeline should test multiple layers:

```text
Developer
   │
   ▼
Unit Tests
   │
   ▼
Integration Tests
   │
   ▼
Container Tests
   │
   ▼
Security Scans
   │
   ▼
Deploy to Test
   │
   ▼
Smoke Tests
   │
   ▼
Production
```

Do not rely only on "the container built successfully."

---

# 🔁 69. Deployment Strategies

## Rolling Deployment

Replace old Pods gradually.

```text
V1 V1 V1
 ↓
V1 V1 V2
 ↓
V1 V2 V2
 ↓
V2 V2 V2
```

## Blue/Green

```text
             Traffic
                │
        ┌───────┴───────┐
        ▼               ▼
      Blue             Green
       V1                V2
```

Switch traffic after validating V2.

## Canary

```text
100% → V1

95%  → V1
5%   → V2

75%  → V1
25%  → V2

50%  → V1
50%  → V2

0%   → V1
100% → V2
```

Choose the strategy based on risk, tooling and business requirements.

---

# 🧭 70. Learning Roadmap

## Level 1 — Beginner

Learn:

- Linux basics
- Git
- Docker
- Dockerfile
- Images
- Containers
- Ports
- Volumes
- Docker Compose

---

## Level 2 — Kubernetes

Learn:

- Pods
- Deployments
- ReplicaSets
- Services
- ConfigMaps
- Secrets
- Namespaces
- Probes
- Requests/limits
- HPA
- Ingress

---

## Level 3 — Terraform

Learn:

- HCL
- Providers
- Resources
- Variables
- Outputs
- Locals
- Data sources
- State
- Backends
- Modules
- Workspaces / environment strategies
- Import
- Plan/apply lifecycle

---

## Level 4 — Azure

Learn:

- Resource Groups
- VNet
- Subnets
- Managed Identity
- ACR
- AKS
- Key Vault
- Azure Monitor
- Application Gateway / ingress architecture

---

## Level 5 — Azure DevOps

Learn:

- Repositories
- YAML pipelines
- Stages
- Jobs
- Tasks
- Artifacts
- Environments
- Approvals
- Service connections
- Variables
- Secure files/secrets
- Deployment strategies

---

## Level 6 — Production Engineering

Learn:

- Security
- Networking
- Observability
- Disaster recovery
- High availability
- Autoscaling
- Cost optimization
- GitOps
- Policy as Code
- DevSecOps
- Platform engineering

---

# 🎤 71. Interview Questions

## Docker

### Q1. What is the difference between an image and a container?

**Answer:**

An image is an immutable package/template containing application code and dependencies. A container is a running instance of that image.

---

### Q2. Why use multi-stage Docker builds?

**Answer:**

To separate build dependencies from runtime dependencies, producing smaller and cleaner production images with a reduced attack surface.

---

## Kubernetes

### Q3. What is a Pod?

A Pod is Kubernetes' smallest deployable unit and can contain one or more tightly coupled containers.

### Q4. Why do we need Services?

Because Pods are ephemeral and their IP addresses can change. Services provide stable networking and load distribution to selected Pods.

### Q5. Deployment vs Pod?

A Pod represents running workload units. A Deployment manages the desired number and rollout lifecycle of Pods.

---

## Terraform

### Q6. What is Terraform state?

Terraform state records the relationship between Terraform configuration and managed infrastructure so Terraform can calculate changes.

### Q7. Why use remote state?

For team collaboration, centralized state management, access control and safer concurrent workflows.

### Q8. What is `terraform plan`?

It previews the changes Terraform proposes before they are applied.

---

## Azure DevOps

### Q9. What is CI/CD?

CI continuously integrates and validates changes. CD automates delivery/deployment of validated software.

### Q10. Why use YAML pipelines?

Pipeline configuration becomes version-controlled, reviewable and reproducible.

---

# 🧠 72. Architecture Interview Question

> **How would you deploy a .NET microservices application to Azure using Docker, Kubernetes, Terraform and Azure DevOps?**

A strong answer:

```text
1. Developers push code to Git.

2. Azure DevOps pipeline starts.

3. Restore, build and unit tests execute.

4. Docker creates immutable application images.

5. Security scanning runs.

6. Image is tagged with a unique build/Git identifier.

7. Image is pushed to Azure Container Registry.

8. Terraform manages Azure infrastructure such as:
   - Resource Group
   - Networking
   - ACR
   - AKS
   - Identity
   - Monitoring

9. Kubernetes manifests/Helm define application workloads.

10. Pipeline deploys the desired application version to AKS.

11. Readiness/liveness probes validate workload health.

12. HPA can scale Pods based on demand.

13. Monitoring and logs provide observability.

14. Production deployments use approvals,
    security controls and controlled rollout strategies.
```

---

# 🚨 73. Common Beginner Mistakes

### ❌ Mistake 1

Using:

```text
latest
```

everywhere.

### Better

Use immutable versions:

```text
1.0.0
1.0.1
<git-sha>
```

---

### ❌ Mistake 2

Putting passwords in Git.

### Better

Use:

```text
Azure Key Vault
Managed Identity
Secure pipeline variables
Kubernetes secret-management integrations
```

---

### ❌ Mistake 3

No resource limits.

### Better

Define:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

---

### ❌ Mistake 4

No health checks.

### Better

Configure:

```text
Readiness
Liveness
Startup where appropriate
```

---

### ❌ Mistake 5

Running Terraform directly from a laptop in production.

### Better

Use a controlled workflow:

```text
Pull Request
    ↓
terraform fmt
    ↓
terraform validate
    ↓
terraform plan
    ↓
Review / Approval
    ↓
terraform apply
```

---

# 🌈 74. The Complete Mental Model

If you remember only one diagram, remember this:

```text
                         ☁️ CLOUD
                           │
                     ┌─────▼─────┐
                     │ Terraform │
                     │   IaC     │
                     └─────┬─────┘
                           │
           ┌───────────────┼────────────────┐
           ▼               ▼                ▼
          VNet            ACR              AKS
                                            │
                                            ▼
                                      Kubernetes
                                            │
                                ┌───────────┼───────────┐
                                ▼           ▼           ▼
                              Pod         Pod         Pod
                                │           │           │
                                └───────────┼───────────┘
                                            ▼
                                        Service
                                            │
                                            ▼
                                          Users

Developer
    │
    ▼
Git
    │
    ▼
Azure DevOps
    │
    ├── Build
    ├── Test
    ├── Docker
    ├── Scan
    ├── Push → ACR
    └── Deploy → AKS
```

---

# 🔗 75. Official Documentation

## Terraform

- [Terraform Documentation](https://developer.hashicorp.com/terraform/docs)
- [Terraform Introduction](https://developer.hashicorp.com/terraform/intro)
- [Terraform Installation](https://developer.hashicorp.com/terraform/install)
- [Terraform Azure Tutorials](https://developer.hashicorp.com/terraform/tutorials/azure-get-started)
- [Terraform Docker Tutorials](https://developer.hashicorp.com/terraform/tutorials/docker-get-started)
- [Terraform Language](https://developer.hashicorp.com/terraform/language)

## Docker

- [Docker Documentation](https://docs.docker.com/)
- [Docker Get Started](https://docs.docker.com/get-started/)
- [Dockerfile Reference](https://docs.docker.com/reference/dockerfile/)
- [Docker Compose](https://docs.docker.com/compose/)

## Kubernetes

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Kubernetes Concepts](https://kubernetes.io/docs/concepts/)
- [Kubernetes Tutorials](https://kubernetes.io/docs/tutorials/)
- [kubectl Reference](https://kubernetes.io/docs/reference/kubectl/)

## Azure Kubernetes Service

- [AKS Documentation](https://learn.microsoft.com/azure/aks/)
- [AKS + Terraform Quickstart](https://learn.microsoft.com/azure/aks/learn/quick-kubernetes-deploy-terraform)
- [Production AKS with Terraform / Azure Verified Modules](https://learn.microsoft.com/azure/aks/deploy-cluster-terraform-verified-module)

## Azure Container Registry

- [Azure Container Registry Documentation](https://learn.microsoft.com/azure/container-registry/)

## Azure DevOps

- [Azure DevOps Documentation](https://learn.microsoft.com/azure/devops/)
- [Azure Pipelines](https://learn.microsoft.com/azure/devops/pipelines/)
- [Deploy to AKS with Azure Pipelines](https://learn.microsoft.com/azure/devops/pipelines/ecosystems/kubernetes/aks-template)
- [Deploy to Kubernetes](https://learn.microsoft.com/azure/devops/pipelines/ecosystems/kubernetes/deploy)
- [Service Connections](https://learn.microsoft.com/azure/devops/pipelines/library/service-endpoints)

## Azure CLI

- [Azure CLI Documentation](https://learn.microsoft.com/cli/azure/)

---

# 🧹 76. Cleanup

For a local Docker environment:

```bash
docker compose down
```

Remove unused Docker resources carefully:

```bash
docker system prune
```

For Kubernetes:

```bash
kubectl delete -f k8s/
```

For Terraform-managed infrastructure:

```bash
terraform destroy
```

⚠️ **Never run destructive commands against production without verifying the target subscription, environment and Terraform plan.**

---

# 🏆 77. Final Summary

The four technologies solve different problems:

| Technology | Main Question |
|---|---|
| 🐳 Docker | **How do I package my application?** |
| ☸️ Kubernetes | **How do I run and operate containers reliably at scale?** |
| 🏗️ Terraform | **How do I create and manage infrastructure as code?** |
| 🔄 Azure DevOps | **How do I automate build, test and deployment?** |

Together:

```text
                 SOFTWARE DELIVERY
                       │
                       ▼
                 👨‍💻 Source Code
                       │
                       ▼
                 🔄 Azure DevOps
                       │
              ┌────────┴────────┐
              ▼                 ▼
          Build/Test        Docker Build
                                │
                                ▼
                               ACR
                                │
                                ▼
                               AKS
                                │
                                ▼
                           Kubernetes
                                │
                                ▼
                              Users

                   INFRASTRUCTURE
                         ▲
                         │
                      Terraform
                         │
            ┌────────────┼────────────┐
            ▼            ▼            ▼
           VNet         ACR          AKS
```

> **The goal is not to memorize commands.**
>
> Understand the responsibilities:
>
> **Terraform builds the environment.**  
> **Docker packages the application.**  
> **ACR stores the package.**  
> **Kubernetes runs and manages it.**  
> **Azure DevOps automates the journey from Git to production.**

---

# ⭐ If This Guide Helped You

Give the repository a ⭐ and share it with other engineers learning:

- Cloud
- DevOps
- Azure
- Kubernetes
- Terraform
- Docker
- CI/CD
- Cloud-Native Architecture

---

## 📌 Suggested Repository Tags

```text
terraform
docker
kubernetes
azure
azure-devops
azure-pipelines
aks
acr
iac
infrastructure-as-code
devops
cicd
cloud-native
microservices
containers
helm
devsecops
cloud-architecture
dotnet
dotnet-core
solution-architecture
```

---

## 📣 Suggested GitHub Repository Description

> 🚀 Beginner-friendly, practical guide to Terraform, Docker, Kubernetes, AKS and Azure DevOps — with real-world analogies, hands-on examples, colorful architecture diagrams, CI/CD pipelines and production-ready cloud-native patterns.

---

## 📝 Note About Diagrams

This article uses **GitHub-compatible Mermaid diagrams** where supported. Mermaid styling can provide colorful architecture diagrams directly inside Markdown. GitHub does not generally allow arbitrary CSS/JavaScript animations inside repository Markdown, so diagrams should remain portable and safe rather than relying on custom browser-side animation.

---

**Happy Learning! 🚀**

**Code → Container → Cluster → Cloud → Continuous Delivery**
