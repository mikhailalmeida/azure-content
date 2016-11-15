<properties
   pageTitle="Collect logs by using Linux Azure Diagnostics | Microsoft Azure"
   description="This article describes how to set up Azure Diagnostics to collect logs from a Service Fabric Linux cluster running in Azure."
   services="service-fabric"
   documentationCenter=".net"
   authors="mani-ramaswamy"
   manager="timlt"
   editor=""/>

<tags
   ms.service="service-fabric"
   ms.devlang="dotNet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="09/28/2016"
   ms.author="subramar"/>


# Collect logs by using Azure Diagnostics

> [AZURE.SELECTOR]
- [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
- [Linux](service-fabric-diagnostics-how-to-setup-lad.md)

When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location. Having the logs in a central location makes it easy to analyze and troubleshoot issues, whether they are in your services, your application, or the cluster itself. One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage. You can read the events from storage and place them in a product such as [Elastic Search](service-fabric-diagnostic-how-to-use-elasticsearch.md) or another log-parsing solution.

## Log sources that you might want to collect
- **Service Fabric logs**: Emitted from the platform via [LTTng](http://lttng.org) and uploaded to your storage account. Logs can be operational events or runtime events that the platform emits. These logs are stored in the location that the cluster manifest specifies. (To get the storage account details, search for the tag **AzureTableWinFabETWQueryable** and look for **StoreConnectionString**.)
- **Application events**: Emitted from your service's code. You can use any logging solution that writes text-based log files--for example, LTTng. For more information, see the LTTng documentation on tracing your application.  


## Deploy the Diagnostics extension
The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster. The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify. The steps vary based on whether you use the Azure portal or Azure Resource Manager.

To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, set **Diagnostics** to **On**. After you create the cluster, you can't change this setting by using the portal.

Then, configure Linux Azure Diagnostics (LAD) to collect the files and place them into your storage account. This process is explained as scenario 3 ("Upload your own log files") in the article [Using LAD to monitor and diagnose Linux VMs](../virtual-machines/virtual-machines-linux-classic-diagnostic-extension.md). Following this process gets you access to the traces. You can upload the traces to a visualizer of your choice.

You can also deploy the Diagnostics extension by using Azure Resource Manager. The process is similar for Windows and Linux and is documented for Windows clusters in [How to collect logs with Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

You can also use Operations Management Suite, as described in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

After you finish this configuration, the LAD agent monitors the specified log files. Whenever a new line is appended to the file, it creates a syslog entry that is sent to the storage that you specified.


## Next steps
To understand in more detail what events you should examine while troubleshooting issues, see [LTTng documentation](http://lttng.org/docs) and [Using LAD](../virtual-machines/virtual-machines-linux-classic-diagnostic-extension.md).
