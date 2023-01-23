---
title: "IPv4"
parent: Interconexions and Network Management
permalink: "/interconexions_network_management/ipv4"
layout: default
---

### TCP/IP Model

It's a model built on a set of layers such as:

1. Physical (Ethernet, Wifi, Token Ring)
2. Network (IP with things such as ICMP and ARP)
3. Transport (TCP or UDP)
4. Application (SMPT, DNS, FTP or many others)

Each level is encapsulated as they go from one end to the other, so the user data receives an application header, a TCP header (now it is considered a segment), a IP header (now it's a datagram) and finally an Ethernet header and trailer (to become a frame).

#### IPv4 Adresses

IPv4 uses 32-bit adresses (unique for each machine). They are divided in 2 parts, the NetID and HostID. There are 3 types of addresses:
- Unicast (One receiver)
- Broadcast (To all devices in network)
- Multicast (to multiple devices)

There is a concept called address class, which divides diferent types of networks based on the number and division made between NetID and HostID. This meant that a lot of addresses of classes with a high number of HostID possiblities would go unutilized.  

Network masks are used to separate the NetID and HostID in an address. They can range between 0.0.0.0 and 255.255.255.255, just like IP addresses. They can be used to agregate various smaller networks into a bigger one called a supernet/subnetting.


#### IP Protocol

It transfers information between a sender and a receiver equipment (in diferent networks).
- Datagram switching  
Each datagram has the destination address, there are no acknowledges, the information can be received in duplicate or out of order and each datagram can follow a different path.  

It is responsible for the management of the maximum information size suported by each network (MTU - Maximum transmission Unit) and it should make apparent to the layers above the limitations from lower layers. The solution is packet fragmentation.

There are two types of fragmentation:
- Transparent: Each network fragments and assembles packets at beginning and ending of a network.  
Every packet exits by the same gateway (potencial loss of performance) and extra processing for repeatably fragmenting and assembling packets.
- Non-Transparent: Once the packet gets fragmented, it is only reassembled in the destination.  
Every host must be able to assemble a packet, each packet has a header and they can go via different gateways (better performance).

#### IP Header (Between 5-15 of 32 bit words)

There are fields like the version being used, IHL (header size), total length and often ignored field called type of service.
There is also a field for Identification of the packet, DF/MD (Don't fragment/More Fragment), Fragment offset and Time to live (How many hops it stays going on the network).
Finally, there is a field for the Protocol being used in the layer above, and there is also a Header Checksum (header error verification).

#### Addressing

Machines in the same network share the same NetID, but they can have multiple IP numbers for conections to multiple networks. Diferent networks mean having different IP addresses, and they don't communicate directly, but via routers.


