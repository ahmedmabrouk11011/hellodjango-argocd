# Simple Hello Django with ArgoCD:hammer::wrench:

This is a sample django project to Practice ArgoCD, Kubernetes.


## Create [Kind](https://kind.sigs.k8s.io/) cluster for k8s deployment

```console
kind create cluster --name testing
kubectl get nodes
```



## Deploy [ArgoCD](https://argo-cd.readthedocs.io/en/stable/getting_started/)
```console
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
### Expose ArgoCD service as a LoadBalancer Service
```console
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
### Expose ArgoCD service using port-forward
```console
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
### Get Login Credentials
```console
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
* username: admin


## Deploy the application
```console
kubectl apply -f application.yaml
```
</br>

#### Links

* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)

