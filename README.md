
```
kubectl create ns crossplane-system
```
```
kubectl create ns project-a
```
```
kubectl create ns monitoring
```

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
kubectl apply -f crossplane-config/provider-kubernetes-incluster.yaml
```

```
kubectl apply -f crossplane-config/provider-helm-incluster.yaml
```

```
kubectl apply -f crossplane-config/config-k8s.yaml
```

```
kubectl apply -f crossplane-config/config-monitoring.yaml
```

```
kubectl apply -f packages/monitoring/definition.yaml
```

```
kubectl apply -f packages/monitoring/prom-loki.yaml
```
