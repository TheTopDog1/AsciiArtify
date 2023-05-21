# Pilot version of AsciiArtify deployed with k3d
We are going to deploy PoC and set access to GUI
1. Create new cluster
```shell
k3d cluster create argo-cd-demo
```
2. Create new namespace
```shell
kubectl create namespace argocd
```
3. Apply manages applications through files defining Kubernetes resources
```shell
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
```
4. Check `svc` on `argocd`
```shell
kubectl get svc -n argocd
```
5. Set up port forwarding
```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
6. The API server can then be accessed using https://localhost:8080
