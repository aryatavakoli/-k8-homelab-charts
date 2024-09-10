# ArgoCD Apps of Apps - Homelab Bootstrap

## Overview

This repository contains the configuration files for deploying and managing an ArgoCD "Apps of Apps" pattern for a Kubernetes homelab environment. The setup leverages ArgoCD to deploy a collection of applications and infrastructure components, managing them declaratively through Kubernetes manifests stored in this repository.

The primary use case for this setup is to automate the deployment and management of Kubernetes resources across different namespaces in a consistent and scalable manner. ArgoCD, as a GitOps tool, ensures that the actual state of the cluster aligns with the desired state defined in Git.

When the [k8-homelab-terraform](https://github.com/aryatavakoli/k8-homelab-terraform) project provisions the Kubernetes cluster, it also deploys an ArgoCD instance. This ArgoCD instance is configured to automatically sync with this repository, enabling the cluster to bootstrap itself with the necessary applications and configurations.

## Key Features

- **GitOps Automation**: The repository follows the GitOps paradigm, ensuring that all changes to the Kubernetes cluster are made through Git commits, with ArgoCD automatically applying changes.
  
- **ArgoCD "Apps of Apps"**: The "Apps of Apps" pattern used here allows for the centralized management of multiple applications. The `bootstrap.yaml` Application acts as the parent app that orchestrates other child applications such as Cert-Manager and Sealed Secrets.

- **Self-Healing**: Leveraging ArgoCD's sync policies, the applications are set to automatically reconcile any drift between the desired and actual state. This ensures that the cluster remains in a consistent state as defined in Git.

- **Pruning & Namespace Creation**: ArgoCD is configured to automatically prune deleted resources and create namespaces as required, reducing manual intervention.