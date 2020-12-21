# spacemesh-dash

spacemesh-dash runs Spacemesh Dashboard back end. It uses mongoDB service
from spacemesh-explorer.

## Prerequisites

- Kubernetes 1.16+
- Helm 3+

## Install

To install the chart with the release name `spacemesh-dash`:

```console
$ helm repo add spacemesh https://spacemeshos.github.io/ws-helm-charts
$ helm install -f values.yaml spacemesh-dash spacemesh/spacemesh-dash
```

Where `values.yaml` is a file with configuration parameters (see below).

## Upgrade

This command will upgrade to new (if available) helm chart and apply values
from `values.yaml`.

```console
$ helm upgrade -f values.yaml spacemesh-dash spacemesh/spacemesh-dash
```

## Uninstall

To uninstall all installed components:

```console
$ helm uninstall spacemesh-dash
```

## Configuration

Minimal values.yaml file example:

```yaml
mongo: mongodb://spacemesh-explorer-mongo
ingress:
  domain: dash-api.spacemesh.io
```

The following table lists main configurable parameters of the spacemesh-api
chart and their default values.

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `replicaCount`  | Number of api replicas  | `2` |
| `mongo` | The name of kubernetes mongo service to connect to | `explorer-mongo` |
| `ingress.domain` | Domain name for api endpoint | `""` |
| `image.tag` | Image tag of dash-backend | `""` (latest) |
