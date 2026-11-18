# Cert-Manager 🥇
```bash
kubectl create ns cert-manager --dry-run=client -o yaml > cert-ns.yaml

helm repo add cert-manager https://charts.jetstack.io

helm repo update 

helm install cert-manager cert-manager/cert-manager \
  --version v1.14.3 \
  -n cert-manager \
  --set installCRDs=true
```

# TLS Cert Verification via Kong 🥇
```bash
kubectl get secret nginx-kong-tls -n nginx-system \
  -o jsonpath='{.data.tls\.crt}' | base64 -D > nginx-kong-tls.crt

openssl x509 -in nginx-kong-tls.crt -noout -subject -issuer

curl -v --cacert nginx-kong-tls.crt \
  --connect-to "nginx.example.test:443:$LB:443" \
  https://nginx.example.test/
```

# Kong TLS Cert

```bash
curl -vk "https://$LB/"
```