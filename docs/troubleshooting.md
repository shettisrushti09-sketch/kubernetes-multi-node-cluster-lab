# Kubernetes Lab – Troubleshooting Guide

This document describes common issues that may occur while setting up and working with a Kubernetes cluster using Kind on Windows.

## 1. Docker Daemon Not Running

**Problem:** Docker commands fail or Docker cannot connect to the Docker Engine.

**Possible cause:** Docker Desktop is not running.

**Solution:**
1. Open Docker Desktop.
2. Wait until the Docker Engine is running.
3. Open PowerShell again.
4. Verify using:

```powershell
docker version
```

## 2. Command Not Recognized

**Problem:** PowerShell displays an error indicating that a command such as `kubectl` or `kind` is not recognized.

**Possible cause:** The required tool is not installed or the terminal has not refreshed its PATH environment.

**Solution:**
1. Verify that the required tool is installed.
2. Close and reopen PowerShell.
3. Check the installation using:

```powershell
kubectl version --client
kind version
```

## 3. WSL 2 or Virtualization Issues

**Problem:** Docker Desktop fails to start because of WSL 2 or virtualization-related issues.

**Possible cause:** WSL 2 is not configured correctly or hardware virtualization is unavailable.

**Solution:**
1. Check the WSL status.
2. Ensure that the required Windows virtualization features are enabled.
3. Restart the system if configuration changes are made.
4. Start Docker Desktop again.

## 4. Kubernetes Nodes Not Ready

**Problem:** One or more Kubernetes nodes show a `NotReady` status.

**Possible cause:** The cluster may still be initializing or a node component may not be ready.

**Solution:**
1. Wait for the cluster to finish starting.
2. Check node status again:

```powershell
kubectl get nodes
```

3. If the issue continues, inspect the cluster and Docker containers before considering recreation of the cluster.

## 5. ImagePullBackOff

**Problem:** An application Pod displays the `ImagePullBackOff` status.

**Possible cause:** Kubernetes is unable to retrieve the requested container image.

**Solution:**
1. Check the Pod details:

```powershell
kubectl describe pod <pod-name>
```

2. Inspect the events for image-pull errors.
3. Verify the image name and network connectivity.

## 6. YAML Parsing Errors

**Problem:** Kind or Kubernetes reports an error while reading a YAML configuration file.

**Possible cause:** Incorrect indentation, invalid YAML syntax, or incorrect configuration values.

**Solution:**
1. Open the YAML file.
2. Check indentation and spacing.
3. Verify that the configuration structure and values are correct.
4. Save the file and retry the relevant command.

## 7. Git Bash Command Issues

**Problem:** Some commands from the lab procedure behave differently or fail in Git Bash.

**Possible cause:** The lab procedure is intended to be followed using Windows PowerShell.

**Solution:** Use Windows PowerShell to execute the commands provided in the lab manual.

## 8. General Troubleshooting Checklist

Before running the lab commands, verify the following:

- Docker Desktop is running.
- WSL 2 is configured.
- Kind is installed.
- kubectl is installed.
- PowerShell is being used.
- The cluster configuration file is available at the specified path.
- The Kubernetes cluster has finished initializing.

## 9. Reference

This guide is based on the troubleshooting section of the college laboratory manual, *Kubernetes Lab on Windows*.

