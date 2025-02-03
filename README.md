# Helm Charts Repository

This repository contains a collection of Helm charts for various applications and services. Each chart is maintained independently and follows Helm best practices.

## Available Charts

### [calico-federation](./calico-federation)
Helm chart for setting up Calico federation between Kubernetes clusters.

## Usage

The charts are available both via GitHub Container Registry (GHCR) and GitHub Pages. Choose your preferred installation method:

### Install via GHCR (Recommended)

```bash
# Pull the chart
helm pull oci://ghcr.io/stewartmoreland/<chart-name> --version <version>

# Install the chart
helm install my-release oci://ghcr.io/stewartmoreland/<chart-name> --version <version>
```

### Install via GitHub Pages

1. Add the repository:
   ```bash
   helm repo add stewart-charts https://raw.githubusercontent.com/stewartmoreland/helm-charts/main/
   ```

2. Update your local repository cache:
   ```bash
   helm repo update
   ```

3. Install a chart:
   ```bash
   helm install my-release stewart-charts/<chart-name>
   ```

## [Contributing](./CONTRIBUTING.md)

1. Fork the repository
2. Create a new branch for your chart
3. Add your chart in a new directory
4. Update this README.md to include your chart
5. Submit a Pull Request

## [License](./LICENSE)

This project is licensed under the MIT License - see the individual chart directories for specific license information.
