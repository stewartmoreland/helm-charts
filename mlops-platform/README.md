# MLOps Platform Helm Chart

A comprehensive MLOps platform for Kubernetes that integrates popular tools for machine learning operations, including:

- Kubeflow for ML workflow orchestration
- MLflow for experiment tracking
- Seldon Core for model serving
- Ray for distributed training
- JupyterHub for notebook management
- MinIO for model storage
- Prometheus & Grafana for monitoring
- Model drift detection and data quality monitoring

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- PV provisioner support in the underlying infrastructure
- (Optional) NVIDIA GPUs for accelerated training

## Installation

### Add Helm Repository

```bash
helm repo add mlops-platform https://ghcr.io/stewart/helm-charts
helm repo update
```

### Install the Chart

```bash
helm install mlops-platform mlops-platform/mlops-platform \
  --namespace mlops \
  --create-namespace \
  --values values.yaml
```

## Configuration

The following table lists the configurable parameters of the MLOps Platform chart and their default values.

### Global Parameters

| Parameter              | Description                                 | Default            |
| ---------------------- | ------------------------------------------- | ------------------ |
| `global.storage.class` | Storage class for persistent volumes        | `""`               |
| `global.storage.size`  | Default storage size for persistent volumes | `"100Gi"`          |
| `global.gpu.enabled`   | Enable GPU support                          | `false`            |
| `global.gpu.type`      | GPU type to use                             | `"nvidia.com/gpu"` |

For detailed configuration options, please refer to the [values.yaml](values.yaml) file.

## Components

### Kubeflow

Provides ML workflow orchestration, training operators, and serving capabilities.

### MLflow

Handles experiment tracking, model registry, and artifact storage.

### Seldon Core

Manages model deployment and serving with advanced features like A/B testing and canary deployments.

### Ray

Enables distributed training and hyperparameter tuning.

### JupyterHub

Provides managed notebook instances for data scientists.

### MinIO

Object storage for models, datasets, and artifacts.

### Monitoring Stack

Includes Prometheus and Grafana for metrics collection and visualization.

## Usage Examples

### Deploying a Model

```yaml
apiVersion: machinelearning.seldon.io/v1
kind: SeldonDeployment
metadata:
  name: example-model
spec:
  predictors:
    - graph:
        name: model
        implementation: SKLEARN_SERVER
        modelUri: s3://models/example-model
      name: default
```

### Creating a Training Pipeline

```yaml
apiVersion: kubeflow.org/v1
kind: Pipeline
metadata:
  name: training-pipeline
spec:
  steps:
    - name: preprocess
      template: data-preprocessing
    - name: train
      template: model-training
      dependencies: [preprocess]
    - name: evaluate
      template: model-evaluation
      dependencies: [train]
```

## Monitoring and Maintenance

The platform includes built-in monitoring with Prometheus and Grafana:

- Model performance metrics
- Resource utilization
- Training job status
- Serving latency and throughput

Access Grafana dashboards at:

```
http://<cluster-ip>/grafana
```

## Troubleshooting

Common issues and solutions:

1. **Storage Issues**

   - Ensure PVC provisioner is working
   - Check storage class exists

2. **GPU Support**

   - Verify NVIDIA device plugin is installed
   - Check GPU nodes are properly labeled

3. **Component Communication**
   - Verify network policies
   - Check service endpoints

## Contributing

Please read [CONTRIBUTING.md](../../CONTRIBUTING.md) for details on contributing to this chart.

## License

This chart is licensed under the Apache License 2.0 - see the [LICENSE](../../LICENSE) file for details.
