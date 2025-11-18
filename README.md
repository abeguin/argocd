# argocd

## Installation 

```shell
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```

```shell
kubectl create namespace argocd
```

```shell
helm install argocd argo/argo-cd -n argocd
```

```shell
helm upgrade --install argocd argo/argo-cd \
  -n argocd \
  -f values.yaml
```

```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

```shell
kubectl apply -n argocd -f argocd/applicationset.yaml
```

```shell
kubectl apply -n argocd -f argocd/bitnami-repository.yaml
```