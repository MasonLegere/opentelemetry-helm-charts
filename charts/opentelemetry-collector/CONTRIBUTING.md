# Collector Chart Contributing Guide

## Bumping Default Collector Version

1. Increase the minor version of the chart by one and set the patch version to zero.
2. If required, add documentation to [UPGRADING.md](UPGRADING.md) reflecting the change.
3. Add tests if possible for new features by creating or modifying values files within `ci/`.
4. Update the chart's `appVersion` to match the new collector version.  This version will be used as the image tag by default.
5. Review the corresponding release notes in [Collector Core](https://github.com/open-telemetry/opentelemetry-collector/releases), [Collector Contrib](https://github.com/open-telemetry/opentelemetry-collector-contrib/releases), and [Collector Releases](https://github.com/open-telemetry/opentelemetry-collector-releases/releases).  If any changes affect the helm charts, adjust the helm chart accordingly.
6. Run `make generate-examples`.

### Testing and Continuous Integration

On pull requests against the `main` branch a [`kind`](https://github.com/kubernetes-sigs/kind) cluster is started and [`chart-testing`](https://github.com/helm/chart-testing) is used to sequentially install the value files `charts/opentelemetry-collector/ci/*-values.yaml` for verification.

The CI can be ran locally with:
```bash
kind create cluster
ct install --charts charts/opentelemetry-collector --helm-extra-args "--timeout 600s"
```
