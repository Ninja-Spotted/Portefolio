---
title: "IPv6"
parent: Interconexions and Network Management
permalink: "/interconexions_network_management/ipv6"
layout: default
---

### IPv6

The IPv6 version was created to solve many of the issues with IPv4. Namely the low number of addresses, the scarcity of the addressing space, inflexibility of the supported services and the colossal size of the routing tables.  

This new version objectives are to support a large number of machines, decrease the size of the routing tables, simplify the protocol, offer better safety and support more services (real-time), mobile machines without address switching, the co-existance of various IP versions and flexibility.  

#### IPv6 Addresses

The IPv6 addresses are 128 bit long and are represented in hexadecimal in groups of 16 bits separated with `:`. Examples:
- `2001:0DF8:0101:0000:0000:00E0:F796:4F31`: Full address
- `2001:DF8:101:0:0:E0:F796:4F31`: Zeros are omitted
- `2001:DF8:101::E0:F796:4F31`: Groups of zeros can be hidden with `::`

In IPv6 it doesn't exist the concept of classes or broadcast addresses.  

Unicast addresses exist in two different categories:
- Link-Local: Only inside a local network.
- Site-Local: Used for addressing inside an institution (allow for subnetting)

Since the IPv6 version is compatible with IPv4, those addresses are now IPv4 mapped when a IPv6 host wants to talk with an IPv4 host:  
`0:0:0:0:0:FFFF:192.168.30.1` -> 80 bits + 16 bits + 32 bits

#### IPv6 Headers

Headers have a fixed lenght (40 bytes) and contain information about the IP version, Priority (real time traffic or not), Flow label (pseudo-conections), Payload length (equivalence to Total length of IPv4 but does not include 40 bytes from header), Next Header (identifies what extension header comes next), Hop limit (same as TTL on IPv4) and Source/Destination addresses.  

Also there are the extension headers that have options for Hop-by-hop options (different information for routers), Routing (defining which route to follow), Fragmentation (**Should be done by sending host and not the routers**), Authentication (receiver can confirm the identity of the sender), Encapsulation security payload (allows for encriptation of contents so that only the receiver can see it).

Fields that exist on IPv4 that became unnecessary:
- IHL: IPv6 header has fixed size
- Protocol: Next header identifies the transport protocol
- All fragmentation fields: Host is the one fragmenting
- Checksum: Other levels of the networking layer already implement it


#### IPv6 Stateless Autoconfiguration (SLAAC)

Manual configuration of machines should not be required. Address autoconfiguration assumes that each interface can provide an unique identifier (interface token), and link-local addresses achieves plug-and-play.


#### NDP (Network/Neighbor Discovery Protocol)

Replaces ARP and RARP and defines 5 ICMPv6 packet types:

- Router Advertisements (RA)  
Messages sent by router to all-host addresses at regular intervals. RA messages contain the required network prefix.

- Router Solicitations (RS)  
Host can wait for the periodic RA message or send a Router Solicitation (RS) message. They are sent to the all-routers multicast address.

- Neighbor Solicitation (RS)  
Used to request the link layer address of a neighbor.

- Neighbor Solicitation (RS)  
Used to respond with the link layer address or unsolicited to add new information quickly.

#### Stateful Configuration

If a stateless configuration is not desired, a DHCP server must be provided. It can also provide information about DNS server identification and other information.

##### Pros & Cons

SLAAC requires minimal setup, simplifies readdressing and doesn't need a DHCPv6 server, only a router.  
However, it removes control, adds vulnerabilities and there is no option to add information like DNS or NTP servers or fallback gateways. It also allocates the last 64 bits of the address.
