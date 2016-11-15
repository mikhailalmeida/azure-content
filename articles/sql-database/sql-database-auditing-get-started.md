<properties
	pageTitle="Get started with SQL database auditing | Microsoft Azure"
	description="Get started with SQL database auditing"
	services="sql-database"
	documentationCenter=""
	authors="ronitr"
	manager="jhubbard"
	editor=""/>

<tags
	ms.service="sql-database"
	ms.workload="data-management"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="10/05/2016"
	ms.author="CarlRabeler; ronitr; giladm"/>

# Get started with SQL database  auditing
Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.

Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.

Auditing enables and facilitates adherence to compliance standards but doesn't guarantee compliance. For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).

+ [Azure SQL Database Auditing overview]
+ [Set up auditing for your database]
+ [Analyze audit logs and reports]

##<a id="subheading-1"></a>Azure SQL Database Auditing overview

SQL Database Auditing allows you to:

- **Retain** an audit trail of selected events. You can define categories of database actions to be audited.
- **Report** on database activity. You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.
- **Analyze** reports. You can find suspicious events, unusual activity, and trends.


There are two **Auditing methods**:

- **Blob auditing** - logs are written to Azure Blob Storage. This is a newer auditing method, which provides **higher performance**, supports **higher granularity object-level auditing**, and is **more cost effective**.
- **Table auditing** - logs are written to Azure Table Storage.

You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.

<!--For each Event Category, auditing of **Success** and **Failure** operations are configured separately.-->

An auditing policy can be defined for a specific database or as a default server policy. A default server auditing policy applies to all existing and newly created databases on a server.


##<a id="subheading-2"></a>Set up auditing for your database

The following section describes the configuration of auditing using the Azure Portal.

###<a id="subheading-2-1">i. Blob Auditing</a>

1. Launch the [Azure Portal](https://portal.azure.com) at https://portal.azure.com.

2. Navigate to the settings blade of the SQL Database / SQL Server you want to audit. In the Settings blade, select **Auditing & Threat detection**.

	<a id="auditing-screenshot"></a>
	![Navigation pane][1]

3. In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings. If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.

	![Navigation pane][2]

4. If you prefer to enable Blob Auditing on the database-level (in addition or instead of server-level auditing), **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose the **Blob** Auditing Type.

	> If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.  

	![Navigation pane][3]

5. Select **Storage Details** to open the Audit Logs Storage Blade. Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom. **Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates.

	<a id="storage-screenshot"></a>
	![Navigation pane][4]

6. If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.

8. Click **Save**.


###<a id="subheading-2-2">ii. Table Auditing</a>

> [AZURE.NOTE] Before setting up **Table auditing**, check if you are using a ["Downlevel Client"](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md). Also, if you have strict firewall settings, please note that the [IP endpoint of your database will change](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md) when enabling Table Auditing.

1. Launch the [Azure Portal](https://portal.azure.com) at https://portal.azure.com.

2. Navigate to the settings blade of the SQL Database / SQL Server you want to audit. In the Settings blade, select **Auditing & Threat detection** (*[see screenshot in Blob Auditing section](#auditing-screenshot)*).

3. In the database auditing configuration blade, you can check the **Inherit settings from server** checkbox to designate that this database will be audited according to its server's settings. If this option is checked, you will see a **View server auditing settings** link that allows you to view or modify the server auditing settings from this context.

	![Navigation pane][2]

4. If you prefer not to inherit Auditing settings from server, **uncheck** the **Inherit Auditing settings from server** option, turn **ON** Auditing, and choose **Table** Auditing Type.

	![Navigation pane][3-tbl]

5. Select **Storage Details** to open the Audit Logs Storage Blade. Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted. **Tip:** Use the same storage account for all audited databases to get the most out of the auditing reports templates (*[see screenshot in Blob Auditing section](#storage-screenshot)*).

6. Click on **Audited Events** to customize which events to audit. In the **Logging by event** blade, click **Success** and **Failure** to log all events, or choose individual event categories.

	> Customizing audited events can also be done via PowerShell or REST API - see the [Automation (PowerShell / REST API)](#subheading-7) section for more details.

	![Navigation pane][5]

7. Once you've configured your auditing settings, you can turn on the new **Threat Detection** (preview) feature, and configure the emails to receive security alerts. Threat Detection allows you to receive proactive alerts on anomalous database activities that may indicate potential security threats. See [Getting Started with Threat Detection](sql-database-threat-detection-get-started.md) for more details.

8. Click **Save**.


##<a id="subheading-3"></a>Analyze audit logs and reports

Audit logs are aggregated in the Azure storage account you chose during setup.

You can explore audit logs using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).

See below specifics for analysis of both **Table** and **Blob** audit logs.

###<a id="subheading-3-1">i. Blob Auditing</a>

Blob Auditing logs are saved as a collection of Blob files within a container named "**sqldbauditlogs**".

For further details about the Blob audit logs storage folder hierarchy, Blob naming convention, and log format, see the [Blob Audit Log Format Reference (doc file download)](https://go.microsoft.com/fwlink/?linkid=829599).

There are several methods to view Blob Auditing logs:

1. Through the Azure Portal - **see method (1) in the [Table Auditing section](#activity-ui) below** (Excel download not supported).

2. Download log files from your Azure Storage Blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).

	Once you have downloaded the log file locally, you can double-click the file to open, view and analyze the logs in SSMS.

	Additional methods:
	- You can **download multiple files simultaneously** via Azure Storage Explorer - right-click on a specific subfolder (e.g. a subfolder that includes all log files for a specific date) and choose "Save as" to save in a local folder.

		After downloading several files (or an entire day, as described above), you can merge them locally as follows:

		**Open SSMS -> File -> Open -> Merge Extended Events -> Choose all files to merge**

	- Programmatically:
		- Extended Events Reader **C# library** ([more info here](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/))
		- Querying Extended Events Files Using **PowerShell** ([more info here](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/))

###<a id="subheading-3-2">ii. Table Auditing</a>

Table Auditing logs are saved as a collection of Azure Storage Tables with a **SQLDBAuditLogs** prefix.

For further details about the Table audit log format, see the [Table Audit Log Format Reference (doc file download)](http://go.microsoft.com/fwlink/?LinkId=506733).

There are several methods to view Table Auditing logs:

<a id="activity-ui"></a>

1. Through the [Azure Portal](https://portal.azure.com) - at the top of the **Auditing & Threat detection** blade, click on **More** and then on **Explore**. An **Audit records** blade will open, where you'll be able to view the logs.
	- You can choose to view specific dates by clicking on **Filter** at the top area of the Audit records blade
	- You can download and view the audit logs in Excel format by clicking on **Open in Excel** at the top area of the Audit records blade

	![Navigation Pane][7]

2. Alternatively, a preconfigured report template is available as a [downloadable Excel spreadsheet](http://go.microsoft.com/fwlink/?LinkId=403540) to help you quickly analyze log data. To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download [here](http://www.microsoft.com/download/details.aspx?id=39379).

	You can also import your audit logs into the Excel template directly from your Azure storage account using Power Query. You can then explore your audit records and create dashboards and reports on top of the log data.

	![Navigation Pane][9]




##<a id="subheading-5"></a>Practices for usage in production
<!--The description in this section refers to screen captures above.-->

###<a id="subheading-6">Auditing Geo-replicated databases</a>

When using Geo-replicated databases, it is possible to set up Auditing on either the Primary database, the Secondary database, or both, depending on the Audit type.

**Table Auditing** - you can configure a separate policy, on either the database or the server level, for each of the two databases (Primary and Secondary) as described in [Set up auditing for your database](#subheading-2-2) section.

**Blob Auditing** - follow these instructions:

1. **Primary database** - turn on **Blob Auditing** either on the server or the database itself, as described in [Set up auditing for your database](#subheading-2-1) section.

2. **Secondary database** - Blob Auditing can only be turned on/off from the Primary database auditing settings.
	- Turn on **Blob Auditing** on the **Primary database**, as described in [Set up auditing for your database](#subheading-2-1) section. (**Note:** Blob Auditing must be enabled on the database itself, not the server).
	- Once Blob Auditing is enabled on the Primary database, it will also become enabled on the Secondary database.
	- **Important:** By default, the **storage settings** for the Secondary database will be identical to those of the Primary database, causing **cross-regional traffic**. You can avoid this by enabling Blob Auditing on the **Secondary Server** and configuring a **local storage** in the Secondary Server storage settings (this will override the storage location for the Secondary database and result in each database saving the Audit logs to a local storage).  


<br>
###<a id="subheading-6">Storage Key Regeneration</a>

In production, you are likely to refresh your storage keys periodically. When refreshing your keys, you need to re-save the auditing policy. The process is as follows:


1. In the storage details blade switch the **Storage Access Key** from *Primary* to *Secondary*, and then click **OK** at the bottom. Then click **SAVE** at the top of the auditing configuration blade.

	![Navigation Pane][6]

2. Go to the storage configuration blade and **regenerate** the *Primary Access Key*.

	![Navigation Pane][8]

3. Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary*, and then click **OK** at the bottom. Then click **SAVE** at the top of the auditing configuration blade.

4. Go back to the storage configuration blade and **regenerate** the *Secondary Access Key* (in preparation for the next keys refresh cycle).

##<a id="subheading-7"></a>Automation (PowerShell / REST API)

You can also configure Auditing in Azure SQL Database using the following automation tools:

1. **PowerShell cmdlets**

	- [Get-AzureRMSqlDatabaseAuditingPolicy][101]
	- [Get-AzureRMSqlServerAuditingPolicy][102]
	- [Remove-AzureRMSqlDatabaseAuditing][103]
	- [Remove-AzureRMSqlServerAuditing][104]
	- [Set-AzureRMSqlDatabaseAuditingPolicy][105]
	- [Set-AzureRMSqlServerAuditingPolicy][106]
	- [Use-AzureRMSqlServerAuditingPolicy][107]

2. **REST API - Blob auditing**

	* [Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt695939.aspx)
	* [Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt771861.aspx)
	* [Get Database Blob Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt695938.aspx)
	* [Get Server Blob Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt771860.aspx)
	* [Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/en-us/library/azure/mt771862.aspx)


2. **REST API - Table auditing**

	* [Create or Update Database Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt604471.aspx)
	* [Create or Update Server Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt604383.aspx)
	* [Get Database Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt604381.aspx)
	* [Get Server Auditing Policy](https://msdn.microsoft.com/en-us/library/azure/mt604382.aspx)






<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7


<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[3-tbl]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on_table.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_audited_events.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_storage_key_regeneration.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_activity_log.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_regenerate_key.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_report_template.png


[101]: https://msdn.microsoft.com/en-us/library/azure/mt603731(v=azure.200).aspx
[102]: https://msdn.microsoft.com/en-us/library/azure/mt619329(v=azure.200).aspx
[103]: https://msdn.microsoft.com/en-us/library/azure/mt603796(v=azure.200).aspx
[104]: https://msdn.microsoft.com/en-us/library/azure/mt603574(v=azure.200).aspx
[105]: https://msdn.microsoft.com/en-us/library/azure/mt603531(v=azure.200).aspx
[106]: https://msdn.microsoft.com/en-us/library/azure/mt603794(v=azure.200).aspx
[107]: https://msdn.microsoft.com/en-us/library/azure/mt619353(v=azure.200).aspx
