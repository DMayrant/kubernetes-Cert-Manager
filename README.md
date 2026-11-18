# Cert-Manager🥇

Cert-manager automates TLS certificate issuance and renewal in Kubernetes. Kong comes with a default self-signed certificate for localhost. In this lab, cert-manager issues a certificate for nginx.example.test and keeps it current in a Kubernetes TLS Secret. Kong reads that Secret and serves the certificate for the matching hostname.

With standard HTTPS, the client verifies the server’s identity. If both sides need to authenticate each other, that requires mutual TLS (mTLS) and a client certificate.

# Update kubeconfig ☁️
```bash
aws eks update-kubeconfig \
  --region us-east-1 \
  --name aws-eks-cluster
```

# Prometheus/Grafana 🔭
```bash
kubectl create ns monitor 

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm install my-prometheus prometheus-community/prometheus --version 29.37.2 - monitor
```

# Istio Service mesh 
This service provides your workloads with additional 

- Observability 🔭
- mTLS 🔐
- Traffic Control 🎛️
- Policy Enforcement and Security 
- Smoke Test 
  
# Installing Istio Service Mesh with helm ☸️

```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts

helm repo update 
```
# Creating namespace and installing istio base chart and pod 📈

```bash
kubectl create namespace istio-system

# Install CRDS 
helm install istio-base istio/base -n istio-system 

# Install control plane
helm install istiod istio/istiod -n istio-system
```

# Label workloads namespace for Istio Enforcement 
```bash
kubectl label namespace nginx istio-injection=enabled --overwrite
```

# Uninstall istio service-mesh and remove ns label 
```bash
kubectl label namespace nginx istio-injection=enabled

kubectl get ns -L istio-injection 

helm uninstall istio-base istio/base -n istio-system 

helm uninstall istiod istio/istiod -n istio-system
```

# Terraform 🏗️
```bash
terraform init
terraform fmt -recursive
terraform validate
terraform plan
terraform apply
```

