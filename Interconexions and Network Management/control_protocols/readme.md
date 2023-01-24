---
title: "Control Protocols"
parent: Interconexions and Network Management
permalink: "/interconexions_network_management/control_protocols"
layout: default
---

### Control Protocols

- ICMP (Internet Control Message Protocol): Reports errors, encapsulated in an IP packet (not reliable)
- ARP (Address Resolution Protocol)
- RARP (Reverse Address Resolution Protocol)

#### ARP (Address Resolution Protocol)

IP datagrams are encapsuled in level 2 frames. They implement their own addressing mechanism, which means that it's necessary to translate the IP addresses into lower level addresses.  

For the mapping there are two ways: conversion tables with addresses (hard to build and keep) or broadcasting the question to all hosts. The answer will then be sent unicast, only to the requester.  
The ARP request is enclosed in a ethernet frame, with the destination address ff:ff:ff:ff:ff:ff and source as its own address. All hosts on the local network then read the frame and the target host recognises the request and replies.  

Since this process takes time and sending and waiting for responses would be inefficient, each node maintains a ARP cache (size limit of 512 entrie).

- Proxy ARP  
Responds to ARP requests that arrive from one of its connected networks for a host that is on another of the connected networks.
- ARP Bridging  
A bridge that works as an intermediate between two networks, and answers the requests from one network to another with its own hardware address.
- ARP Spoofing (ARP Poisoning)  
When fake ARP messages are sent to an ethernet LAN, making machines to believe that an IP addressis associated to a different MAC address.

#### RARP (Reverse Address Resolution Protocol)
Knowing the Ethernet address, it tries to find the IP address. This only aplies to devices with no storage (unknown own IP), so they ask a RARP server (**required server**).  
The messaging is similar to the ARP messages.
