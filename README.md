# Kubernetes Multi-Node Cluster Lab

A hands-on Kubernetes laboratory project demonstrating multi-node cluster configuration, NGINX deployment, and application scaling using **Kind, Docker Desktop, and kubectl on Windows**.

## Overview

This project explores the fundamental operations of a Kubernetes cluster in a local development environment. The cluster is configured with one control-plane node and two worker nodes.

The experiment demonstrates how to inspect cluster resources, deploy a containerized web application, scale application replicas, and examine Kubernetes workloads and events.

## Objectives

- Understand the architecture of a multi-node Kubernetes cluster.
- Configure a local cluster using Kind.
- Inspect cluster nodes and Kubernetes system components.
- Deploy an NGINX application using a Kubernetes Deployment.
- Scale the application from three replicas to six replicas.
- Inspect Pod status, node distribution, Deployment details, and Kubernetes events.

## Technology Stack

| Technology | Purpose |
|---|---|
| Windows | Host operating system |
| WSL 2 | Linux environment support for Docker Desktop |
| Docker Desktop | Container runtime environment |
| Kind | Creates a local Kubernetes cluster |
| kubectl | Interacts with Kubernetes resources |
| Kubernetes | Container orchestration |
| NGINX | Sample web server application |
| YAML | Cluster and application configuration |

## Cluster Architecture

The cluster contains three nodes:

- **Control-plane node:** Coordinates cluster operations and manages the desired state of resources.
- **Worker node 1:** Runs scheduled application workloads.
- **Worker node 2:** Runs scheduled application workloads.

Kind runs the Kubernetes nodes as Docker containers.

![Kubernetes multi-node cluster architecture](docs/architecture.png)

## Repository Structure

```text
kubernetes-multi-node-cluster-lab/
├── config/
│   └── kind-config.yaml
├── manifests/
│   └── web-deployment.yaml
├── screenshots/
│   ├── 01-cluster-nodes.png
│   ├── 02-system-pods.png
│   ├── 03-nginx-3-replicas.png
│   ├── 04-nginx-6-replicas.png
│   ├── 05-nginx-six-running-pods.png
│   ├── 06-deployment-details.png
│   ├── 07-pod-distribution.png
│   └── 08-kubernetes-events.png
├── docs/
│   ├── architecture.png
│   ├── experiment-report.md
│   ├── command-reference.md
│   └── troubleshooting.md
├── .gitignore
└── README.md
```

*Note: This structure describes the intended final organization. Ensure the files are actually located at these paths in GitHub.*

## Experiment Workflow

### 1. Verify the Environment

Verify Docker, Kind, and kubectl installations and confirm that Docker can run a test container.

### 2. Configure and Create the Cluster

Configure one control-plane node and two worker nodes, then create the cluster using Kind.

```powershell
kind create cluster --config kind-config.yaml
```

Verify the cluster:

```powershell
kubectl cluster-info --context kind-kind
kubectl get nodes
```

### 3. Inspect System Components

Inspect the Pods running in the Kubernetes system namespace.

```powershell
kubectl get pods -n kube-system -o wide
```

### 4. Deploy NGINX

Create a Deployment named `web` with three replicas.

```powershell
kubectl create deployment web --image=nginx --replicas=3
```

Check the Deployment and Pods:

```powershell
kubectl get deployments
kubectl get pods -o wide
```

### 5. Scale the Application

Increase the desired number of replicas from three to six.

```powershell
kubectl scale deployment web --replicas=6
```

Verify the resulting Pods:

```powershell
kubectl get pods -o wide
```

### 6. Inspect Cluster Activity

Review Deployment details, Pod distribution, and Kubernetes events using the commands documented in the command reference.

## Results

The recorded lab evidence covers the following activities:

- Inspection of the three-node cluster.
- Inspection of Kubernetes system Pods.
- NGINX deployment with three replicas.
- Scaling the deployment to six replicas.
- Inspection of running Pods and their node distribution.
- Examination of Deployment details and Kubernetes events.

Refer to the `screenshots/` directory for the recorded execution evidence.

## Documentation

| Document | Description |
|---|---|
| [Experiment Report](docs/experiment-report.md) | Aim, objectives, architecture, procedure, observations, and learning outcomes |
| [Command Reference](docs/command-reference.md) | Commands and their purposes |
| [Troubleshooting Guide](docs/troubleshooting.md) | Common setup and Kubernetes errors |
| [Cluster Architecture](docs/architecture.png) | Visual representation of the cluster |

## Additional Deployment Manifest

The file `manifests/web-deployment.yaml` provides a reusable YAML definition for the NGINX Deployment.

The original lab procedure created the initial Deployment using `kubectl create deployment`. The manifest is included as an additional configuration artifact.

## Learning Outcomes

This laboratory provides practical exposure to:

- Kubernetes cluster architecture.
- Control-plane and worker-node roles.
- Containerized application deployment.
- Deployment replica management and scaling.
- Inspection of Pods, nodes, and cluster events.
- Configuration and documentation of a reproducible lab environment.

## Author

**GitHub:** [shettisrushti09-sketch](https://github.com/shettisrushti09-sketch)

---

*Academic laboratory project: Kubernetes multi-node cluster setup and application scaling.*
