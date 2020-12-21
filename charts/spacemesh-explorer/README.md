# spacemesh-explorer

spacemesh-explorer runs Spacemesh Explorer. It consists of two parts:

- collector - parse blockchain data and save it to mongoDB
- api - endpoint for front end

Collector pod includes go-spacemesh, mongodb and collector itself. There are
several such pods. Number of pods regulated by `collector.replicaCount`. All
collector pods are endpoint for mongo service. `api` connects to this mongo
service. If some of collectors failed, it will be excluded from endpoints.

## Prerequisites

- Kubernetes 1.16+
- Helm 3+

## Install

To install the chart with the release name `spacemesh-explorer`:

```console
$ helm repo add spacemesh https://spacemeshos.github.io/ws-helm-charts
$ helm install -f values.yaml spacemesh-explorer spacemesh/spacemesh-explorer
```

Where `values.yaml` is a file with configuration parameters (see below).

## Upgrade

This command will upgrade to new (if available) helm chart and apply values
from `values.yaml`.

```console
$ helm upgrade -f values.yaml spacemesh-explorer spacemesh/spacemesh-explorer
```

Collector pods with new version will be started. When they are ready (synced),
they will replace the old ones.

## Uninstall

To uninstall all installed components:

```console
$ helm uninstall spacemesh-explorer
```

## Configuration

Minimal values.yaml file example:

```yaml
apiServer:
  ingress:
    domain: explorer-api.spacemesh.io
node:
  netID: 100
  config: |
    {
      "api": { ...
  peers: |
    {"Key": ...
```

The following table lists main configurable parameters of the spacemesh-api
chart and their default values.

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `node.netID` | Network ID | `""` |
| `node.config` | `go-spacemesh` config file in json format | `""` |
| `node.peers` | peers.json file that contains p2p peers | `""` |
| `apiServer.ingress.domain` | Domain name for explorer api endpoint | `""` |
| `collector.replicaCount`  | Number of collector pod replicas  | `2` |
| `imageTag` | Image tag of explorer-backend | `""` (latest) |
