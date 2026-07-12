
# 🚀 Automated OpenShift Deployment Platform Using GitHub Actions and Kustomize

![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker\&logoColor=white)
![OpenShift](https://img.shields.io/badge/OpenShift-Container_Platform-EE0000?logo=redhatopenshift\&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?logo=kubernetes\&logoColor=white)
![Kustomize](https://img.shields.io/badge/Kustomize-Kubernetes_Configuration-326CE5?logo=kubernetes\&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?logo=githubactions\&logoColor=white)

A complete DevOps automation pipeline that builds container images using GitHub Actions and automatically deploys applications to an OpenShift cluster using Kustomize.

---

# 📖 Overview

Modern cloud-native application delivery requires automated and reliable deployment processes that reduce manual operations and improve software delivery speed.

Traditional deployment approaches often require engineers to manually:

* Build Docker images.
* Push images to container registries.
* Authenticate into Kubernetes/OpenShift clusters.
* Apply YAML manifests.
* Update application configurations.
* Verify application deployments.

These manual processes increase the risk of configuration errors and slow down development teams.

This project demonstrates a complete Continuous Integration and Continuous Deployment (CI/CD) workflow that automates the entire application delivery process.

The pipeline uses:

* **Docker** for containerizing applications.
* **GitHub Actions** for CI/CD automation.
* **Kustomize** for Kubernetes/OpenShift configuration management.
* **OpenShift** as the application deployment platform.

Whenever code changes are pushed to the repository, GitHub Actions automatically builds the Docker image, installs the required deployment tools, authenticates with OpenShift, and deploys the application using Kustomize.

This project demonstrates practical DevOps and Platform Engineering concepts including automation, containerization, declarative deployment, and cloud-native application management.

---

# 🎯 Project Objectives

The main objectives of this project are:

* Automate application deployment to OpenShift.
* Eliminate manual `oc apply` deployment processes.
* Implement a complete CI/CD pipeline using GitHub Actions.
* Use Kustomize for reusable Kubernetes/OpenShift configurations.
* Automate Docker image creation and publishing.
* Demonstrate secure OpenShift cluster authentication.
* Create a repeatable and reliable deployment workflow.
* Apply modern DevOps best practices.

---

# 💼 Business Problem

Many development teams still rely on manual deployment processes, creating several challenges:

| Challenge                     | Impact                                 |
| ----------------------------- | -------------------------------------- |
| Manual Docker builds          | Slow application delivery              |
| Manual OpenShift deployments  | Human errors and inconsistent releases |
| Large duplicated YAML files   | Difficult configuration management     |
| Manual cluster authentication | Operational overhead                   |
| Environment differences       | Configuration drift                    |
| Lack of deployment automation | Slower development cycles              |

These challenges reduce productivity and make application delivery less reliable.

---

# ✅ Solution

This project implements an automated deployment platform that creates a complete CI/CD workflow.

The solution automatically performs:

1. Source code checkout.
2. Docker image build.
3. Container image publishing.
4. Kustomize installation.
5. OpenShift authentication.
6. Kubernetes/OpenShift manifest generation.
7. Application deployment.
8. Deployment validation.

The result is a consistent, automated, and repeatable deployment process.

---

# ⭐ Key Features

## 🔄 Continuous Integration

The pipeline automatically:

* Checks out application source code.
* Builds Docker images.
* Validates the container build.
* Publishes images to a container registry.

---

## 🚀 Continuous Deployment

The deployment pipeline provides:

* Automated OpenShift authentication.
* Automated Kustomize installation.
* Declarative application deployment.
* Kubernetes resource management.
* Automatic application updates.

---

## ☸️ Kubernetes/OpenShift Management

The project manages:

* Deployments.
* Services.
* Routes.
* Configurations.
* Application replicas.
* Container workloads.

---

## 📦 Kustomize Configuration Management

Kustomize provides:

* Reusable Kubernetes manifests.
* Environment-specific configuration.
* Cleaner YAML management.
* Reduced configuration duplication.

---

## 🔐 Secure Deployment

Security practices include:

* GitHub encrypted secrets.
* Secure OpenShift authentication.
* Protected container registry credentials.
* No credentials stored in source code.

---

## 🐳 Containerization

The application is packaged using Docker to provide:

* Consistent runtime environments.
* Portable deployments.
* Simplified application delivery.
* Cloud-native deployment compatibility.

---
# 🏗️ High-Level Architecture
![Achitectural Diagram](https://github.com/smogalloyubio/Openshift-platform-project-02/blob/main/Achitecturaldiagram/Openshiftcluster.jpg)
---

# 🧩 System Components

| Component            | Purpose                             |
| -------------------- | ----------------------------------- |
| GitHub Repository    | Source code management              |
| GitHub Actions       | CI/CD automation                    |
| Docker               | Container image creation            |
| Container Registry   | Image storage                       |
| Kustomize            | Kubernetes configuration management |
| OpenShift            | Application runtime platform        |
| OpenShift CLI (`oc`) | Cluster operations                  |

---


# 🛠️ Technology Stack

This project uses modern cloud-native and DevOps technologies to automate application delivery from source code to a running workload on OpenShift.

| Category                 | Technology           | Purpose                                   |
| ------------------------ | -------------------- | ----------------------------------------- |
| Containerization         | Docker               | Build and package application containers  |
| CI/CD                    | GitHub Actions       | Automate build and deployment workflow    |
| Container Platform       | Red Hat OpenShift    | Run and manage containerized applications |
| Orchestration            | Kubernetes           | Application workload management           |
| Configuration Management | Kustomize            | Manage Kubernetes/OpenShift manifests     |
| CLI Tools                | OpenShift CLI (`oc`) | Authenticate and interact with OpenShift  |
| Version Control          | Git & GitHub         | Source code management                    |
| Configuration            | YAML                 | Define Kubernetes resources               |

---

# 📂 Project Structure

The repository follows a DevOps-friendly structure separating application code, container configuration, Kubernetes manifests, and CI/CD automation.

```text
OpenShift-platform-project-02
│
├── .github/
│   └── workflows/
│       └── deployment.yaml
│
├── k8s/
│   │
│   ├── base/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   ├── route.yaml
│   │   └── kustomization.yaml
│   │
│   └── overlays/
│       │
│       ├── dev/
│       │   ├── kustomization.yaml
│       │   └── patches/
│       │
│       └── prod/
│           ├── kustomization.yaml
│           └── patches/
│
├── Dockerfile
│
├── application/
│
├── requirements.txt
│
└── README.md
```

---

# 📁 Repository Components

| Directory/File       | Description                                               |
| -------------------- | --------------------------------------------------------- |
| `.github/workflows/` | Contains GitHub Actions CI/CD pipeline definitions        |
| `Dockerfile`         | Instructions for building the application container image |
| `k8s/base/`          | Base Kubernetes/OpenShift resources                       |
| `k8s/overlays/`      | Environment-specific configurations                       |
| `kustomization.yaml` | Defines Kustomize resources and transformations           |
| Application source   | Contains application code                                 |
| `requirements.txt`   | Application dependencies                                  |

---

# 📋 Prerequisites

Before deploying this project, ensure the following tools are available.

## Required Tools

| Tool                 | Purpose                               |
| -------------------- | ------------------------------------- |
| Git                  | Clone and manage repository           |
| Docker               | Build container images                |
| GitHub Account       | Store code and execute pipelines      |
| OpenShift Cluster    | Application deployment platform       |
| OpenShift CLI (`oc`) | Cluster authentication and management |
| Kustomize            | Kubernetes configuration management   |

---

# 🚀 Installation

## Step 1 — Clone the Repository

Clone the project:

```bash
git clone https://github.com/smogalloyubio/Openshift-platform-project-02.git
```

Navigate into the project directory:

```bash
cd Openshift-platform-project-02
```

---

# 🐳 Step 2 — Build Docker Image Locally (Optional)

Before using the automated pipeline, the Docker image can be tested locally.

Build the image:

```bash
docker build -t openshift-platform-app .
```

Verify the image:

```bash
docker images
```

Run the container:

```bash
docker run -p 8080:8080 openshift-platform-app
```

Test the application:

```text
http://localhost:8080
```

---

# ⚙️ Configuration

The deployment process requires access to:

* Container registry credentials.
* OpenShift cluster credentials.
* Deployment configuration.

Configuration values are managed securely through GitHub Actions Secrets.

---

# 🔐 GitHub Actions Secrets

The pipeline uses GitHub encrypted secrets to securely authenticate with external services.
Required secrets:

| Secret              | Purpose                        |
| ------------------- | ------------------------------ |
| `OPENSHIFT_SERVER`  | OpenShift API endpoint         |
| `OPENSHIFT_TOKEN`   | OpenShift authentication token |
| `REGISTRY_USERNAME` | Container registry username    |
| `REGISTRY_PASSWORD` | Container registry password    |

---

# 🔑 OpenShift Authentication

The GitHub Actions workflow securely authenticates into OpenShift using the provided token.

Example:

```bash
oc login \
--server=$OPENSHIFT_SERVER \
--token=$OPENSHIFT_TOKEN
```

After authentication, the pipeline can execute OpenShift deployment commands.

---

# 🎯 Namespace Configuration

The deployment targets a specific OpenShift namespace/project.

Example:

```bash
oc project my-project
```

Verify the active project:

```bash
oc project
```

---

# 🧩 Kustomize Configuration

Kustomize is used to maintain Kubernetes/OpenShift resources in a clean and reusable way.

Instead of managing multiple copies of YAML files, Kustomize allows the project to maintain:

* Common base resources.
* Environment-specific overlays.
* Configuration patches.
* Image updates.

Example structure:

```text
k8s/

├── base/
│
│   deployment.yaml
│   service.yaml
│   route.yaml
│
└── overlays/

    ├── dev/

    └── prod/
```

---

# Why Kustomize?

Using Kustomize provides several advantages:

| Traditional YAML Management      | Kustomize Approach          |
| -------------------------------- | --------------------------- |
| Duplicate manifests              | Reusable base configuration |
| Manual image updates             | Automated image replacement |
| Difficult environment management | Overlay-based configuration |
| Configuration drift              | Consistent deployments      |

---

# ▶️ Running Kustomize Locally

Validate the generated Kubernetes/OpenShift manifests:

```bash
kustomize build k8s/overlays/dev
```

Preview the deployment:

```bash
kustomize build k8s/overlays/dev | less
```

Apply manually:

```bash
kustomize build k8s/overlays/dev | oc apply -f -
```

---

# ✅ Deployment Validation

After deployment, verify the resources:

Check Pods:

```bash
oc get pods
```

Check Services:

```bash
oc get svc
```

Check Routes:

```bash
oc get routes
```

Check Deployment status:

```bash
oc get deployment
```

---

# Application Health Verification

Confirm that:

* Pods are running.
* Services are created.
* Routes are accessible.
* Containers start successfully.
* Application logs show no errors.

View logs:

```bash
oc logs deployment/<deployment-name>
```

---

