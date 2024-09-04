# frps Helm Chart

## Introduction

This Helm chart deploys frps (frp server) on a Kubernetes cluster. frp is a fast reverse proxy that allows you to expose a local server behind a NAT or firewall to the Internet. This chart specifically deploys the server component (frps) of frp.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installing the Chart

To install the chart with the release name `my-frps`:

```bash
helm install my-frps ./frps
```

## Configuration

The following table lists the configurable parameters of the frps chart and their default values.

| Parameter                | Description             | Default        |
|--------------------------|-------------------------|----------------|
| `image.repository`       | frps image repository   | `snowdreamtech/frps` |
| `image.tag`              | frps image tag          | `latest`       |
| `image.pullPolicy`       | Image pull policy       | `IfNotPresent` |
| `replicaCount`           | Number of frps replicas | `1`            |
| `service.type`           | Kubernetes service type | `ClusterIP`    |
| `service.port`           | Service port            | `7000`         |
| `configInline`           | frps configuration      | See values.yaml |

### Example configuration

```yaml
configInline: |
  bindPort = 7000
  vhostHTTPPort = 80
  vhostHTTPSPort = 443
  webServer.addr = "0.0.0.0"
  webServer.port = 7500
  webServer.user = "admin"
  webServer.password = "admin"
```

## Features

This Helm chart supports many of frps's features, including:

- TCP/UDP port exposure
- HTTP/HTTPS services with custom domains
- Websocket support
- Plugin system
- Connection pool
- Load balancing
- Health checks
- TLS support

For detailed usage of these features, please refer to the [official frp documentation](https://github.com/fatedier/frp).

## Security

Remember to change default credentials and consider using Kubernetes secrets for sensitive information.

## Persistence

This chart doesn't require persistence by default. All configuration is passed via the `configInline` value.

## Upgrading

```bash
helm upgrade my-frps ./frps
```

## Uninstalling the Chart

To uninstall/delete the `my-frps` deployment:

```bash
helm delete my-frps
```

## Support

For support, please refer to the [official frp GitHub repository](https://github.com/fatedier/frp).