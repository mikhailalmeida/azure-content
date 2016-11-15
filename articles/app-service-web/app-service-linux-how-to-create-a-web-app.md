<properties
	pageTitle="How to create a web app with App Service on Linux | Microsoft Azure"
	description="Web app creation workflow for App Service on Linux."
	keywords="azure app service, web app, linux, oss"
	services="app-service"
	documentationCenter=""
	authors="naziml"
	manager="wpickett"
	editor=""/>

<tags
	ms.service="app-service"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="10/10/2016"
	ms.author="naziml"/>

# Create a web app with App Service on Linux

## Use the Azure portal to create your web app
You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:

![Start creating a web app on the Azure portal][1]

Next, the **Create blade** opens as shown in the following image:

![The Create blade][2]

1. 	Give your web app a name.
2.	Choose an existing resource group or create a new one. (See available regions in the [limitations section](./app-service-linux-intro.md).)
3.	Choose an existing Azure App Service plan or create a new one. (See App Service plan notes in the [limitations section](./app-service-linux-intro.md).)
4.	Choose the application stack that you intend to use. You can choose between several versions of Node.js and PHP.

Once you have created the app, you can change the application stack from the application settings as shown in the following image:

![Application settings][3]

## Deploy your web app

Choosing **deployment options** from the management portal gives you the option to use local a Git or GitHub repository to deploy your application. The rest of the instructions are similar to those for a non-Linux web app, and you can follow these instructions in either our [local Git deployment](./app-service-deploy-local-git.md) or our [continuous deployment](./app-service-continuous-deployment.md) article for GitHub.

You can also use FTP to upload your application to your site. You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:

![Diagnostics logs][4]


## Next steps ##

* [What is App Service on Linux?](./app-service-linux-intro.md)
* [Using PM2 Configuration for Node.js in Web Apps on Linux](./app-service-linux-using-nodejs-pm2.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
