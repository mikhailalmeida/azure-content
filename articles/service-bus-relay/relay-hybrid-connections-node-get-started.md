<properties
    pageTitle="Get started with Relay Hybrid Connections | Microsoft Azure"
    description="How to write a Node console application for Hybrid Connections"
    services="service-bus"
    documentationCenter="node"
    authors="jtaubensee"
    manager="timlt"
    editor=""/>

<tags
    ms.service="service-bus"
    ms.devlang="tbd"
    ms.topic="hero-article"
    ms.tgt_pltfrm="node"
    ms.workload="na"
    ms.date="10/28/2016"
    ms.author="jotaub"/>

# Get started with Relay Hybrid Connections

[AZURE.INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

## What will be accomplished

Since Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial. Here are the steps:

1. Create a Relay namespace, using the Azure portal.

2. Create a Hybrid Connection, using the Azure portal.

3. Write a server console application to receive messages.

4. Write a client console application to send messages.

## Prerequisites

1. [Node.js](https://nodejs.org/en/) (This sample uses Node 7.0).

2. An Azure subscription.

[AZURE.INCLUDE [create-account-note](../../includes/create-account-note.md)]

## 1. Create a namespace using the Azure portal

If you already have a Relay namespace created, jump to the [Create a Hybrid Connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.

[AZURE.INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## 2. Create a Hybrid Connection using the Azure portal

If you already have a Hybrid Connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.

[AZURE.INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## 3. Create a server application (listener)

To listen and receive messages from the Relay, we will write a Node.js console application.

[AZURE.INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## 4. Create a client application (sender)

To send messages to the Relay, we will write a Node.js console application.

[AZURE.INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## 5. Run the applications

1. Run the server application.

2. Run the client application and enter some text.

3. Ensure that the server application console outputs the text that was entered in the client application.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Congratulations, you have created an end-to-end Hybrid Connections application.

## Next steps:

- [Relay FAQ](relay-faq.md)
- [Create a namespace](relay-create-namespace-portal.md)
- [Get started with .NET](relay-hybrid-connections-dotnet-get-started.md)
- [Get started with Node](relay-hybrid-connections-node-get-started.md)