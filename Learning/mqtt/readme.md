---
title: "MQTT"
parent: Learning
permalink: "/learning/mqtt"
layout: default
---

## MQTT

This document introduces MQTT (“Message Queuing Telemetry Transport”), a very simple and lightweight communication protocol for the Internet-of-Things (IoT).

### Introduction

The ubiquity of IoT brings some questions: how to support reliable, timely and secure computations and communications over resource-constrained computing devices that are many times embedded or moving in uncontrolledand harsh environments? Clever solutions must be found to guarantee the QoS tradeoffs required by IoT applications, e.g. cross-layer design, “edge” computing, efficient and dynamic hardware and radio resource management, lighweight software and communication architectures, just to name a few.  
In an increasingly populated and heterogeneous IoT landscape, there is an eagerness for open, standardized and off-the-shelf software, hardware and communication technologies, materializing e.g. on operating systems, programming/simulation frameworks, hardware platforms and communication protocols.  
\
MQTT emerged as a lightweight protocol that is bandwidth and energy-efficient, comparing to other application-layer protocols running over TPC/UDP, such as HTTP and XMPP.  
MQTT has very little protocol complexity and overhead, being only as short as 2 bytes in some cases. There is also an even lighter version of MQQT (MQTT-SN) specifically designed for wireless sensor networks and running over Zigbee.  
\
The MQTT protocol is based on the principle of publishing messages and subscribing topics. Multiple clients connect to a data broker and subscribe to topics they are interested in, and also publish messages to topics.  
The broker filters and controls messages yet to be published, deciding which group of subscribers it should be delivered to. It is also him that controlls authentication and session controll, every time a client establishes a permanent session, the broker stores relevant data like ClientID, and if the connection is lost, the broker stores the subscribed topics and lost messages, restoring them as soon as the conection is reestablished.  
\
It may need to handle thousands of clients so some systems use Broker Clusters, which enable a redundant, balanced and distributed aproach.  
\
A MQTT client can be any computing device that runs a MQTT library and connects to a MQTT broker over a network. It can be a publisher or subscriber (or both) of a topic, a publisher specifies the topic and send messages, while subcribers receive messages by subscribing to topics.  
In terms of programming, integrating a MQTT client into an application is quite simple and there are libraries for commodity programming languages and development frameworks, such as Android, Arduino, C, C++, C#, Go, iOS, Java, JavaScript, Python and .NET.  
There are mechanisms benefitting the interaction between them:
* Subscribers are unknown to the publisher, so it does not need to store their addresses
* The publication or subscription may be dynamic and asynchronous, allowing transparent reconfiguration, modularity and mobility
* Message delivery is guaranteed even if a subscriber is temporarily off, provided that the flag `retained message` is set to true (broker stores the messasse and QoS)
* Client can use the Last will and testament (LWT) feature to instruct a broker to notify other clients after the unexpected disconnection, enabling the system to react and adapt.  

\
First thing a client should do is establish connection with the server, via a CONNECT message with information required to initiate connection. Then, the server checks the CONNECT packet and performs authentication and authorization, sending back a CONNACK response. After this, the broker will mantain the connection active untill it receives a DISCONNECT message or abrupt disconnect. If the client sends an invalid CONNECT, the server will automatically close connecton.  
\
The CONNECT control message embeds all required settings in specific fields/flags. The client must send its ID, protocol version, session preferences and actions uppon disconnection.  
\
The broker must "filter" the incoming messages depending on the clients' subscriptions. It relies on a topic-based filtering, based on a hierarchical tree of topics.  
The slash `/` is used to separate each level of topics, e.g. in `country/factory/current/rawmats/water`, the `coutry` is at the upper level and `water` at the lowest level. If a client subscribes to one of these topics it only receives the messages published for the corresponding level.  
\
A client can, however, subscribe to several topics by using wildcards:
`+` : This "single-level" wildcard enables to replace the content of a level by any of the existing topics, this means, a client subscribing to `country/factory/+/rawmats/water` will receive from `country/factory/current/rawmats/water` and from `country/factory/history/rawmats/water` but not from `country/factory/current/temperature` since the sub-level aren't the same.  
\
`#` : This "multi-level" wildcard replaces the content of preceding, current and lower levels. So, a subscription to `country/factory/#` will receive from `country/factory`, `country/factory/current/rawmats/water`, `country/factory/history/rawmats/water` and `country/factory/current/temperature`.  
\
The quality of service levels represent a tradeoff between time to transmit and confidence that it has been received:
* QoS 0 : Delivery acording to the capabilities of the network, and no response is sent, neither is a retry by the sender.
* QoS 1 : Sender guarantees the arrival once, and stores the packet ID and content until it receives a PUBACK confirming reception, otherwise, the sender retries (the receiver may get a repeated message).
* QoS 2 : This guarantees the reception of the message exactly once, through a four-way handshake.

### Instalation

In this document we will use the Eclipse Paho MQTT C Client libraries. This should work on any Debian-based distribution, however, the execution depends on other technologies like Docker containers and some prepared files with all the frontend content.

        sudo apt update
        sudo apt install build-essential make cmake cmake-gui cmake-curses-gui
        sudo apt install libssl-dev nlohmann-json3-dev
        git clone https://github.com/eclipse/paho.mqtt.c.git
        cd paho.mqtt.c
        make
        sudo make install
        
To compile the C++ programs, use the following:

        g++ test.cpp -o test -lpaho-mqtt3c

