# DNS server from VPN

When you connect to Dell VPN network, VPN client forces your computer to use DNS server from VPN. 
DNS server knows all GLACIATION clusters inside VPN and resolves related domain names. 
If the server does not know some domain name, it delegates the resolution to a global public DNS server.

A diagram below illustrates basic principles of domain name resolution in our environment. 

![dns_and_k8s.drawio.svg](dns_and_k8s.drawio.svg)

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


