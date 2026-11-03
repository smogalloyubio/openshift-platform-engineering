
# OpenShift Platform Engineering: Automated CI/CD and GitOps Deployment

![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker&logoColor=white)
![OpenShift](https://img.shields.io/badge/OpenShift-Container_Platform-EE0000?logo=redhatopenshift&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?logo=kubernetes&logoColor=white)
![Kustomize](https://img.shields.io/badge/Kustomize-Configuration_Management-326CE5?logo=kubernetes&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?logo=githubactions&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo_CD-GitOps-EF7B4D?logo=argo&logoColor=white)
![Quay](https://img.shields.io/badge/Quay-Container_Registry-2A7AE2?logo=redhat&logoColor=white)

## Overview

This project demonstrates an automated cloud-native application delivery workflow using GitHub Actions, Docker, Quay.io, Kustomize, Argo CD and Red Hat OpenShift.

The application is a Python Flask-based cryptocurrency dashboard that exposes REST API endpoints for cryptocurrency information, historical price data, market statistics and application health.

The project demonstrates how application source code can move through a CI/CD pipeline, be packaged into a container image, scanned for vulnerabilities, published to a container registry and deployed to an OpenShift environment.

It also explores GitOps practices through Argo CD and environment-specific Kubernetes configuration using Kustomize.

## Project Goals

- Automate application testing and container image creation.
- Implement CI/CD using GitHub Actions.
- Scan application dependencies and container images with Trivy.
- Publish container images to Quay.io.
- Deploy containerized workloads to OpenShift.
- Manage reusable Kubernetes manifests using Kustomize.
- Explore GitOps deployment using Argo CD.
- Separate development, staging and production configurations.
- Demonstrate secure handling of deployment credentials.

## Architecture

![OpenShift Architecture](Achitecturaldiagram/Openshiftcluster.jpg)

### Application delivery workflow

1. A developer pushes application changes to GitHub.
2. GitHub Actions checks out the source code.
3. Python 3.12 is configured and application dependencies are installed.
4. Pytest executes the application tests.
5. Trivy scans the repository filesystem for vulnerabilities.
6. Docker Buildx builds the application image.
7. Trivy scans the built image.
8. The image is published to Quay.io.
9. The deployment workflow authenticates to OpenShift using GitHub Actions secrets.
10. Kustomize is used to prepare the Kubernetes manifests.
11. OpenShift receives the application resources.
12. The deployment rollout is checked.

Argo CD configuration is also included to demonstrate declarative GitOps management of development, staging and production applications.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.12 | Application runtime |
| Flask | Web application and REST API |
| Pytest | Application testing |
| Docker | Container image creation |
| GitHub Actions | CI/CD automation |
| Trivy | Vulnerability scanning |
| Quay.io | Container image registry |
| Kubernetes | Container orchestration |
| Red Hat OpenShift | Application platform |
| Kustomize | Manifest customization |
| Argo CD | GitOps continuous delivery |
| YAML | Infrastructure and application configuration |

## Repository Structure

```text
openshift-platform-engineering/
│
├── .github/
│   └── workflows/
│       └── docker-image.yml
│
├── Achitecturaldiagram/
│   └── Openshiftcluster.jpg
│
├── argocd/
│   └── argocd-project.yaml
│
├── argocdApplication/
│   └── argocdapplication.yaml
│
├── kustomized/
│   ├── base/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── kustomization.yaml
│   │
│   └── overlay/
│       ├── dev/
│       │   └── kustomization.yaml
│       ├── stage/
│       │   └── kustomization.yaml
│       └── prod/
│           └── kustomization.yaml
│
├── mysql-deploy/
│   ├── argocd.yaml
│   └── mysqldeployment.yaml
│
├── static/
│   ├── css/
│   │   └── main.css
│   └── js/
│       └── main.js
│
├── templates/
│   └── index.html
│
├── tests/
│   └── test_app.py
│
├── app.py
├── Dockerfile
├── requirements.txt
├── mysql-sealed-secret.yaml
└── README.md
```

## Application Components

### 1. Flask Application

The application is implemented in `app.py` using Flask.

It provides the following endpoints:

| Endpoint | Description |
|---|---|
| `/` | Renders the cryptocurrency dashboard. |
| `/api/crypto` | Returns simulated cryptocurrency market data. |
| `/api/crypto/<coin_id>/history` | Returns generated historical price data. |
| `/api/stats` | Returns market statistics. |
| `/health` | Returns application health information. |

**Important:** The cryptocurrency information is simulated using Python's random number generation. It is not a live financial market data integration.

### 2. Docker Containerization

The Dockerfile packages the Flask application into a Python 3.12 container.

Build the image locally:

```bash
docker build -t mypython-app:latest .
```

Run the container:

```bash
docker run -d \
  --name mypython-app \
  -p 5000:5000 \
  mypython-app:latest
```

Test the application:

```bash
curl http://localhost:5000/health
```

Expected response:

```json
{
  "status": "healthy",
  "timestamp": 1234567890
}
```

### 3. GitHub Actions CI/CD

The workflow is defined in:

```text
.github/workflows/docker-image.yml
```

It is configured for pushes to `main` and `develop`, and pull requests targeting `main`.

The workflow contains four jobs.

**Test**

- Checks out the source code.
- Configures Python 3.12.
- Installs dependencies from `requirements.txt`.
- Executes the Pytest suite.

```bash
pytest tests/ -v --tb=short
```

**Scan Docker**

- Runs after successful tests.
- Uses Trivy filesystem scanning.
- Checks for HIGH and CRITICAL vulnerabilities.

**Build**

- Builds the Docker image using Docker Buildx.
- Uses Quay.io as the image registry.
- Scans the built image with Trivy.
- Publishes the image to Quay.io.

The configured image repository is:

```text
quay.io/ubiowororuki/mypython-app
```

**Deploy**

- Installs the OpenShift CLI.
- Authenticates to the OpenShift API.
- Updates the image reference.
- Applies Kubernetes resources.
- Checks the deployment rollout.

The deployment commands require a working Kustomize installation and a valid Kustomize build target.

### 4. Kustomize Configuration

The project separates common resources from environment-specific configuration.

**Base configuration**

```text
kustomized/base/
```

Contains:

- `deployment.yaml`
- `service.yaml`
- `kustomization.yaml`

The Deployment defines four replicas by default and uses the Quay.io application image. The Service exposes port 5000.

**Environment overlays**

```text
kustomized/overlay/
├── dev/
├── stage/
└── prod/
```

The overlays customize namespace, resource names and replica counts.

| Environment | Namespace | Replicas |
|---|---|---:|
| Development | dev | 2 |
| Staging | stage | 4 |
| Production | prod | 4 |

These are the values declared in the overlay manifests.

Build an individual overlay:

```bash
kustomize build kustomized/overlay/dev
```

```bash
kustomize build kustomized/overlay/stage
```

```bash
kustomize build kustomized/overlay/prod
```

Review the rendered manifests before applying them:

```bash
kustomize build kustomized/overlay/dev
```

Apply an environment after confirming the configuration:

```bash
kustomize build kustomized/overlay/dev | oc apply -f -
```

### 5. Argo CD GitOps Configuration

The repository includes Argo CD Project definitions in:

```text
argocd/argocd-project.yaml
```

It also contains Application definitions in:

```text
argocdApplication/argocdapplication.yaml
```

The configuration defines three applications:

- `app-dev`
- `app-stage`
- `app-prod`

Each application references an environment-specific Kustomize overlay.

The development and staging applications declare automated synchronization with pruning and self-healing enabled.

Production declares automated synchronization with pruning and self-healing disabled.

The Argo CD configuration also defines project-level source repository restrictions, destination namespaces and resource permissions.

Before deploying these definitions, verify that their configured Git repository URL matches this repository and that the Argo CD Projects and namespaces exist or can be created.

### 6. MySQL Deployment and Secret Management

The repository contains a separate MySQL deployment:

```text
mysql-deploy/
├── argocd.yaml
└── mysqldeployment.yaml
```

The MySQL workload uses MySQL 8.0 and exposes port 3306 through a Kubernetes Service.

Its environment variables reference Kubernetes Secret keys:

- `mysql-root-password`
- `mysql-db`
- `mysql-user`
- `mysql-password`

The repository also contains:

```text
mysql-sealed-secret.yaml
```

This is intended to support encrypted secret management using Bitnami Sealed Secrets.

The SealedSecret controller must be installed and configured in the target cluster. The encrypted resource must be compatible with the controller's sealing key.

For production use, MySQL should also have persistent storage, resource requests and limits, appropriate access controls and backup procedures. These should be verified or added before treating the database deployment as production-ready.

## Prerequisites

Before deploying the project, prepare:

- Git and GitHub account.
- Docker.
- Python 3.12.
- OpenShift cluster access.
- OpenShift CLI (`oc`).
- Kustomize.
- Quay.io account and registry permissions.
- GitHub Actions enabled.
- Argo CD installed if using the GitOps configuration.
- Sealed Secrets controller installed if using the SealedSecret manifest.

## Configuration: GitHub Actions Secrets

Configure the following repository secrets:

| Secret | Purpose |
|---|---|
| `QUAY_USERNAME` | Quay.io registry username |
| `QUAY_TOKEN` | Quay.io authentication token |
| `OPENSHIFT_SERVER` | OpenShift API endpoint |
| `OPENSHIFT_TOKEN` | OpenShift service account or deployment token |

Do not commit access tokens, passwords or other credentials to the repository.

The OpenShift identity used by CI/CD should have only the permissions required to deploy and verify the application in its target namespace.

## Local Installation and Testing

Clone the repository:

```bash
git clone https://github.com/smogalloyubio/openshift-platform-engineering.git
```

Enter the project directory:

```bash
cd openshift-platform-engineering
```

Create a Python virtual environment:

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run tests:

```bash
pytest tests/ -v
```

Start the application:

```bash
python app.py
```

Open:

```text
http://localhost:5000
```

## OpenShift Deployment Verification

After a successful deployment, inspect the application resources:

```bash
oc get pods -n ubiowororuki-dev
```

```bash
oc get deployments -n ubiowororuki-dev
```

```bash
oc get services -n ubiowororuki-dev
```

Check the deployment rollout:

```bash
oc rollout status deployment/mypython-app \
  -n ubiowororuki-dev
```

Inspect application logs:

```bash
oc logs deployment/mypython-app \
  -n ubiowororuki-dev
```

Test the health endpoint through an appropriate OpenShift-accessible service or route.

## Security Considerations

This project demonstrates several security-related practices:

- GitHub Actions encrypted secrets for external credentials.
- Trivy filesystem vulnerability scanning.
- Trivy container image vulnerability scanning.
- Quay.io container image storage.
- Sealed Secrets configuration for encrypted Kubernetes secret management.
- OpenShift namespace-based workload deployment.

For a stronger production implementation, consider:

- Pinning GitHub Actions to verified commit SHAs.
- Using a verified OpenShift TLS certificate rather than disabling TLS verification.
- Building and deploying immutable image tags or digests.
- Enforcing least-privilege RBAC.
- Adding persistent storage and backup policies for MySQL.
- Running containers as non-root where compatible.
- Adding image signing and provenance verification.
- Adding resource requests, limits and readiness/liveness probes.
- Validating all deployment manifests before applying them.

## Troubleshooting

| Problem | What to check |
|---|---|
| GitHub Actions test failure | Python dependencies and Pytest output. |
| Quay authentication failure | `QUAY_USERNAME`, `QUAY_TOKEN` and registry permissions. |
| Trivy scan failure | Vulnerability report and configured severity threshold. |
| OpenShift login failure | API URL, token permissions and cluster connectivity. |
| Kustomize build failure | Kustomize installation, file paths and manifest structure. |
| Image pull failure | Image name, tag and registry pull permissions. |
| Pod not starting | `oc describe pod` and container logs. |
| Argo CD application out of sync | Repository URL, target revision, overlay path and sync policy. |
| MySQL startup failure | Secret keys, database configuration and persistent storage requirements. |

## Conclusion

This project demonstrates a practical cloud-native delivery workflow built around OpenShift.

It brings together application testing, containerization, vulnerability scanning, image publishing, declarative Kubernetes configuration and GitOps deployment concepts.

The project provides a foundation for exploring how platform and DevOps engineers can standardize application delivery, reduce manual deployment operations and improve consistency across multiple environments.

**Repository:** https://github.com/smogalloyubio/openshift-platform-engineering
