## Pasos

Pre requisitos:
1 - Cluster Kubernetes
2 - Tener instalada las siguientes herramientas:
- kubectl
- helm

Una vez instalado el cluster kubernetes ejecutar los siguientes comandos:

```
kubectl create ns crossplane-system
```
```
kubectl create ns project-a
```
```
kubectl create ns monitoring
```

Instalamos las dependencias:

```
helm repo add crossplane-stable https://charts.crossplane.io/stable
```

```
helm repo update
```

```
helm upgrade -i crossplane crossplane-stable/crossplane -n crossplane-system \
    --create-namespace --wait
```

```
kubectl apply -f crossplane-config/provider-kubernetes.yaml
```

```
kubectl apply -f crossplane-config/provider-helm-incluster.yaml
```

```
kubectl apply -f crossplane-config/config-k8s.yaml
```

```
kubectl apply -f crossplane-config/config-gitops.yaml
```

```
kubectl apply -f crossplane-config/config-monitoring.yaml
```
