# Calico Enterprise Federation Helm Chart

This Helm chart automates the setup of Calico Enterprise federation between Kubernetes clusters, enabling cross-cluster networking and policy management using VXLAN overlay networking.

## Prerequisites

- Kubernetes clusters running Calico Enterprise v3.20+
- Helm 3.x
- Administrative access to both clusters
- Network connectivity between clusters (UDP port 4789 for VXLAN)
- Non-overlapping Pod and Service CIDR ranges between clusters

## Features

- Automated setup of cluster federation components
- VXLAN overlay networking for cross-cluster connectivity
- Federation of Calico Enterprise features:
  - Global alerts and reports
  - Global network policies
  - Host endpoints
  - Network sets
  - License key management

## Installation

1. Add the required values to your `values.yaml`:

```yaml
clusterName: "cluster1"  # Name of this cluster
peerCluster:
  name: "cluster2"       # Name of the peer cluster
  apiServer: ""         # API server URL of the peer cluster
  secretName: "remote-cluster-secret"
  namespace: "calico-system"

remoteClusterConfiguration:
  enabled: true
  vxlan:
    enabled: true
    mode: CrossSubnet
    port: 4789
    vni: 4096
    mtu: 1450
```

2. Install the chart:

```bash
helm install calico-federation ./calico-federation
```

## Configuration

### Required Values

| Parameter | Description | Default |
|-----------|-------------|---------|
| `clusterName` | Name of the local cluster | `"cluster1"` |
| `peerCluster.name` | Name of the remote cluster | `"cluster2"` |
| `peerCluster.apiServer` | API server URL of the remote cluster | `""` |
| `peerCluster.secretName` | Name of the secret for cluster credentials | `"remote-cluster-secret"` |
| `peerCluster.namespace` | Namespace for the federation secret | `"calico-system"` |

### VXLAN Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `remoteClusterConfiguration.vxlan.enabled` | Enable VXLAN overlay | `true` |
| `remoteClusterConfiguration.vxlan.mode` | VXLAN mode (CrossSubnet/Always) | `"CrossSubnet"` |
| `remoteClusterConfiguration.vxlan.port` | VXLAN UDP port | `4789` |
| `remoteClusterConfiguration.vxlan.mtu` | MTU for VXLAN interfaces | `1450` |

### Federated Features

| Parameter | Description | Default |
|-----------|-------------|---------|
| `remoteClusterConfiguration.features` | List of Calico features to federate | See values.yaml |

## Post-Installation

After installing the chart, follow the instructions in the NOTES.txt to:

1. Create the federation service account and RBAC rules
2. Generate and retrieve the service account token
3. Create the federation secret in the peer cluster
4. Verify the federation setup

## Verification

Verify the federation setup by:

1. Checking the RemoteClusterConfiguration status
2. Verifying cross-cluster pod connectivity
3. Checking Typha logs for successful synchronization
4. Testing cross-cluster policy enforcement

## AWS Clusters

For AWS clusters, additional configuration is available:

```yaml
remoteClusterConfiguration:
  ipPools:
    enabled: true
    outgoingNATDisabled: true
    cidr: "<aws-vpc-cidr>"
```

## Troubleshooting

Common issues and solutions:

1. **Connection Issues**:
   - Verify VXLAN port (4789) is open between clusters
   - Check MTU settings
   - Verify API server URL is accessible

2. **Authentication Issues**:
   - Verify service account token is valid
   - Check RBAC permissions
   - Ensure secret is created in correct namespace

3. **Networking Issues**:
   - Verify no CIDR overlaps
   - Check VXLAN configuration
   - Verify Typha logs for connectivity

## References

- [Calico Enterprise Documentation](https://docs.tigera.io/calico-enterprise/latest/)
- [Federation Configuration Guide](https://docs.tigera.io/calico-enterprise/latest/multicluster/federation/kubeconfig)
- [AWS Cluster Configuration](https://docs.tigera.io/calico-enterprise/latest/multicluster/federation/aws)
