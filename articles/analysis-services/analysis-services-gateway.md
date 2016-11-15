<properties
   pageTitle="On-premises data gateway | Microsoft Azure"
   description="An On-premises gateway is necessary if your Analysis Services server in Azure will connect to on-premises data sources."
   services="analysis-services"
   documentationCenter=""
   authors="minewiskan"
   manager="erikre"
   editor=""
   tags=""/>
<tags
   ms.service="analysis-services"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="na"
   ms.date="10/24/2016"
   ms.author="owend"/>

# On-premises data gateway

The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services server in the cloud.

A gateway is installed on a computer in your network. One gateway must be installed for each Azure Analysis Services server you have in your Azure subscription. For example, if you have two servers in your Azure subscription that connect to on-premises data sources, a gateway must be installed on two separate computers in your network.

## Requirements

**Minimum Requirements:**

- .NET 4.5 Framework
- 64-bit version of Windows 7 / Windows Server 2008 R2 (or later)

**Recommended:**

- 8 Core CPU
- 8 GB Memory
- 64-bit version of Windows 2012 R2 (or later)

**Important considerations:**

- The gateway cannot be installed on a domain controller.

- Only one gateway can be installed on a single computer.

- Install the gateway on a computer that remains on and does not go to sleep. If the computer is not on, your Azure Analysis Services server cannot connect to your on-premises data sources to refresh data.

- Do not install the gateway on a computer wirelessly connected to your network. Performance can be diminished.

- To change the server name for a gateway that has already been configured, you need to reinstall and configure a new gateway.

- In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error. To learn more, see [Datasource connections](analysis-services-datasource.md).

## Supported on-premises data sources
For preview, the gateway supports connections between your Azure Analysis Services server and the following on-premises data sources:

- SQL Server
- SQL Data Warehouse
- APS
- Oracle
- Teradata


## Download
 [Download the gateway](https://aka.ms/azureasgateway)


## Install and configure

1. Run setup.

2. Choose an installation location and accept the license terms.

3. Sign in to Azure.

4. Specify your Azure Analysis Server name. You can only specify one server per gateway. Click **Configure** and you're good to go.

    ![sign in to azure](./media\analysis-services-gateway\aas-gateway-configure-server.png)


## How it works
The gateway runs as a Windows service, **On-premises data gateway**, on a computer in your organization's network. The gateway you install for use with Azure Analysis Services is based on the same gateway used for other services like Power BI, but with some differences in how it's configured.

![How it works](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Queries and data flow work like this:

1.	A query is created by the cloud service with the encrypted credentials for the on-premises data source. It's then sent to a queue for the gateway to process.

2.	The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).

3.	The on-premises data gateway polls the Azure Service Bus for pending requests.

4.	The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.

5.	The gateway sends the query to the data source for execution.

6.	The results are sent from the data source, back to the gateway, and then onto the cloud service.

## Windows Service account

The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential. By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on. This credential is not the same account used to connect to on-premises data sources or your Azure account.  

If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.

## Ports

The gateway creates an outbound connection to Azure Service Bus. It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.  The gateway does not require inbound ports.

It's recommended you whitelist the IP addresses for your data region in your firewall. You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653). This list is updated weekly.

> [AZURE.NOTE]  The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation. For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24. Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).

The following are the fully qualified domain names used by the gateway.

|Domain names|Outbound ports|Description|
|---|---|---|
|*.powerbi.com|80|HTTP used to download the installer.|
|*.powerbi.com|443|HTTPS|
|*.analysis.windows.net|443|HTTPS|
|*.login.windows.net|443|HTTPS|
|*.servicebus.windows.net|5671-5672|Advanced Message Queuing Protocol (AMQP)|
|*.servicebus.windows.net|443, 9350-9354|Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)|
|*.frontend.clouddatahub.net|443|HTTPS|
|*.core.windows.net|443|HTTPS|
|login.microsoftonline.com|443|HTTPS|
|*.msftncsi.com|443|Used to test internet connectivity if the gateway is unreachable by the Power BI service.|
|*.microsoftonline-p.com|443|Used for authentication depending on configuration.|


### Forcing HTTPS communication with Azure Service Bus

You can force the gateway to communicate with Azure Service Bus using HTTPS instead of direct TCP; however, this can greatly reduce performance. You need to modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file. Change the value from `AutoDetect` to `Https`. This file is located, by default, at *C:\Program Files\On-premises data gateway*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```


## Troubleshooting
Under the hood, the on-premises data gateway used for connecting Azure Analysis Services to your on-premises data sources is the same gateway used with Power BI.

If you’re having trouble when installing and configuring a gateway, be sure to see [Troubleshooting the Power BI Gateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem-tshoot/). If you think you are having an issue with your firewall, see the firewall or proxy sections.

If you think you're encountering proxy issues, with the gateway, see [Configuring proxy settings for the Power BI Gateways](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy.md).

## Next steps
- [Manage Analysis Services](analysis-services-manage.md)
- [Get data from Azure Analysis Services](analysis-services-connect.md)
