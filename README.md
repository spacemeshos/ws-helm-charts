# Spacemesh Helm Charts

This repository contains spacemesh charts and values for external charts.
`gh-pages` branch contains helm repository: index.yaml and helm packages.

## Prerequisites

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Some external charts have to be installed:

- ingress-nginx provides [ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) support
- cert-manager requests TLS certificates for endpoints
- external-dns creates DNS records on CloudFlare
- prometheus gathers metrics and fires alerts
- grafana visualizes metrics

Install ingress-nginx:

```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install -f charts/ingress-nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx
```

Install cert-manager:

```
helm repo add jetstack https://charts.jetstack.io
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml
helm install cert-manager jetstack/cert-manager
kubectl apply -f cert-manager/cluster-issuer.yaml
```

Install external-dns:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install -f charts/external-dns/values.yaml external-dns bitnami/external-dns
```

Install prometheus:

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus
```

Install grafana:

```
helm repo add grafana https://grafana.github.io/helm-charts 
helm install -f charts/grafana/values.yaml grafana grafana/grafana
```

## Install spacemesh charts

See the documentation for each chart in [charts](charts) directory.
