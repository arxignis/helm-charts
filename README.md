![Arxignis logo](./images/logo.png)

<p align="center">
  <a href="https://github.com/arxignis/helm-charts/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache 2-green" alt="License - Apache 2"></a> &nbsp;
  <a href="https://github.com/arxignis/helm-charts/actions?query=branch%3Amain"><img src="https://github.com/arxignis/helm-charts/actions/workflows/release-moat.yaml/badge.svg" alt="Release Moat"></a> &nbsp;
  <a href="https://github.com/arxignis/helm-charts/actions?query=branch%3Amain"><img src="https://github.com/arxignis/helm-charts/actions/workflows/release-moat-operator.yaml/badge.svg" alt="Release Moat Operator"></a> &nbsp;
  <a href="https://github.com/arxignis/helm-charts/actions?query=branch%3Amain"><img src="https://github.com/arxignis/helm-charts/actions/workflows/release-moat-stack.yaml/badge.svg" alt="Release Moat Stack"></a> &nbsp;
  <a href="https://github.com/arxignis/helm-charts/releases"><img src="https://img.shields.io/github/release/arxignis/helm-charts.svg?label=Release" alt="Release"></a> &nbsp;
  <img alt="GitHub Downloads (all assets, all releases)" src="https://img.shields.io/github/downloads/arxignis/helm-charts/total"> &nbsp;
  <a href="https://docs.arxignis.com/"><img alt="Static Badge" src="https://img.shields.io/badge/arxignis-documentation-page?style=flat&link=https%3A%2F%2Fdocs.arxignis.com%2F"></a> &nbsp;
  <a href="https://discord.gg/jzsW5Q6s9q"><img src="https://img.shields.io/discord/1377189913849757726?label=Discord" alt="Discord"></a> &nbsp;
  <a href="https://x.com/arxignis"><img src="https://img.shields.io/twitter/follow/arxignis?style=flat" alt="X (formerly Twitter) Follow" /> </a>
</p>

# Community
[![Join us on Discord](https://img.shields.io/badge/Join%20Us%20on-Discord-5865F2?logo=discord&logoColor=white)](https://discord.gg/jzsW5Q6s9q)
[![Substack](https://img.shields.io/badge/Substack-FF6719?logo=substack&logoColor=fff)](https://arxignis.substack.com/)


# Helm Charts

This repository contains Helm charts for deploying Moat and related components.

## Charts

### moat

A Helm chart for Moat reverse proxy with security features.

**Dependencies:**
- `valkey` - Redis-compatible in-memory data store
- `clamav` - Antivirus engine

### moat-operator

A Helm chart for the Moat Kubernetes operator.

### moat-stack

Umbrella chart that installs both the Moat dataplane and the Moat Kubernetes operator together.

**Dependencies:**
- `moat` - Moat reverse proxy chart

## Installation

### Add the Helm repository

```bash
helm repo add arxignis https://helm.arxignis.com
helm repo update
```

### Install moat-stack (recommended)

Install both the Moat dataplane and operator together:

```bash
helm install moat-stack arxignis/moat-stack --version 0.1.2
```

### Install moat only

Install just the Moat reverse proxy:

```bash
helm install moat arxignis/moat --version 1.0.0
```

### Install moat-operator only

Install just the Moat Kubernetes operator:

```bash
helm install moat-operator arxignis/moat-operator --version 1.0.0
```

## Usage

See the individual chart directories for detailed configuration options:

- [moat chart values](charts/moat/values.yaml)
- [moat-operator chart values](charts/moat-operator/values.yaml)
- [moat-stack chart values](charts/moat-stack/values.yaml)

## Repository

Charts are automatically published to:
- **Repository URL**: `https://helm.arxignis.com/helm-charts`
- **GitHub Repository**: `https://github.com/arxignis/helm-charts`

## Development

### Releasing Charts

Charts are automatically released via separate GitHub Actions workflows when changes are pushed to the `main` branch:

- **Moat Chart**: Changes to `charts/moat/**` trigger the `release-moat.yaml` workflow
- **Moat Operator Chart**: Changes to `charts/moat-operator/**` trigger the `release-moat-operator.yaml` workflow
- **Moat Stack Chart**: Changes to `charts/moat-stack/**` trigger the `release-moat-stack.yaml` workflow

Each workflow can also be triggered manually via workflow_dispatch. The workflows use [chart-releaser-action](https://github.com/helm/chart-releaser-action) to package and publish charts to the GitHub Pages repository.

### Manual Release

You can also use the Makefile for manual releases:

```bash
make release VERSION=x.y.z MOAT_VERSION=x.y.z
```

## License

See the LICENSE file in the root of this repository.

