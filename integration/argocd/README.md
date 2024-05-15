# ArgoCD

## How to install from scratch

1. Follow official [docs](https://argo-cd.readthedocs.io/en/stable/getting_started/).
2. Apply `argocd-*.yaml` configmaps of our custom configuration.
   ```
   $ kubectl apply -f "argocd-*.yaml" -n=argocd
   ```
3. Use [bootstrap.yaml](bootstrap.yaml) as App-of-Apps configuration.