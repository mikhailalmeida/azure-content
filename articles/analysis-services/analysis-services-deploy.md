<properties
   pageTitle="Deploy to Azure Analysis Services | Microsoft Azure"
   description="Learn how to deploy a tabular model to an Azure Analysis Services server."
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

# Deploy to Azure Analysis Services

Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it. You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on. Or, you can use SQL Server Management Studio (SSMS) to deploy an existing tabular model database from an Analysis Services instance.

## Before you begin
To get started, you need:

- **Analysis Services server** in Azure. To learn more, see [Create an Analysis Services in Azure](analysis-services-create-server.md).
- **Tabular model project** in SSDT or an existing tabular model at the 1200 compatibility level on an Analysis Services instance. Never created one? Try the [Adventure Works Tutorial](https://msdn.microsoft.com/library/hh231691.aspx).
- **On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md). The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.

## To deploy a tabular model from SSDT
In order to deploy from SSDT, make sure you're using the [latest version](https://msdn.microsoft.com/library/mt204009.aspx), updated September 30th, 2016 or later.


> [AZURE.TIP] Before you deploy, make sure you can process the data in your tables. In SSDT, click **Model** > **Process** > **Process All**. If processing fails, deploying will to.

1. Before you deploy, you need to get the server name. In **Azure portal** > server > **Overview** > **Server name**, copy the server name.

    ![Get server name in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)

2. In SSDT > **Solution Explorer**, right-click the project > **Properties**. Then in **Deployment** > **Server** paste the server name.   

    ![Paste server name into deployment server property](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)

3. In **Solution Explorer**, right-click **Properties**, then click **Deploy**. You may be prompted to sign in to Azure.

    ![Deploy to server](./media/analysis-services-deploy/aas-deploy-deploy.png)

    Deployment status appears in both the Output window and in Deploy.

    ![Deployment status](./media/analysis-services-deploy/aas-deploy-status.png)

That's all there is to it!

## To deploy using XMLA script
1. In SSMS, right-click the tabular model database you want to deploy, click **Script** > **Script Database as** > **CREATE to**, then choose a location.

2. Execute the query on the server instance you want to deploy to. If you're deploying to the same server, you must at least change the **name** property in the XMLA script.  


## But, something went wrong

If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server. Make sure you can connect to your server using SSMS. Then make sure the Deployment Server property for the project is correct.

If deployment fails on a table, it's likely because your server couldn't connect to a data source. If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).

## Next steps

Now that you have your tabular model deployed to your server, you're ready to connect to it. You can [connect to it with SSMS](analysis-services-manage.md) to manage it. And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.
