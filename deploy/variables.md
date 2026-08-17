# Deploy Variables

This document describes all variables and parameters required to deploy the controller.

## Credentials Secret

The controller reads Huawei Cloud credentials from a Kubernetes Secret named `huawei-cloud-credentials` in the `everest-system` namespace.

| Key | Required | Description | Example |
|---|---|---|---|
| `ak` | Yes | Huawei Cloud Access Key (permanent, not STS) | `HPUANXUOD69...` |
| `sk` | Yes | Huawei Cloud Secret Key (permanent, not STS) | `***` |
| `project-id` | Yes | Project ID (found in console top-right dropdown) | `72854f25...` |
| `region` | Yes | Must match your CCE cluster region | `cn-north-4` |

Create the Secret:

```bash
kubectl create secret generic huawei-cloud-credentials \
  --namespace everest-system \
  --from-literal=ak=<your-AK> \
  --from-literal=sk=<your-SK> \
  --from-literal=project-id=<your-ProjectID> \
  --from-literal=region=<your-region>
```

> **Security**: Never commit credentials to the repository. Always use the Secret mechanism above.

## Container Image

| Variable | Location | Description |
|---|---|---|
| `image` | `deploy/deployment.yaml` line 24 | SWR image address, format: `<swr-registry>/<namespace>/huawei-elb-controller:latest` |
| `imagePullPolicy` | `deploy/deployment.yaml` | Default `Always` (ensures latest image is pulled) |

Replace the placeholder before deploying:

```bash
sed -i 's|<swr-registry>|swr.cn-north-4.myhuaweicloud.com/<your-namespace>|' deploy/deployment.yaml
```

## Controller Runtime Parameters

| Flag | Default | Description |
|---|---|---|
| `--metrics-bind-address` | `:8081` | Metrics server listen address |
| `--health-probe-bind-address` | `:8082` | Health probe server listen address |
| `--webhook-port` | `9443` | Mutating webhook HTTPS server port |

## Namespace

The controller is deployed to `everest-system`. The Mutating Webhook only intercepts Service CREATE in the `everest` namespace (configured via `namespaceSelector` in `webhook.yaml`).

## Network Auto-Detection

The controller auto-detects the following from cluster nodes (no manual configuration needed):

| Parameter | Source |
|---|---|
| VPC ID | Node ECS metadata |
| Subnet ID | Node labels / ECS metadata |
| Availability Zones | Node `topology.kubernetes.io/zone` labels |

## ELB Default Parameters (Auto Mode)

When no LoadBalancerConfig is specified, these defaults apply:

| Parameter | Default |
|---|---|
| ELB type | Public (with EIP) |
| Bandwidth | 10 Mbit/s |
| Billing mode | Traffic |
| EIP type | 5_bgp |
| Health check | TCP, 10s interval / 10s timeout / 3 retries |
| Backend mode | NodePort (node IP + NodePort) |
