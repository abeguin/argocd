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

### Port forward

```shell
kubectl port-forward service/argocd-server -n argocd 8080:443
```

### Retrieve initial password

```shell
argocd admin initial-password -n argocd
```

### Login

```shell
argocd login localhost:8080
```

### Update password

```shell
argocd account update-password --account admin
```

```shell
kubectl apply -n argocd -f argocd/applicationset.yaml
```

```shell
kubectl apply -n argocd -f argocd/bitnami-repository.yaml
```

## Sealed secrets

```shell
kubectl apply -f https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.33.1/controller.y
aml
```

```shell
kubeseal --controller-namespace kube-system \
--controller-name sealed-secrets-controller \
--format yaml \
--namespace paperless-abe \
< $GIT_ROOT/local/postgresql-secret.yaml \
> $GIT_ROOT/apps/paperless/abe/paperless-db-secret-sealed.yaml
```

## K8s external secrets

### Links 

- https://operatorhub.io/operator/external-secrets-operator
- https://external-secrets.io/latest/introduction/getting-started/
- https://github.com/external-secrets/external-secrets?tab=readme-ov-file

### Getting started 

```shell
helm repo add external-secrets https://charts.external-secrets.io

helm install external-secrets \
   external-secrets/external-secrets \
    -n external-secrets \
    --create-namespace \
  # --set installCRDs=false
```

