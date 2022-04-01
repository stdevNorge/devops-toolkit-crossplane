## Instalacion de los componentes base de la solucion:

### Instalamos crossplane, el cual nos permitira definir los componentes de la solucion.

```bash
kubectl create ns crossplane-system
```

```bash
helm repo update
```

```bash
helm upgrade -i crossplane crossplane-stable/crossplane -n crossplane-system \
    --create-namespace --wait
```

```bash
helm repo add crossplane-stable https://charts.crossplane.io/stable
```

**Nota**: Podemos comprobar que el crossplane haya quedado correctamente instalado ejecutando :

```
kubectl -n crossplane-system get pods
```
Deberia mostrar los pods del crossplane en un estado **READY**

```
NAME                                                          READY   STATUS    RESTARTS   AGE
crossplane-57f79b9488-7tn9c                                    1/1     Running   4          3d5h
crossplane-provider-helm-f6c5ce0da0dd-5bf9bc5675-lpzrn         1/1     Running   7          3d5h
crossplane-provider-kubernetes-e3a9c3ae909b-79bbb66d8b-dpcmn   1/1     Running   5          2d6h
crossplane-rbac-manager-7496649f5f-5vwgp                       1/1     Running   4          3d5h
```
### Luego instalamos los demas elementos que precisaremos para ejecutar las pruebas:
Creamos namespaces para organizar nuestros proyectosy los componentes de monitoreo , ademas de instalar las configuraciones de los proveedores (las  cuales nos permitiran interactuar con nuestro cluster K8s) y los elementos de monitoreo,logs y gitops (Prometheus, Grafana y ArgoCD)

```
kubectl create ns project-a
```

```
kubectl create ns monitoring
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
kubectl apply -f packages/monitoring/definition.yaml
kubectl apply -f packages/monitoring/prom-loki.yaml
```

```
kubectl apply -f examples/monitoring/prom-loki.yaml
```

```
kubectl apply -f packages/gitops/argo-cd.yaml
kubectl apply -f packages/gitops/definition.yaml
```

```
kubectl apply -f examples/gitops/argo-cd-no-claim.yaml
```

Una vez ejecutados los comandos anteriores estamos en condiciones de comenzar a ejecutar nuestras pruebas.
