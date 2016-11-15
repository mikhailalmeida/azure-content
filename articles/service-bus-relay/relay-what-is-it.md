<properties
	pageTitle="What is Azure relay? | Microsoft Azure"
	description="Overview of Azure Relay"
	services="service-bus"
	documentationCenter=".net"
	authors="banisadr"
	manager="timlt"
	editor="" />

<tags
	ms.service="service-bus"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="multiple"
	ms.topic="article"
	ms.date="10/28/2016"
	ms.author="babanisa" />

# What is Azure Relay?

Azure Relay service facilitates your hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure. Relay supports a variety of different transport protocols and web services standards.

The relay service supports traditional one-way, request/response, and peer-to-peer traffic. It also supports event distribution at internet-scope to enable publish/subscribe scenarios and bi-directional socket communication for increased point-to-point efficiency. 

In the relayed data tansfer pattern, an on-premises service connects to the relay service through an outbound port and creates a bi-directional socket for communication tied to a particular rendezvous address. The client can then communicate with the on-premises service by sending traffic to the relay service targeting the rendezvous address. The relay service will then "relay" data to the on-premises service through a bi-directional socket dedicated to each client. The client does not need a direct connection to the on-premises service, it is not required to know where the service resides, and the on-premises service does not need any inbound ports open on the firewall.

The key capability elements provided by Relay are bi-directional, unbuffered communication across network boundaries with TCP-like throttling, endpoint discovery, connectivity status, and overlaid endpoint security. Relay's capabilities differ from network-level integration technologies such as VPN in that it can be scoped to a single application endpoint on a single machine, while VPN technology is far more intrusive as it relies on altering the network environment.

Azure Relay has two features:

1. [Hybrid Connections](#hybrid-connections) - Uses the open standard Web Sockets enabling multiplatform scenarios

2. [WCF Relays](#wcf-relays) - Uses Windows Communication Foundation to enable Remote Procedural Calls

Hybrid Connections and WCF Relays both enable secure connection to assests that exist within a corporate enterprise network. Use of one over the other is dependent on your particular needs detailed below:

|                                    | WCF Relay | Hybrid Connections |
| ---------------------------------- |:---------:|:------------------:|
| **WCF**                            |     x     |                    |
| **.NET Core**                      |           |         x          |
| **.NET Framework**                 |     x     |         x          |
| **JavaScript/NodeJS***             |           |         x          |
| **Java***                          |           |         x          |
| **Standards-Based Open Protocol**  |           |         x          |
| **Multiple RPC Programing Models** |           |         x          |
*<sub>By General Availability</sub>

## Hybrid Connections

Azure Relay's Hybrid Connections capability is a secure, open-protocol evolution of the existing Relay features that can be implemented on any platform and in any language that has a basic WebSocket capability, which explicitly includes the WebSocket API in common web browsers. Hybrid Connections is based on HTTP and WebSockets.

## WCF Relays

The WCF Relay works for the full .NET Framework (NETFX) and for WCF. You initiate the connection between your on-premise service and the relay service using a suite of WCF "relay" bindings. Behind the scenes, the relay bindings map to new transport binding elements designed to create WCF channel components that integrate with Service Bus in the cloud.

## Service History

Hybrid Connections transplants the former, equally named "BizTalk Services" feature that was built on the Azure Service Bus WCF Relay. The new Hybrid Connections capability complements the existing WCF Relay and these two service capabilities will exist side-by-side in the Relay service for the foreseeable future; they share a common gateway, but are otherwise different implementations.

WCF Relay is the legacy Relay offering that many customers may already use with their WCF programing models.

## Next steps:

- [Relay FAQ](relay-faq.md)
- [Create a namespace](relay-create-namespace-portal.md)
- [Get started with .NET](relay-hybrid-connections-dotnet-get-started.md)
- [Get started with Node](relay-hybrid-connections-node-get-started.md)
