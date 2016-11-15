<properties
   pageTitle="Understanding outbound connections in Azure | Microsoft Azure "
   description="This article explains how Azure enables VMs to communicate with public Internet services."
   services="load-balancer"
   documentationCenter="na"
   authors="sdwheeler"
   manager="carmonm"
   editor=""
/>
<tags
   ms.service="load-balancer"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="10/31/2016"
   ms.author="sewhee"
/>

# Understanding outbound connections in Azure

A Virtual Machine (VM) in Azure can communicate with endpoints outside of Azure in public IP address space. When a VM initiates an outbound flow to a destination in public IP address space, Azure maps the VM's private IP address to a public IP address and allows return traffic to reach the VM.

Azure provides three different methods to achieve outbound connectivity. Each method has its own capabilities and constraints. Review each method carefully to choose which one meets your needs.

|Scenario|Method|Note|
|---|---|---|
|Standalone VM (no load balancer, no Instance Level Public IP address)|Default SNAT|Azure associates a public IP address for SNAT|
|Load-balanced VM (no Instance Level Public IP address on VM)|SNAT using the load balancer|Azure uses a public IP address of the Load Balancer for SNAT|
|VM with Instance Level Public IP address (with or without load balancer)|SNAT is not used|Azure uses the public IP assigned to the VM|

If you do not want a VM to communicate with endpoints outside of Azure in public IP address space, you can use Network Security Groups (NSG) to block access. Using NSGs is discussed in more detail in [Preventing Public Connectivity](#preventing-public-connectivity).

## Standalone VM with no Instance Level Public IP address

In this scenario, the VM is not part of an Azure Load Balancer pool and does not have an Instance Level Public IP (ILPIP) address assigned to it. When the VM creates an outbound flow, Azure translates the private source IP address of the outbound flow to a public source IP address. The public IP address used for this outbound flow is not configurable. Azure uses Source Network Address Translation (SNAT) to perform this function. Ephemeral ports of the public IP address are used to distinguish individual flows originated by the VM. SNAT dynamically allocates ephemeral ports when flows are created. In this context, the ephemeral ports used for SNAT are referred to as SNAT ports.

SNAT ports are a finite resource that can be exhausted. It is important to understand how they are consumed. One SNAT port is consumed per flow to a single destination IP address. For multiple flows to the same destination IP address, each flow consumes a single SNAT port. This ensures that the flows are unique when originated from the same public IP address to the same destination IP address. Multiple flows, each to a different destination IP address consume a single SNAT port per destination. The destination IP address makes the flows unique.

You can use [Log Analytics for Load Balancer](load-balancer-monitor-log.md) and [Alert event logs to monitor for SNAT port exhaustion messages](load-balancer-monitor-log.md#alert-event-log). When SNAT port resources are exhausted, outbound flows fail until SNAT ports are released by existing flows. Load Balancer uses a 4-minute idle timeout for reclaiming SNAT ports.

## Load-balanced VM with no Instance Level Public IP address

In this scenario, the VM is part of an Azure Load Balancer pool. The VM does not have a public IP address assigned to it. When the load-balanced VM creates an outbound flow, Azure translates the private source IP address of the outbound flow to the public IP address of the public Load Balancer frontend. Azure uses Source Network Address Translation (SNAT) to perform this function. Ephemeral ports of the Load Balancer's public IP address are used to distinguish individual flows originated by the VM. SNAT dynamically allocates ephemeral ports when outbound flows are created. In this context, the ephemeral ports used for SNAT are referred to as SNAT ports.

SNAT ports are a finite resource that can be exhausted. It is important to understand how they are consumed. One SNAT port is consumed per flow to a single destination IP address. For multiple flows to the same destination IP address, each flow consumes a single SNAT port. This ensures that the flows are unique when originated from the same public IP address to the same destination IP address. Multiple flows, each to a different destination IP address consume a single SNAT port per destination. The destination IP address makes the flows unique.

You can use [Log Analytics for Load Balancer](load-balancer-monitor-log.md) and [Alert event logs to monitor for SNAT port exhaustion messages](load-balancer-monitor-log.md#alert-event-log). When SNAT port resources are exhausted, outbound flows fail until SNAT ports are released by existing flows. Load Balancer uses a 4-minute idle timeout for reclaiming SNAT ports.

## VM with an Instance Level Public IP address (with or without Load Balancer)

In this scenario, the VM has an Instance Level Public IP (ILPIP) assigned to it. It does not matter whether the VM is load balanced or not. When an ILPIP is used, Source Network Address Translation (SNAT) is not used. The VM uses the ILPIP for all outbound flows. If your application initiates many outbound flows and you experience SNAT exhaustion, you should consider assigning an ILPIP to avoid SNAT constraints.

## Discovering the public IP used by a given VM

There are many ways to determine the public source IP address of an outbound connection. OpenDNS provides a service that can show you the public IP address of your VM. Using the nslookup command, you can send a DNS query for the name myip.opendns.com to the OpenDNS resolver. The service returns the source IP address that was used to send the query. When you execute the following query from your VM, the response is the public IP used for that VM.

    nslookup myip.opendns.com resolver1.opendns.com

## Preventing Public Connectivity

Sometimes it is undesirable for a VM to be allowed to create an outbound flow or there may be a requirement to manage which destinations can be reached with outbound flows. In this case, you use [Network Security Groups (NSG)](../virtual-network/virtual-networks-nsg.md) to manage the destinations that the VM can reach. When you apply an NSG to a load-balanced VM, you need to pay attention to the [default tags](../virtual-network/virtual-networks-nsg.md#default-tags) and [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).

You must ensure that the VM can receive health probe requests from Azure Load Balancer. If an NSG blocks health probe requests from the AZURE_LOADBALANCER default tag, your VM health probe fails and the VM is marked down. Load Balancer stops sending new flows to that VM.
