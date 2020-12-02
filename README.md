# Spacemesh Helm Charts

This functionality is in beta and is subject to change.

## Prerequisites

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Install ingress-nginx:

```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install -f ingress-nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx
```

Install cert-manager:

```
helm repo add jetstack https://charts.jetstack.io
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml
helm install cert-manager jetstack/cert-manager
kubectl apply -f cert-manager/cluster-issuer.yaml
```

## Install spacemesh-api

Add spacemesh repo as follows:

```
helm repo add spacemesh https://spacemeshos.github.io/ws-helm-charts
```

Create values file `net123.yaml` for specific network:

```yaml
configFile: config-net123.conf
ingress:
  grpcDomain: api-net123.spacemesh.io
  jsonRpcDomain: api-json-net123.spacemesh.io
```

Download config file `config-net123.conf` for the network.

Install public api services with following command:

```
helm install -f net123.yaml net123 spacemesh/spacemesh-api
```
