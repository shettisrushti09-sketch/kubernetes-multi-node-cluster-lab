# Kubernetes Lab – Command Reference

This document contains the PowerShell commands used in the Kubernetes Multi-Node Cluster Lab, along with their purposes.

## 1. Docker Verification

### Check Docker installation

```powershell
docker version
```

**Purpose:** Displays Docker client and server version information. It helps verify that Docker is installed and the Docker Engine is accessible.

### Test Docker functionality

```powershell
docker run hello-world
```

**Purpose:** Runs the Hello World test container to verify that Docker can successfully run containers.

## 2. Kubernetes Tools Verification

### Check kubectl installation

```powershell
kubectl version --client
```

**Purpose:** Displays the installed kubectl client version.

### Check Kind installation

```powershell
kind version
```

**Purpose:** Displays the installed Kind version.

## 3. Cluster Creation and Inspection

### Create the Kind cluster

```powershell
kind create cluster --config kind-config.yaml
```

**Purpose:** Creates a Kubernetes cluster using the specified Kind configuration file.

The configuration defines one control-plane node and two worker nodes.

### Display cluster information

```powershell
kubectl cluster-info --context kind-kind
```

**Purpose:** Displays information about the Kubernetes cluster and its control-plane endpoint.

### List cluster nodes

```powershell
kubectl get nodes
```

**Purpose:** Lists the nodes registered in the Kubernetes cluster and displays their status.

### Display Docker containers

```powershell
docker ps
```

**Purpose:** Lists currently running Docker containers, including the containers used by Kind for cluster nodes.

### Inspect Kubernetes system Pods

```powershell
kubectl get pods -n kube-system -o wide
```

**Purpose:** Displays Pods in the `kube-system` namespace, including additional details such as the node on which each Pod is running.

## 4. Application Deployment

### Create an NGINX deployment

```powershell
kubectl create deployment web --image=nginx --replicas=3
```

**Purpose:** Creates a Deployment named `web` using the NGINX container image and specifies three replicas.

### Check deployment status

```powershell
kubectl get deployments
```

**Purpose:** Displays the available Deployments and their desired, current, and ready replica counts.

### List application Pods

```powershell
kubectl get pods -o wide
```

**Purpose:** Displays application Pods along with details such as their status, IP address, and assigned node.

## 5. Application Scaling

### Scale the deployment

```powershell
kubectl scale deployment web --replicas=6
```

**Purpose:** Changes the desired number of replicas in the `web` Deployment from three to six.

### Verify scaled Pods

```powershell
kubectl get pods -o wide
```

**Purpose:** Checks the Pods after scaling and displays their current status and node distribution.

## 6. Additional Inspection Commands

The following commands are useful for examining Kubernetes resources and observing cluster activity.

### Describe a Pod

```powershell
kubectl describe pod <pod-name>
```

**Purpose:** Displays detailed information about a specific Pod, including its configuration, conditions, and events.

Replace `<pod-name>` with the actual name of the Pod.

### Watch Pod changes

```powershell
kubectl get pods -w
```

**Purpose:** Continuously displays Pod status changes as they occur.

### Display Kubernetes events

```powershell
kubectl get events
```

**Purpose:** Lists events recorded in the current namespace, which can help understand resource creation and cluster activity.

## 7. Optional Self-Healing Demonstration

The following commands are included in the lab manual as an optional activity to observe Kubernetes replacing a deleted Pod.

### Delete a Pod

```powershell
kubectl delete pod <pod-name>
```

**Purpose:** Deletes the specified Pod.

### Check Pod replacement

```powershell
kubectl get pods
```

**Purpose:** Displays the Pods after deletion. A Deployment controller can create a replacement Pod to maintain the desired replica count.

**Note:** These are optional commands from the lab procedure. Their inclusion in this reference does not imply that the activity was performed.

## 8. Command Summary

| Command | Purpose |
|---|---|
| `docker version` | Verify Docker |
| `docker run hello-world` | Test Docker |
| `kubectl version --client` | Verify kubectl |
| `kind version` | Verify Kind |
| `kind create cluster` | Create cluster |
| `kubectl get nodes` | List cluster nodes |
| `docker ps` | List running containers |
| `kubectl get pods` | List Pods |
| `kubectl get deployments` | List Deployments |
| `kubectl scale deployment` | Scale application |
| `kubectl describe pod` | Inspect Pod details |
| `kubectl get events` | Inspect cluster events |

## 9. Important Note

Run these commands in PowerShell after ensuring Docker Desktop is running and the required tools are installed. Replace placeholder values such as `<pod-name>` with actual resource names.
