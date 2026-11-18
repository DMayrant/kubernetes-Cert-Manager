# Istio 🎛️
```bash
# Install CRDS 
helm install istio-base istio/base -n istio-system 

# Install control plane
helm install istiod istio/istiod -n istio-system

# Inject ns for istio
kubectl label namespace nginx-system istio-injection=enabled --overwrite

kubectl get ns -L istio-injection 

helm uninstall istio-base istio/base -n istio-system 
```

# Kiali for Istio Performance Observability 🔭

```bash
helm repo add kiali https://kiali.org/helm-charts

helm install my-kiali-server kiali/kiali-server \
  --namespace istio-system \
  --version 2.33.0 \
  --set external_services.prometheus.enabled=true \
  --set-string external_services.prometheus.url=http://my-prometheus-server.monitor.svc.cluster.local:80
  
kubectl get svc -n istio-system 
kubectl create token kiali -n istio-system
```