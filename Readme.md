### Istio v-1.2.2

## Install Istio binaries

```bash
    curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.2.2 sh -
```

## For minikube run

Replace LoadBalancer by NodePort in install/kubernetes/istio-demo.yaml

## Install CRDs

```bash
    for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
```

## Install Istio in to the cluster

```bash
    kubectl apply -f install/kubernetes/istio-demo.yaml
```

## Show kiali

```bash
    kubectl port-forward $(kubectl get pod -n istio-system -l app=kiali -o jsonpath='{.items[0].metadata.name}') -n istio-system 20001
```
Login : admin
password : admin

## Show graphana

```bash
    kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000
```

## Show jaeger

```bash
    kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686
```