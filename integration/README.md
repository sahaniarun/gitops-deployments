# Integration Cluster

## Avalable services

| service | url |
| ---     | --- |
| grafana | http://grafana.integration/ |
| gatekeeper policy manager UI | http://gpm.integration/ |
| Argo CD | http://argocd.integration/ |
| MinIO Glaciation Tenant API | http://glaciation-tenant.integration/ |
| MinIO Glaciation Tenant Console | http://glaciation-tenant-console.integration/ |

## DNS workaround

Our Kubernetes cluster has no DNS server set up yet. 
To override it, add to your host file `/etc/hosts` the following configurations:

```
10.14.1.160 grafana.integration 
10.14.1.160 gpm.integration
10.14.1.160 argocd.integration
10.14.1.160 glaciation-tenant.integration
10.14.1.160 glaciation-tenant-console.integration
```

## How to install ArgoCD from scratch

1. Follow official [docs](https://argo-cd.readthedocs.io/en/stable/getting_started/).
2. Apply `argocd-*.yaml` configmaps of our custom configuration.
   ```
   $ kubectl apply -f "argocd-*.yaml" -n=argocd
   ```
3. Use [bootstrap.yaml](bootstrap.yaml) as App-of-Apps configuration.