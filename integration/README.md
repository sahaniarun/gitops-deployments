# Integration Cluster

## Available services

| Service                         | URL                                           |
|---------------------------------|-----------------------------------------------|
| ArgoCD                          | http://argocd.integration/                    |
| Data sanitization API           | http://data-sanitization.integration/         |
| Gatekeeper Policy Manager UI    | http://gpm.integration/                       |
| Grafana                         | http://grafana.integration/                   |
| Metadata service                | http://metadata.integration /                 |
| MinIO Glaciation Tenant API     | http://glaciation-tenant.integration/         |
| MinIO Glaciation Tenant Console | http://glaciation-tenant-console.integration/ |
| Prometheus                      | http://prometheus.integration                 |
| Spark history server UI         | http://spark-history-server.integration/      |
| Vault UI                        | https://vault.integration/                    |

## How to connect

### VPN

Get a VPN access to the cluster from Dell. There is no direct connectivity without VPN. 

## Initial configuration

### Traffic routing

The diagram demonstrates traffic routing from web client to application running in cluster.  

![traffic-routing.drawio.svg](docs/traffic-routing.drawio.svg)

Ingress controller is mapped to a master node port 31080. It is not the best practice. We use this approach for a quick start. Consider to use the best practices.

Load balancer is a manually installed Nginx. Check [load-balancer](load-balancer) for more details.

### DNS

When you connect to VPN network, VPN client forces your computer to use DNS server from VPN. 
DNS server knows all GLACIATION clusters inside VPN and resolves related domain names. 
If the server does not know some domain name, it delegates the resolution to a global public DNS server.

A diagram below illustrates basic principles of domain name resolution in our environment. 

![dns_and_k8s.drawio.svg](docs/dns_and_k8s.drawio.svg)

You can debug domain name resolution with a shell command `nslookup`.

Example 1. Laptop is connected to VPN, name is resolved by DNS server form VPN.

```shell
alex@laptop ~ % nslookup argocd.integration
Server:		10.14.253.253
Address:	10.14.253.253#53

Name:	argocd.integration
Address: 10.14.1.160
```

Example 2. Laptop is not connected to VPN and use DNS server from internet provider. The name is not resolved.

```shell
alex@laptop ~ % nslookup argocd.integration
Server:		172.20.10.1
Address:	172.20.10.1#53

** server can't find argocd.integration: NXDOMAIN
```

### ArgoCD

How to install ArgoCD.

1. Follow official [docs](https://argo-cd.readthedocs.io/en/stable/getting_started/).
2. Apply `argocd-*.yaml` configmaps of our custom configuration.
   ```
   $ kubectl apply -f "argocd-*.yaml" -n=argocd
   ```
3. Use *.yaml as App-of-Apps configurations.
