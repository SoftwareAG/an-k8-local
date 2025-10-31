# Adabas and Natural on Kubernetes

## Overview

This document provides comprehensive instructions for deploying Adabas and Natural components in a local Kubernetes environment, supporting business-critical development and testing scenarios. All deployments (Adabas, Natural, and Adabas Manager) are configured to run within a single dedicated namespace for streamlined management and secure inter-component communication.

---

### Local Kubernetes Setup Requirements

- The manifests are designed for use with a local Kubernetes cluster, such as Docker Desktop (with Kubernetes enabled) or Minikube.
- Ensure your local cluster is running and accessible via `kubectl` before deploying the manifests.
- All resources (Deployments, ConfigMaps, Services, and optional Ingress) will be created in the same namespace, which you must create before applying the manifests.
- The setup is intended for local development and testing, but can be adapted for cloud environments if needed.

The provided manifests include Deployments, ConfigMaps, Services, and (optionally) Ingress resources for Adabas, Natural, and Adabas Manager.

- **Adabas**: Software AG enterprise database system, deployed as a StatefulSet or Deployment. Adabas stands for "Adaptable Database System." It is a high-performance, non-relational (NoSQL) database management system.
- **Natural**: Proprietary fourth-generation programming language (4GL) by Software AG, designed to work closely with Adabas as the database backend.
- **Adabas Manager**: Management and monitoring component, deployed as a Deployment.

All components communicate via Kubernetes Services within the same namespace. ConfigMaps are used to provide configuration files. The manifests files are tailored for local use and can be customized as needed.

---

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- **Docker Desktop** (with Kubernetes enabled) or **Minikube**
- **kubectl** (Kubernetes CLI)
- **git**

### Installation Resources

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [git](https://git-scm.com/downloads)

---

## Deployment Steps

### 1. Clone the Repository

Open a terminal and run:

```bash
# Clone the repository and change directory
git clone https://github.com/SoftwareAG/an-k8-local 
cd an-k8-local
```



---

### 2. Start Local Kubernetes Cluster

- **Docker Desktop**: Ensure Kubernetes is enabled in Docker Desktop settings.
- **Minikube**: Start Minikube with:

  ```bash
  minikube start
  ```

Verify your cluster is running:

```bash
kubectl cluster-info
```

---

### 3. Configure kubectl Context (if needed)

If you have multiple clusters, ensure you are using the correct context:

```bash
kubectl config get-contexts
kubectl config use-context <context-name>
```

---

### 4. Create a Dedicated Namespace

Choose a namespace name (e.g., `adanat-local`) and create it:

```bash
kubectl create namespace adanat-local
```

---

### 5. Deploy Solution Manifests

Apply all manifest files in the directory to your namespace:

```bash
kubectl apply -n adanat-local -f .
```

> **Note:**
> - Ensure all required ConfigMaps, Deployments, and Services are present in the local directory.
> - If you add or modify manifests, re-run the above command to update the resources.

---

### 6. Validate Deployment Status

Check the status of pods and services:

```bash
kubectl get pods -n adanat-local
kubectl get svc -n adanat-local
```

---

### 7. Access Deployed Applications

- For NodePort or LoadBalancer services, use `kubectl get svc -n adanat-local` to find the exposed ports.

---

### 8. Clean Up Resources

To remove all resources from the namespace:

```bash
kubectl delete -n adanat-local -f .
kubectl delete namespace adanat-local
```

---

## Troubleshooting and Support

- Use `kubectl describe <resource> -n adanat-local` for detailed info.
- Check logs with `kubectl logs <pod-name> -n adanat-local`.
- Ensure Docker Desktop or Minikube is running before applying manifests.

---

## Additional References

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Docker Desktop Kubernetes](https://docs.docker.com/desktop/kubernetes/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
- [Rancher Quick Start Guide](https://ranchermanager.docs.rancher.com/pages-for-subheaders/quick-start-guide)
- [Install Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Install Docker Desktop](https://docs.docker.com/desktop/install/)
- [Install Rancher Locally](https://ranchermanager.docs.rancher.com/pages-for-subheaders/quick-start-guide)

---

For further assistance, contact the project maintainer or refer to the documentation above.
