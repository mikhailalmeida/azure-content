<properties
	pageTitle="Azure Machine Learning FAQ | Microsoft Azure"
	description="Azure Machine Learning introduction: FAQ covering billing, capabilities, and limitations of a cloud service for streamlined predictive modeling."
	keywords="machine learning introduction,predictive modeling,what is machine learning"
	services="machine-learning"
	documentationCenter=""
	authors="garyericson"
	manager="paulettm"
	editor="cgronlun"/>

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.date="10/26/2016"
	ms.author="garye"/>

# Azure Machine Learning Frequently Asked Questions (FAQ): Billing, capabilities, limitations, and support

This FAQ answers questions about Azure Machine Learning, a cloud service for developing predictive models and operationalizing solutions through web services. This FAQ covers questions about using the service, including the billing model, capabilities, limitations, and support.

## General questions

**What is Azure Machine Learning?**

Azure Machine Learning is a fully managed service that you can use to create, test, operate, and manage predictive analytic solutions in the cloud. With only a browser, you can sign-in, upload data, and immediately start machine learning experiments. Drag-and-drop predictive modeling, a large pallet of modules, and a library of starting templates makes common machine learning tasks simple and quick.  For more information, see the [Azure Machine Learning service overview](https://azure.microsoft.com/services/machine-learning/). For a machine learning introduction covering key terminology and concepts, see [Introduction to Azure Machine Learning](machine-learning-what-is-machine-learning.md).

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**What is Machine Learning Studio?**

Machine Learning Studio is a workbench environment you access through a web browser. Machine Learning Studio hosts a pallet of modules with a visual composition interface that enables you to build an end-to-end, data science workflow in the form of an experiment.

For more information about Machine Learning Studio, see [What is Machine Learning Studio?](machine-learning-what-is-ml-studio.md)

**What is the Machine Learning API service?**

The Machine Learning API service enables you to deploy predictive models, such as those built in Machine Learning Studio, as scalable, fault-tolerant, web services. The web services created by the Machine Learning API service are REST APIs that provide an interface for communication between external applications and your predictive analytics models.

For more information, see [Connect to a Machine Learning web service](machine-learning-connect-to-azure-machine-learning-web-service.md).

**Where are my classic web services listed? Where are my new Azure Resource Manager based web services listed?**

Classic Web services and New Azure Resource Manager based Web services are listed in the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal. 

Classic Web services are also listed in [Machine Learning Studio](http://studio.azureml.net) on the Web services tab.

## Microsoft Azure Machine Learning Web Service questions

**What are Azure Machine Learning Web Services?**

Machine Learning Web Services provide an interface between an application and a Machine Learning workflow scoring model. Using the Azure Machine Learning web service, an external application can communicate with a Machine Learning workflow scoring model in real time. A Machine Learning web service call returns prediction results to an external application. To make a Machine Learning web service call, you pass an API key that was created when you deployed the web service. The Machine Learning web service is based on REST, a popular architecture choice for web programming projects.

Azure Machine Learning has two types of services:

* Request-Response Service (RRS) - A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.
* Batch Execution Service (BES) - An asynchronous service that scores a batch for data records.

There are several ways to consume the REST API and access the web service. For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service.

The sample code is available on:
The Consume page for the Web service in the Azure Machine Learning Web Services portal.
The API Help Page in the Web service dashboard in Machine Learning Studio.

Or you can use the sample Microsoft Excel workbook created for you (also available in the web service dashboard in Studio).

**What are the main updates with the new Azure ML Web Services?**

For more information about the New Azure Machine Learning Web Services, refer to the [related documentation](machine-learning-whats-new.md).

## Machine Learning Studio questions

### Importing and exporting data for Machine Learning

**What data sources does Machine Learning support?**

Data can be loaded into a Machine Learning Studio experiment in one of three ways: by uploading a local file as a dataset, by using a module to import data from cloud data services, or by importing a dataset saved from another experiment. To learn more about supported file formats, see [Import training data into Machine Learning Studio](machine-learning-data-science-import-data.md).


#### <a id="ModuleLimit"></a>How large can the data set be for my modules?

Modules in Machine Learning Studio support datasets of up to 10 GB of dense numerical data for common use cases. If a module takes more than one input, the 10 GB is the total of all input sizes. You can also sample larger datasets via Hive or Azure SQL Database queries, or by Learning by Counts pre-processing, before ingestion.  

The following types of data can expand into larger datasets during feature normalization, and are limited to less than 10 GB:

- Sparse
- Categorical
- Strings
- Binary data

The following modules are limited to datasets less than 10GB:

- Recommender modules
- SMOTE module
- Scripting modules: R, Python, SQL
- Modules where the output data size can be larger than input data size, such as Join or Feature Hashing.
- Cross-validation, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when number of iterations is very large.

For datasets larger than a few GB, you should upload data to Azure storage or Azure SQL Database or use HDInsight, rather than directly uploading from local file.


####<a id="UploadLimit"></a>What are the limits for data upload?
For datasets larger than a couple GB, upload data to Azure storage or Azure SQL Database or use HDInsight, rather than directly uploading from local file.

**Can I read data from Amazon S3?**

If you have a small amount of data and want to expose it via an http URL, then you can use the [Import Data][import-data] module. For any larger amounts of data to transfer it to Azure Storage first and then use the [Import Data][import-data] module to bring it into your experiment.
<!--
<SEE CLOUD DS PROCESS>
-->

**Is there a built-in image input capability?**

You can learn about image input capability in the [Import Images][image-reader] reference.

### Modules

**The algorithm, data source, data format, or data transformation operation I am looking for isn't in Azure Machine Learning Studio. What are my options?**

You can visit the [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231) to see feature requests that we are tracking. Add your vote to a request if a capability you're looking for has already been requested. If the capability you're looking for doesn't exist, create a new request. You can view the status of your request in this forum too. We track this list closely and update the status of feature availability frequently. In addition, with the built-in support for R and Python custom transformations can be created as needed.


**Can I bring my existing code into Machine Learning Studio?**

Yes, you can bring your existing R or Python code into Machine Learning Studio, run it in the same experiment with Azure Machine Learning learners, and deploy the solution as a web service via Azure Machine Learning. For more information, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) and [Execute Python machine learning scripts in Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).

**Is it possible to use something like [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) to define a model?**

No, that is not supported, however custom R and Python code can be used to define a module.

**How many modules can I execute in parallel in my experiment?**  

You can execute up to four modules in parallel in an experiment.


### Data processing

**Is there an ability to visualize data (beyond R visualizations) interactively within the experiment?**

By clicking the output of a module, you can visualize the data and get statistics.

**When previewing results or data in the browser, the number of rows and columns is limited, why?**

Since the data is being transmitted to the browser and may be large, the data size is limited to prevent slowing down Machine Learning Studio. To visualize all the data/result, it's better to download the data and use Excel or another tool.

### Algorithms

**What existing algorithms are supported in Machine Learning Studio?**

Machine Learning Studio provides state-of-the-art algorithms, such as Scalable Boosted Decision trees, Bayesian Recommendation systems, Deep Neural Networks, and Decision Jungles developed at Microsoft Research. Scalable open-source machine learning packages like Vowpal Wabbit are also included. Machine Learning Studio supports machine learning algorithms for multiclass and binary classification, regression, and clustering. See the complete list of [Machine Learning Modules][machine-learning-modules].

**Do you automatically suggest the right Machine Learning algorithm to use for my data?**

No, however there are various ways in Machine Learning Studio to compare the results of each algorithm to determine the right one for your problem.

**Do you have any guidelines on picking one algorithm over another for the provided algorithms?**
See [How to choose an algorithm](machine-learning-algorithm-choice.md).

**Are the provided algorithms written in R or Python?**

No, these algorithms are mostly written in compiled languages to provide higher performance.

**Are any details of the algorithms provided?**

The documentation provides some information about the algorithms, and the parameters provided for tuning are described to optimize the algorithm for your use.  

**Is there any support for online learning?**

No, currently only programmatic retraining is supported.

**Can I visualize the layers of a Neural Net Model using the built-in Module?**

No.

**Can I create my own modules in C# or some other language?**

Currently new custom modules can only be created in R.

### R module

**What R packages are available in Machine Learning Studio?**

Machine Learning Studio supports 400+ CRAN R packages today, and here is the [current list](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) of all included packages. Also, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) to learn how to retrieve this list yourself. If the package you want is not in this list, provide the name of package at [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231).

**Is it possible to build a custom R module?**

Yes, see [Author custom R modules in Azure Machine Learning](machine-learning-custom-r-modules.md) for more information.

**Is there a REPL environment for R?**

No, there is no REPL environment for R in the studio.

### Python module

**Is it possible to build a custom Python module?**

Not currently, but you can use one or more [Execute Python Script][python] modules to get the same result.

**Is there a REPL environment for Python?**

You can use the Jupyter Notebooks in Machine Learning Studio. For more information, see [Introducing Jupyter Notebooks in Azure Machine Learning Studio] (http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).

## Web service

###Retraining Models Programmatically

**How do I Retrain Azure Machine Learning models programmatically?**

Use the Retraining APIs. for more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md). Sample code is also available in the [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).

### Create

**Can I deploy the model locally or in an application without an internet connection?**

No.


**Is there a baseline latency that is expected for all web services?**

See the [Azure subscription limits](../azure-subscription-service-limits.md)

### Use

**When would I want to run my predictive model as a Batch Execution service versus a Request Response service?**

The Request Response service (RRS) is a low-latency, high-scale web service that is used to provide an interface to stateless models that are created and deployed from the experimentation environment. The Batch Execution service (BES) is a service for asynchronously scoring a batch of data records. The input for BES is similar to data input used in RRS. The main difference is that BES reads a block of records from a variety of sources, such as the Blob service and Table service in Azure, Azure SQL Database, HDInsight (hive query), and HTTP sources. For more information, see [How to consume Machine Learning web services](machine-learning-consume-web-services.md).

**How do I update the model for the deployed web service?**

Updating a predictive model for an already deployed service is as simple as modifying and rerunning the experiment that you used to author and save the trained model. Once you have a new version of the trained model available, Machine Learning Studio asks you if you want to update your web service. For details on how to update a deployed web service, see [Deploy a Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).

You can also use the Retraining APIs.
For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md). Sample code is also available in the [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).

**How do I monitor my web service deployed in production?**

Once a predictive model has been deployed, you can monitor it from the Azure classic portal (Classic web services only) or the Azure Machine Learning Web Services portal. Each deployed service has its own dashboard where you can see monitoring information for that service. For more information on managing your deployed web services, see  [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) and [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).

**Is there a place where I can see the output of my RRS/BES?**

For RRS, the web service response is typically where you see the result. You can also write it to Azure blob storage. For BES, the output is written to a blob by default. You can also write the output to a database or table using the [Export Data][export-data] module.

**Can I create web services only from models created in Machine Learning Studio?**

No, you can also create web services directly from Jupyter Notebooks and RStudio.

**Where can I find information about error codes?**

See [Machine Learning Module Error Codes](https://msdn.microsoft.com/library/azure/dn905910.aspx) for a list of error codes and descriptions.

## Scalability

**What is the scalability of the web service?**

Currently, the default endpoint is provisioned with 20 concurrent RRS requests per endpoint. You can scale this to 200 concurrent requests per endpoint and you can scale each web service to 10,000 endpoints per web service as described in [Scaling a Web Service](machine-learning-scaling-webservice.md). For BES, each endpoint allows processing 40 requests at a time and additional requests beyond 40 requests are queued. These queued requests run automatically as the queue drains.


**Are R jobs spread across nodes?**

No.  


**How much data can I use for training?**

Modules in Machine Learning Studio support datasets of up to 10 GB of dense numerical data for common use cases. If a module takes more than one input, the total size for all inputs together is 10 GB. You can also sample larger datasets via Hive or Azure SQL Database queries, or by pre-processing with [Learning with Counts][counts] modules before ingestion.  

The following types of data can expand into larger datasets during feature normalization, and are limited to less than 10 GB:

- sparse
- categorical
- strings
- binary data

The following modules are limited to datasets less than 10 GB:

- Recommender modules
- SMOTE module
- Scripting modules: R, Python, SQL
- Modules where the output data size can be larger than input data size, such as Join or Feature Hashing.
- Cross-Validate, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when number of iterations is very large.

For datasets larger than a few GB, you should upload data to Azure storage or Azure SQL Database, or use HDInsight, rather than directly uploading from a local file.


**Are there any vector size limitations?**

Rows and columns are each limited to the .NET limitation of Max Int: 2,147,483,647.

**Can the size of the virtual machine being used to run the web service be adjusted?**

No.  

## Security and availability

**Who has access to the http endpoint for the web service by default? How do I restrict access to the endpoint?**

After a web service is deployed, a default endpoint is created for that service. The default endpoint can be called using its API Key. Additional endpoints can be added with their own keys from the Azure classic portal or programmatically using the Web Service Management APIs. Access keys are needed to make calls to the web service. For more information, see [Connect to a Machine Learning web service](machine-learning-connect-to-azure-machine-learning-web-service.md).


**What happens if my Azure storage account can't be found?**

Machine Learning Studio relies on a user supplied Azure storage account to save intermediary data when executing the workflow. This storage account is provided to Machine Learning Studio at the time a workspace is created. After the workspace is created, if the storage account is deleted and can no longer be found, the workspace will stop functioning and all experiments in that workspace will fail.

If you accidentally deleted the storage account, recreate the storage account with the same name in the same region as the deleted storage account. After that, resync the Access Key.


**What happens if my storage account access key is out of sync?**

Machine Learning Studio relies on a user supplied Azure storage account to store intermediary data when executing the workflow. This storage account is provided to Machine Learning Studio at the time a workspace is created and the Access Keys are associated with that workspace. if the Access Keys are changed, after the workspace is created, the workspace can no longer access the storage account. It will stop functioning and all experiments in that workspace will fail.

If you have changed storage account Access Keys, resync the Access Keys in the workspace using the Azure classic portal.  


## Azure Marketplace

See the [FAQ for publishing and using apps in the Machine Learning Marketplace](machine-learning-marketplace-faq.md).

## Support and training

**Where can I get training for Azure Machine Learning?**

[Azure Machine Learning Documentation Center](https://azure.microsoft.com/services/machine-learning/) hosts video tutorials and how-to guides. These step-by-step guides provide an introduction to the services and walk through the data science life cycle of importing data, cleaning data, building predictive models and deploying them in production with Azure Machine Learning.

We are adding new material to the Machine Learning Center on an ongoing basis. You can submit requests for additional learning material on Machine Learning Center at the [user feedback forum](https://windowsazure.uservoice.com/forums/257792-machine-learning).

You can also find training at [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**How do I get support for Azure Machine Learning?**

To get technical support for Azure Machine Learning, go to [Azure Support](/support/options/) and select **Machine Learning**.

Azure Machine Learning also has a community forum on MSDN where you can ask questions related to Azure Machine Learning. The forum is monitored by the Azure Machine Learning team. Visit [Azure Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## Billing questions

**How does Machine Learning billing work?**

There are two components to the Azure Machine Learning service. The Machine Learning Studio and Machine Learning Web Services.

While you are evaluating Machine Learning Studio, you can use the free billing tier.  The free tier also allows you to deploy a classic web service with limited capacity.

Once you have decided that Azure Machine Learning meets your needs, you can sign up for the standard tier. To sign up, you must have a Microsoft Azure Subscription.

In the standard tier you are billed a monthly for each workspace you define in Machine Learning Studio. When you run an experiment in the studio, you are billed for compute resources when you are running an experiment. When you deploy a Classic Web Service, transactions and compute hours are billed on a Pay As You Go (PAYG) basis.

The New Machine Learning Web Services introduce Billing Plans that allow for more predictability in costs. Tiered pricing offers discounted rates to customers that need a large amount of capacity.

When you create a plan, you commit to a fixed cost that comes with an included quantity of API compute hours and API transactions. If you need more included quantities, you can add additional instances to your plan. If you need a lot more included quantities, you can choose a higher tier plan that provides considerably more included quantities and a better discounted rate.

After the included quantities in existing instances are used up, additional usage is charged at the overage rate associated with the billing plan tier.

Note: Included quantities are reallocated every 30 days and unused included quantities do not roll over to the next period.

For additional billing and pricing information, see [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/).

**Does Machine Learning have a free trial?**

 Azure Machine Learning has a free subscription option (see [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/) for details), and Machine Learning Studio has an 8-hour quick evaluation trial available (log in to [Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2) for this trial).

 In addition, when you sign up for an Azure free trial, you can try any Azure services for a month. To learn more about the Azure free trial, visit [Azure Free Trial FAQ](/pricing/free-trial-faq/).

**What is a transaction?**

A transaction represents an API call that Azure Machine Learning responds to. Transactions from Request-Response Service (RRS) and Batch Execution Service (BES) calls are aggregated and charged against your billing plan.

**Can I use the included transaction quantities in a plan for both RRS and BES transactions?**

Yes, your transactions from your RRS and BES are aggregated and charged against your billing plan.

**What is an API compute hour?**

An API compute hour is the billing unit for the time API Calls take to run using the ML compute resources. All your calls are aggregated for billing purposes.

**How long does a typical production API call take?**

Production API call times can vary significantly, generally ranging from hundreds of milliseconds to a few seconds, but may require minutes depending on the complexity of the data processing and machine learning model. The best way to estimate production API call times is to benchmark a model on the Machine Learning service.

**What is a Studio Compute hour?**

A Studio Compute hour is the billing unit for the aggregate time your experiments use compute resources in studio.

**In the New Web Services, what is the dev/test tier meant for?**

The Azure ML new Web Services provide multiple tiers that you can use to provision your billing plan. The dev/test tier is a tier that provides limited included quantities that allow you to test your experiment as new web service without incurring costs. You have the opportunity to "Kick the Tires" to see how it works.

**Are there separate storage charges?**

The Machine Learning Free tier does not require or allow separate storage. The Machine Learning Standard tier requires users to have an Azure storage account. Azure storage is [billed separately](https://azure.microsoft.com/pricing/details/storage/).

**How does Machine Learning support high-availability work?**

Production API call times can vary significantly, generally ranging from hundreds of milliseconds to a few seconds, but may require minutes depending on the complexity of the data processing and machine learning model. The best way to estimate production API call times is to benchmark a model on the Machine Learning service.

**What specific kind of compute resources will my production API calls be run on?**

The Machine Learning service is a multitenant service, and actual compute resources used on the backend vary and are optimized for performance and predictability.

### Management of New Web Services

**What happens if I delete my plan?**

The plan is removed from your subscription and you are billed for a prorated usage.

Note: You cannot delete a plan that is in use by a web service. To delete the plan, you must either assign a new plan to the web service or delete the web service.

**What is a plan instance?**

A plan instance is a unit of included quantities that you can add to your billing plan. When you select a billing tier for your billing plan, it comes with one instance. If you need more included quantities, you can add instances of the selected billing tier to your plan.

**How many plan instances can I add?**

You can have one instance of the dev/test tier in a subscription.

For tiers S1, S2, and S3 you can add as many as necessary.

Note: Depending on your anticipated usage, it may be more cost effective to upgrade to a higher included quantities tier rather than add instances to the current tier.

**What happens when I change plan tiers (Upgrade / downgrade)?**

The old plan is deleted and the current usage is billed on a prorated basis. A new plan with the full included quantities of the upgraded/downgraded tier is created for the rest of the period.

Note: Included quantities are allocated per period and unused quantities do not roll over.

**What happens when I increase the instances in a plan?**

Quantities are included on a prorated basis and may take 24 hours to be effective.

**What happens when I delete an instance of a plan?**

The instance is removed from your subscription and you are billed for a prorated usage.


### Signing up for New Web Services plans

**How do I sign up for a plan?**

You have two ways to create billing plans.

When you first deploy a new web service, you can choose an existing plan or create a new plan.

Plans created in this manner are in your default region and your web service will be deployed to that region.

If you want to deploy services to regions other than your default region, you may want to define your billing plans before you deploy your service,

In that case you can log into the Azure Machine Learning Web Services portal and navigate to the plans page. From there, you can Add and Delete plans, as well as modify existing plans.

**Which plan should I choose to start off with?**

We recommend you that you start with the standard S1 tier and monitor your service for usage. If you find you are using your included quantities rapidly, you can add instances or move to a higher tier and get better discounted rates. You can adjust your billing plan as needed throughout your billing cycle.

**Which regions are the new plans available in?**

The new billing plans are available in the three production regions in which we support the new web services:

* South Central US
* West Europe
* South East Asia

**I have web services in multiple regions. Do I need a plan for every region?**

Yes. Plan pricing varies by region. When you deploy a web service to another region, you need to assign it a plan specific to that region.

### New Web Services - Overages

**How do I check if my web service usage is in overage?**

You can view the usage on all your plans on the Plans page in the Azure Machine Learning Web Services portal. sign in to the portal and click the Plans menu option.

In the Transactions and Compute columns of the table, you can see the included quantities of the plan and the percentage used.

**What happens when I use up the include quantities in the dev/test tier?**

Services that have a dev/test tier assigned them are stopped until the next period or you move them to one of the paid tiers.

**For Classic Web Services and Overages of New Web Services, how are prices calculated for Request Response (RRS) and Batch (BES) workloads?**

For an RRS workload, you are charged for every API transaction call that you make and for the compute time associated with those requests. Your RRS Production API Transaction costs are calculated as the total number of API calls that you make multiplied by the price per 1,000 transactions (prorated by individual transaction). Your RRS API Production API Compute Hour costs are calculated as the amount of time required for each API call to run, multiplied by the total number of API transactions multiplied by the price per Production API Compute Hour.

For example for Standard S1 overage, 1,000,000 API Transactions that take 0.72 seconds each to run would result in (1,000,000 * $0.50/1K API transactions) in $500 in Production API Transaction costs and (1,000,000 * 0.72 sec * $2/hr) $400 in Production API Compute Hours, for a total of $900.

For a BES workload, you are charged in the same manner, however, the API transaction costs represent the number of batch jobs that you submit and the compute costs represent the compute time associated with those batch jobs. Your BES Production API Transaction costs are calculated as the total number of jobs submitted multiplied by the price per 1,000 transactions (prorated by individual transaction). Your BES API Production API Compute Hour costs are calculated as the amount of time required for each row in your job to run multiplied by the total number of rows in your job multiplied by the total number of jobs multiplied by the price per Production API Compute Hour. When using the Machine Learning calculator, the transaction meter represents the number of jobs that you plan to submit and the time per transaction field represents the combined time needed for all the rows in each job to run.

For example with Standard S1 overage, if you submit 100 jobs per day that each consist of 500 rows that take 0.72 seconds each, then your monthly overage costs would be (100 jobs per day = 3,100 jobs/mo * $0.50/1K API transactions) $1.55 in Production API Transaction costs and (500 rows * 0.72 sec * 3,100 Jobs * $2/hr) $620 in Production API Compute Hours, for a total of $621.55.

### Azure ML Classic Web Services

**Is the Pay As You Go still available?**
Yes, Classic Web Services are still available in Azure Machine Learning.  

### Azure Machine Learning Free and Standard Tier

**What is included in the Azure Machine Learning Free tier?**

The Azure Machine Learning Free tier is intended to provide an in-depth introduction to the Azure Machine Learning Studio. All you need is a Microsoft account to sign up. The Free tier includes free access to one Azure Machine Learning Studio workspace per [Microsoft account](https://www.microsoft.com/account/default.aspx). It includes the ability to use up to 10 GB of storage and the ability to operationalize models as staging APIs. Free tier workloads are not covered by an SLA and are intended for development and personal use only. Free tier workloads canâ€™t access data by connecting to an on-premises SQL server.

**What is included in the Azure Machine Learning Standard tier and plans?**

The Azure Machine Learning Standard tier is a paid production version of Azure Machine Learning Studio. The Azure ML service Studio monthly fee is billed on a per workspace per month basis and prorated for partial months. Azure ML Studio experiment hours are billed per compute hour for active experimentation. Billing is prorated for partial hours.  

The Azure ML API service is billed depending on whether it's a classic web services or a new web service.

The following charges are aggregated per workspace for your subscription.

* Machine Learning Workspace Subscription - The Machine Learning Workspace Subscription is a monthly fee that provides access to an ML Studio workspace and is required to run experiments both in the studio and utilizing the production APIs.
* Studio Experiment Hours - this meter aggregates all compute charges accrued by running experiments in ML Studio and running production API calls in the staging environment.
* Access data by connecting to an on-premises SQL server in your models for your training and scoring.
* For Classic Web Services:
	* Production API Compute Hours - this meter includes compute charges accrued by Web services running in production.
	* Production API Transactions (in 1000s) - this meter includes charges accrued per call to your production web service.

Apart from the preceding charges, in the case of New Web Services, charges are aggregated to the plan selected:

* Standard S1/S2/S3 API Plan (Units) - this meter represents the type of instance selected for new Web Services
* Standard S1/S2/S3 Overage API Compute Hours - this meter includes compute charges accrued by the New Web Services running in production after the included quantities in existing instance(s) are used up. The additional usage is charged at the overate rate associated with S1/S2/S3 plan tier.
* Standard S1/S2/S3 Overage API Transactions (in 1,000s) - this meter includes charges accrued per call to your production New Web Service after the included quantities in existing instance(s) are used up. The additional usage is charged at the overate rate associated with S1/S2/S3 plan tier.
* Included Quantity API Compute Hours - with the New Web Services, this meter represents the included quantity of API Compute Hours
* Included Quantity API Transactions (in 1,000s) - with the New Web Services, this meter represents the included quantity of API Transactions


**How do I sign up for Azure ML Free tier?**

All you need is a Microsoft account. Go to [Azure Machine Learning home](https://azure.microsoft.com/services/machine-learning/), and click **Start Now**. Log in with your Microsoft account and a workspace in Free tier is created for you. You can start to explore and create Machine Learning experiments right away.

**How do I sign up for Azure ML Standard tier?**

You must first have access to an Azure subscription in order to create a Standard ML workspace. You can sign up for a 30-day free trial Azure subscription and later upgrade to a paid Azure subscription, or purchase a paid Azure subscription outright. You can then create a Machine Learning workspace from the Microsoft Azure classic portal after gaining access to the subscription. View the [step-by-step instructions](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Alternatively, you can be invited by a Standard ML workspace owner to access the owner's workspace.

**Can I specify my own Azure blob storage account to use with the Free tier?**

No, the Standard tier is equivalent to the version of the Machine Learning service that was available before the tiers were introduced.

**Can I deploy my machine learning models as APIs in the Free tier?**

Yes, you can operationalize machine learning models to staging API services as part of the free tier. In order to put the staging API service into production and get a production end point for the operationalized service, you must use the Standard tier.

**What is the difference between Azure Free trial and Azure Machine Learning Free tier?**

The [Microsoft Azure free trial](https://azure.microsoft.com/free/) offers credits that can be applied to any Azure service for one month. The Azure Machine Learning Free tier offers continuous access specifically to the Azure Machine Learning service for non-production workloads.

**How do I move an experiment from the Free tier to the Standard tier?**

To copy your experiments from the Free tier to the Standard tier:

1.	Log into Azure Machine Learning Studio and make sure you can see both the Free workspace and the Standard workspace in the workspace selector in the top navigation bar.
2.	Switch to Free workspace if you are in the Standard workspace.
3.	In the experiment list view, select an experiment you'd like to copy, and click the Copy command button.
4.	Select the Standard workspace from the pop-up dialog box and click the Copy button.
    All the associated datasets, trained model, etc. are copied together with the experiment into the Standard workspace.
6.	You need to rerun the experiment and republish your web service in the Standard workspace.

### Studio Workspace

**Will I see different bills for different workspaces?**

Workspace charges are broken out separately for each applicable meter on a single bill.

**What specific kind of compute resources will my experiments be run on?**

The Machine Learning service is a multitenant service, and actual compute resources used on the backend vary and are optimized for performance and predictability.

### Guest access

**What is Guest Access to Azure Machine Learning Studio?**

Guest Access is a restricted trial experience that allows you to create and run experiments in the Azure Machine Learning Studio at no cost and without authentication. Guest sessions are non-persistent (cannot be saved) and limited to 8 hours. Other limitations include lack of R and Python support, lack of staging APIs and restricted dataset size and storage capacity. By comparison, users who choose to sign in with a Microsoft account have full access to the Free-tier of Machine Learning Studio described above which includes a persistent workspace and more comprehensive capabilities. Choose your free Machine Learning experience by clicking **Get started** on [https://studio.azureml.net](https://studio.azureml.net), and selecting either Guess Access or sign in with a Microsoft account.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
