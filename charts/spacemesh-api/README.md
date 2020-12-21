# spacemesh-api

spacemesh-api exposes public api of
[go-spacemesh](https://github.com/spacemeshos/go-spacemesh). It runs several
replicas of `go-spacemesh`, waits for full sync and then puts them to work.

## Prerequisites

- Kubernetes 1.16+
- Helm 3+

## Install

To install the chart with the release name `spacemesh-api`:

```console
$ helm repo add spacemesh https://spacemeshos.github.io/ws-helm-charts
$ helm install -f values.yaml spacemesh-api spacemesh/spacemesh-api
```

Where `values.yaml` is a file with configuration parameters (see below).

## Upgrade

This command will upgrade to new (if available) helm chart and apply values
from `values.yaml`.

```console
$ helm upgrade -f values.yaml spacemesh-api spacemesh/spacemesh-api
```

If the node has been changed, it will run the new one and wait for it to sync.
Only when all new nodes are ready, old ones will be killed.

## Uninstall

To uninstall all installed components:

```console
$ helm uninstall spacemesh-api
```

## Configuration

Minimal values.yaml file example:

```yaml
netID: 100
ingress:
  grpcDomain: api-100.spacemesh.io
  jsonRpcDomain: api-json-100.spacemesh.io
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
| `netID` | Network ID | `""` |
| `config` | `go-spacemesh` config file in json format | `""` |
| `peers` | peers.json file that contains p2p peers | `""` |
| `ingress.grpcDomain` | Domain name for gRPC endpoint | `""` |
| `ingress.jsonRpcDomain` | Domain name for json-rpc endpoint | `""` |
| `replicaCount`  | Number of spacemesh-api replicas  | `2` |
| `image.tag` | Image tag | `""` (latest) |
