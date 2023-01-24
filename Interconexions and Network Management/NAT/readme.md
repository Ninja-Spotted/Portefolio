---
title: "NAT"
parent: Interconexions and Network Management
permalink: "/interconexions_network_management/nat"
layout: default
---

### NAT (Network Address Translation)

Since a private network uses a different method of addressing from an external/public network it cannot be directly connected to the internet.
NAT allows for the subtituition of IP addresses on a header when a packet enters or leaves the private network, allowing for transparent comunication. The gateways of private networks implement NAT.

Migration of the ISP is done easily, since only the refresh of the NAT table is needed.

The address translation can be done using a table (Basic NAT) or with Dynamic NAT.

### NAPT (Network Address and Port Translation)

It is a mix of NAT and PAT (port address translation) and is often called IP masquerading. It is used when only a public IP is available, so that IP is mapped for all users in the private network, only changing the source ports of the traffic to distinguish receivers.

Linux uses the Netfilter/iptables package to add filtering rules to the IP module. Example:
        
First example:
        iptables –t nat –A POSTROUTING –s 10.0.1.2
        –j SNAT --to-source 128.143.71.21
Pooling of IP addresses:
        iptables –t nat –A POSTROUTING –s 10.0.1.0/24
        –j SNAT --to-source 128.128.71.0–128.143.71.30
ISP migration:
        iptables –t nat –R POSTROUTING –s 10.0.1.0/24
        –j SNAT --to-source 128.195.4.0–128.195.4.254
IP masquerading:
        iptables –t nat –A POSTROUTING –s 10.0.1.0/24
        –o eth1 –j MASQUERADE
Load balancing:
        iptables -t nat -A PREROUTING -i eth1 -j DNAT
        --to-destination 10.0.1.2-10.0.1.4
