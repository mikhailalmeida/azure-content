<properties
	pageTitle="Create a VM image from an Azure VM | Microsoft Azure"
	description="Learn how to create a generalized VM image from an existing Azure VM created in the Resource Manager deployment model"
	services="virtual-machines-windows"
	documentationCenter=""
	authors="cynthn"
	manager="timlt"
	editor=""
	tags="azure-resource-manager"/>

<tags
	ms.service="virtual-machines-windows"
	ms.workload="infrastructure-services"
	ms.tgt_pltfrm="vm-windows"
	ms.devlang="na"
	ms.topic="article"
	ms.date="10/10/2016"
	ms.author="cynthn"/>


# Download the template for a VM

When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you. You can use this template to quickly duplicate a deployment. The template contains information about all of the resources in a resource group. For a virtual machine, this means the template containers everything that is created in support of the VM in that resource group, including the networking resources.

## Download the template using the portal

1. Log in to the [Azure portal](https://portal.azure.com/).
2. One the hub menu, select **Virtual Machines**.
3. Select the virtual machine from the list.
5. Select **Automation script**.
6. Select **Download** and save the .zip file to your local computer.
7. Open the .zip file and extract the files to a folder. The .zip file will contain:
	
	- deploy.ps1
	- deploy.sh 
	- deployer.rb
	- DeploymentHelper.cs
	- parameters.json
	- template.json

The .json file is the template.
	
## Download the template using PowerShell

You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. You can use the `-path` parameter to provide the filename and path for the .json file. This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.

```powershell
	Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## Next steps

To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../resource-manager-template-walkthrough.md).