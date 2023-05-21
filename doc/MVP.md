# MVP Deployment
1. Install `k3d` & `kubectl`
2. Create new cluster
```shell
k3d cluster create argocd
```
3. Create namespace
```shell
kubectl create namespace argocd
```
4. Apply manages applications through files defining Kubernetes resources
```shell
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
5. Wait untill all the pods will be in "running" state
```shell
kubectl get pods -n argocdq
```
6. Allow access to pod from outside:
```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
7. The initial password for the admin account is auto-generated and stored as clear text in the field password in a secret named `argocd-initial-admin-secret` in your Argo CD installation namespace. You can simply retrieve this password using command:
```shell
kubectl -n argocd get secret argocd-initial-admin-secret --namespace=argocd -o jsonpath="{.data.password}" | base64 -d
```
or in order to reset password you might remove `'admin.password'` and `'admin.passwordMtime'` keys from argocd-secret and restart api server pod. Password will be reset to pod name:
```shell
kubectl patch secret argocd-secret  -p '{"data": {"admin.password": null, "admin.passwordMtime": null}}'
```
8. Using the username `admin` and the password from above login in **UI**: http://localhost:8080
   Although keep in mind updating the secret does not change the application password.
8. Configure **ArgoCD** according to [YouTube-video](https://youtu.be/3bf1RPE2zoE)
9. Be happy!)
   

# Asciinema Demo:
[![asciicast](https://asciinema.org/a/p91l1yvgLZHjzGbL2DqJNcN0q.svg)](https://asciinema.org/a/p91l1yvgLZHjzGbL2DqJNcN0q?autoplay=1)