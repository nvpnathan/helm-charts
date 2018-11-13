# Helm Installation and Lab

## Introduction

Helm is a package manager for Kubernetes that allows developers and operators to more easily package, configure, and deploy applications and services onto Kubernetes clusters.

## Overview

Most every programming language and operating system has its own package manager to help with the installation and maintenance of software. Helm provides the same basic feature set as many of the package managers you may already be familiar with, such as Debian's apt, or Python's pip.

### Helm capabilities:

- Install software.
- Automatically install software dependencies.
- Upgrade software.
- Configure software deployments.
- Fetch software packages from repositories.

### Prereq's 

- ServiceAccount and ClusterRoleBinding for **Tiller**
- Command line tool `helm` 

### Prepare the K8s cluster for Tiller

1.0 SSH to the cli-vm

<details><summary>Screenshot 1.0</summary>
<img src="images/ssh-cli-vm.png">
</details>

1.1 Pull down the Helm Chart lab repo with `git clone`

`git clone https://github.com/nvpnathan/helm-charts.git`

1.2 Navigate into the helm-charts directory

`cd helm-charts/planespotter/tiller`

1.3 Apply the Tiller ServiceAccount and ClusterRoleBinding, along with a default storage class for MySQL to your K8s cluster

`kubectl apply -f rbac-config.yaml`
`kubectl apply -f default-sc.yaml`

1.4 Navigate to the **helm chart** for Planespotter

`cd ..`

1.5 Install the `helm` binary on your jumpbox

1.6 Install **tiller** into your K8s cluster with the service account created in 1.3

`helm init --service-account tiller`

1.7 Verify Tiller is running in your **kube-system** namespace

`kubectl get pods -n kube-system`

1.8 Install the **Planespotter** application with `helm`

`helm install planespotter ./planespotter`