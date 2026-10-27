\# Kubernetes Multi-Node Cluster Lab



A hands-on Kubernetes lab project completed on Windows using WSL2, Docker Desktop, Kind, and kubectl.



\## Project Overview



This project demonstrates how to create and manage a multi-node Kubernetes cluster locally using Kind (Kubernetes IN Docker).



The cluster contains:

\- 1 control-plane node

\- 2 worker nodes



An Nginx deployment was created, scaled from 3 replicas to 6 replicas, and tested for automatic pod replacement after deleting a pod.



\## Tools and Technologies



\- Windows

\- WSL2

\- Ubuntu

\- Docker Desktop 4.97.0

\- Docker Engine 29.9.2

\- Kubernetes kubectl v1.36.1

\- Kind v0.33.0

\- Kubernetes node image: kindest/node:v1.37.0

\- Nginx



\## Cluster Architecture



The local Kubernetes cluster consists of:



\- kind-control-plane

\- kind-worker

\- kind-worker2



\## Project Structure



\- kind-config.yaml - Kind cluster configuration

\- deployment/ - Kubernetes deployment manifest

\- docs/ - Lab documentation and results

\- screenshots/ - Screenshots of the completed lab

\- commands.md - Commands used during the lab



\## Lab Implementation



\### 1. Verify the Tools



The following tools were installed and verified:



\- Docker

\- kubectl

\- Kind



Docker was tested using the hello-world container.



\### 2. Create the Kubernetes Cluster



A Kind cluster was created using the configuration in kind-config.yaml.



The cluster was verified using kubectl cluster-info and kubectl get nodes.



All three nodes reached the Ready state.



\### 3. Deploy Nginx



An Nginx deployment was created with 3 replicas:



kubectl create deployment web --image=nginx --replicas=3



The deployment reached 3/3 ready replicas.



\### 4. Scale the Deployment



The deployment was scaled from 3 replicas to 6:



kubectl scale deployment web --replicas=6



All 6 Nginx pods reached the Running state.



\### 5. Test Self-Healing



One Nginx pod was deleted manually.



Kubernetes automatically created a replacement pod to maintain the desired replica count of 6.



The final pod count remained at 6.



\## Results



\- Successfully created a three-node Kubernetes cluster.

\- All cluster nodes reached Ready status.

\- Kubernetes system pods reached Running status.

\- Successfully deployed Nginx with 3 replicas.

\- Scaled the deployment to 6 replicas.

\- Verified automatic pod replacement after deleting a pod.



\## Author



GitHub: shettisrushti09-sketch

