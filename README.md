# helm-harbor

A Crossplane Configuration package that installs the Harbor Helm chart with a minimal, stable interface.

## Overview

`helm-harbor` renders a single Helm release for Harbor. It exposes only the inputs needed
for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<clusterName>-harbor` in the `harbor` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.2)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-harbor
spec:
  package: ghcr.io/hops-ops/helm-harbor:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: Harbor
metadata:
  name: harbor
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    expose:
      type: ingress
      ingress:
        hosts:
          core: harbor.example.com
    externalURL: https://harbor.example.com
```

## Development

```bash
make render
make validate
make test
```
