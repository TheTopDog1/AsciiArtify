# Comparative analysis of tools for local development system based on Kubernetes:<br>Minikube & Kind & K3d
## Introduction
In this document we will make a comparative analysis of three tools for deploying Kubernetes clusters in a local environment - minikube, kind and k3d. The risks that may arise with Docker licensing will also be taken into account.
## Basic characteristic of each tool
|                           | Minikube | Kind | K3d |
|---------------------------|----------|------|-----|
| Windows x86               | +        | +    | +   |
| Windows x64               | +        | +    | +   |
| MacOS x86                 | +        | +    | +   |
| MacOS x64                 | +        | +    | +   |
| Linux x86                 | +        | +    | +   |
| Linux x64                 | +        | +    | +   |
| Automation support        | +        | +    | +   |
| Management via Kubernetes | +        | +    | +   |
## Description
| Minikube                                   | Kind                                                                         | K3d                                                                                                    |
|--------------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| Is deployed as one-node Kubernetes cluster | Is Kubernetes cluster deployed in Docker. Looks alike production environment | Is a lightweight Kubernetes distribution. Enables to run multi-node Kubernetes cluster on one machine. |
## Merits vs Demerits
|          | Advantages                                                                                                                                                  | Disadvantages                                                                                                                |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Minikube | - Easiest to use<br>- Supports many container runtimes & hypervisors<br>- Cluster is easily accessible thanks to kubectl<br>- Widely spread (big community) | - Limited scalability<br>- Can be run on single node only<br>- Is limited for distributed services                           |
| Kind     | - Easy to use<br>- Docker containers as cluster nodes<br>supports Kubernetes config-files<br>supports distributed services                                  | - Is depended on Docker<br>- Is limited in comparison with Kubernetes cluster                                                |
| K3d      | - Easy to use<br>- Lightweight<br>- Supports multi-node clusters<br>- Starts really fast                                                                    | - Limited scalability<br>- Not so widely spread (not so big community)<br>- Is limited in comparison with Kubernetes cluster |
## Demonstration: Deploying the "Hello World" application on Kubernetes with k3d
We will set up a basic 'Hello World' web page running on k3s cluster
1. Install `kubectl` and `k3d` on a host
2. Create a new `k3d` cluster:
```
k3d cluster create hello
```
3. Verify that the cluster is running:
```
kubectl cluster-info
```
4. Start a single instance of nginx pod in the default namespace
```shell
kubectl run hello-world --image=hello-world
```
5. Check pods:
```shell
kubectl get pods -o wide
```
6. Check logs of pod:
```shell
kubectl logs hello-world
```
## Why Podman
1. No deamon needed
2. Can be run without administrative privileges
3. Uses "under the hood" standard tools such as `systemd`, `runc`, and `CNI`
4. Can deploy and manage Kubernetes containers
5. Supports building, running, and managing containers

## Conclusions: Recommendations for using best tool in our PoC for a startup
We have chosen k3d for implementing our PoC.