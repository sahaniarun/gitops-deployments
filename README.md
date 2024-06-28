# GLACIATION Platform configuration

This repository contains GitOps definitions for GLACIATION Platform.

## Clusters

Platform installation to Kubernetes cluster is called GLACIATION Node. See more details about deployed nodes: 
* [Integration cluster](integration/README.md)
* [Uce case 2 cluster](UC2/README.md)

## CI/CD

The diagram shows how CI/CD works in GLACIATION project.

![image](docs/process-diagram.drawio.svg)

A reference example of application repository is [glaciation-metadata-service](https://github.com/glaciation-heu/glaciation-metadata-service).

## How to install a new node

1. Install ArgoCD
   1. Follow official [docs](https://argo-cd.readthedocs.io/en/stable/getting_started/).
   2. Apply `argocd-*.yaml` configmaps of our custom configuration.
      ```
      $ kubectl apply -f "argocd-*.yaml" -n=argocd
      ```
   3. Use *.yaml as App-of-Apps configurations.

1. Install load balancer. Check [load-balancer](load-balancer) for more details.

1. Set up DNS server. Check [dns-server](docs/dns-server/node-configuration.md) for more details.


