# Kubernetes Multi-Node Cluster Lab

## 1. Experiment Title

Building a Three-Node Kubernetes Cluster Using Kind and Deploying an NGINX Application.

## 2. Aim

To create a multi-node Kubernetes cluster on Windows using Kind, deploy an NGINX application, scale the deployment, and observe how Kubernetes manages application Pods across the cluster.

## 3. Objectives

- Understand the basic architecture of Kubernetes.
- Create a three-node Kubernetes cluster using Kind.
- Identify the roles of the control-plane and worker nodes.
- Inspect Kubernetes system components and Pods.
- Deploy an NGINX application.
- Scale the application from three replicas to six replicas.
- Observe Pod distribution and Kubernetes events.

## 4. Software and Tools Required

The experiment uses the following tools:

- **Windows 10/11:** Host operating system.
- **WSL 2:** Provides the Linux environment required by Docker Desktop.
- **Docker Desktop:** Runs the Kubernetes nodes as containers.
- **Kind:** Creates and manages the local Kubernetes cluster.
- **kubectl:** Command-line tool used to communicate with the Kubernetes cluster.
- **NGINX:** Web server application deployed inside the cluster.
- **PowerShell:** Terminal used to execute the lab commands.

## 5. Kubernetes Cluster Architecture

The experiment uses a three-node Kubernetes cluster consisting of:

- **One control-plane node:** Manages the cluster and coordinates its operations.
- **Two worker nodes:** Run application workloads and Kubernetes Pods.

The control plane includes components such as:

- API Server
- Scheduler
- Controller Manager
- etcd

The worker nodes contain components such as kubelet and kube-proxy and are responsible for running application workloads.

Kind runs the cluster nodes as Docker containers on the host machine.

## 6. Cluster Configuration

The cluster configuration is defined in `config/kind-config.yaml`.

The configuration specifies one control-plane node and two worker nodes.

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

## 7. Implementation Procedure

### Step 1: Verify the Required Tools

The following commands are used to check the installed tools and Docker environment.

```powershell
docker version
docker run hello-world
kubectl version --client
kind version
```

### Step 2: Create the Kubernetes Cluster

The cluster is created using the Kind configuration file.

```powershell
kind create cluster --config kind-config.yaml
```

The cluster information is checked using:

```powershell
kubectl cluster-info --context kind-kind
```

The available nodes are displayed using:

```powershell
kubectl get nodes
```

Docker containers running the cluster nodes can be inspected using:

```powershell
docker ps
```

### Step 3: Inspect Kubernetes System Components

The system Pods running in the kube-system namespace are inspected using:

```powershell
kubectl get pods -n kube-system -o wide
```

This helps identify the Kubernetes control-plane and networking components.

### Step 4: Deploy the NGINX Application

An NGINX Deployment named `web` is created with three replicas.

```powershell
kubectl create deployment web --image=nginx --replicas=3
```

The deployment status is checked using:

```powershell
kubectl get deployments
```

The running Pods and their node assignments are inspected using:

```powershell
kubectl get pods -o wide
```

### Step 5: Scale the Deployment

The NGINX deployment is scaled from three replicas to six replicas.

```powershell
kubectl scale deployment web --replicas=6
```

The Pods are inspected again using:

```powershell
kubectl get pods -o wide
```

This demonstrates how Kubernetes adjusts the number of application replicas according to the desired replica count.

## 8. Observations

The following observations were recorded during the experiment:

1. A Kubernetes cluster was configured with one control-plane node and two worker nodes.
2. Kubernetes system Pods were inspected in the `kube-system` namespace.
3. An NGINX Deployment named `web` was created with three replicas.
4. The deployment was scaled to six replicas.
5. The running Pods and their node distribution were inspected.
6. Kubernetes deployment details and cluster events were examined.

## 9. Result

A three-node Kubernetes cluster was created using Kind. An NGINX application was successfully deployed and its replica count was increased from three to six using Kubernetes scaling commands.

The experiment demonstrated basic multi-node cluster management, application deployment, scaling, and inspection of Kubernetes resources.

## 10. Learning Outcomes

Through this experiment, the following concepts were understood:

- Basic Kubernetes cluster architecture.
- Difference between control-plane and worker nodes.
- Role of Kind in creating local Kubernetes clusters.
- Use of kubectl to manage Kubernetes resources.
- Deployment of containerized applications.
- Horizontal scaling of application replicas.
- Inspection of Pods, node distribution, and cluster events.

## 11. Repository Contents

The GitHub repository contains the following supporting materials:

- `config/kind-config.yaml` – Kind cluster configuration.
- `manifests/web-deployment.yaml` – Additional reusable NGINX Deployment manifest.
- `screenshots/` – Screenshots captured during the lab implementation.
- `docs/` – Experiment report, command reference, and troubleshooting documentation.

**Note:** The original NGINX deployment was created using the `kubectl create deployment` command. The YAML manifest in the repository is provided as an additional reusable configuration.
