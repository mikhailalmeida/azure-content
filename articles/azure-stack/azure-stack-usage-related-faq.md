<properties
	pageTitle="Usage-related FAQs | Microsoft Azure"
	description="List of Azure Stack meters, comparison to Azure usage API, Usage Time and Reported Time, error codes."
	services="azure-stack"
	documentationCenter=""
	authors="AlfredoPizzirani"
	manager="byronr"
	editor=""/>

<tags
	ms.service="azure-stack"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="10/18/2016"
	ms.author="alfredop"/>

# Azure Stack Usage API FAQs
This article answers some frequently asked questions about the Azure Stack Usage API.

## What meter IDs can I see?

Currently, usage is reported for the network, storage, and compute
resource providers.

| **Resource provider** | **Meter ID** |**Meter name** | **Unit** | **Additional info** |
| --------------------------- | --------------------------------------- | -------------------------- | ---------------------------- | ----------------------------------------- |
| **Network ** | f114cb19-ea64-40b5-bcd7-aee474b62853 | Public IP Address Usage | IP address |                    
| **Storage**  | B4438D5D-453B-4EE1-B42A-DC72E377F1E4 | TableCapacity | GB\*hours | Total capacity consumed by tables |
|              | B5C15376-6C94-4FDD-B655-1A69D138ACA3 | PageBlobCapacity | GB\*hours | Total capacity consumed by page blobs |
|              | B03C6AE7-B080-4BFA-84A3-22C800F315C6 | QueueCapacity  | GB\*hours  | Total capacity consumed by queue |
| | 09F8879E-87E9-4305-A572-4B7BE209F857 | BlockBlobCapacity | GB\*hours  | Total capacity consumed by block blobs |
| | B9FF3CD0-28AA-4762-84BB-FF8FBAEA6A90 | TableTransactions  | Request count in 10,000s   | Table service requests (in 10,000s) |
| | 50A1AEAF-8ECA-48A0-8973-A5B3077FEE0D | TableDataTransIn | Ingress data in GB | Table service data ingress in GB |
| | 1B8C1DEC-EE42-414B-AA36-6229CF199370 | TableDataTransOut | Outgress in GB | Table service data egress in GB |
| | 43DAF82B-4618-444A-B994-40C23F7CD438 | BlobTransactions | Requests count in 10,000s | Blob service requests (in 10,000s) |
| | 9764F92C-E44A-498E-8DC1-AAD66587A810   | BlobDataTransIn    | Ingress data in GB          | Blob service data ingress in GB 
| | 3023FEF4-ECA5-4D7B-87B3-CFBC061931E8   | BlobDataTransOut   | Outgress in GB              | Blob service data egress in GB 
| | EB43DD12-1AA6-4C4B-872C-FAF15A6785EA   | QueueTransactions  | Requests count in 10,000s   | Queue service requests (in 10,000s) 
| | E518E809-E369-4A45-9274-2017B29FFF25   | QueueDataTransIn          | Ingress data in GB         | Queue service data ingress in GB 
| | DD0A10BA-A5D6-4CB6-88C0-7D585CEF9FC2   | QueueDataTransOut         | Outgress in GB  | Queue service data egress in GB 
| **Compute** | 6DAB500F-A4FD-49C4-956D-229BB9C8C793 | VM Size Hours | Virtual machine size |



## How do the Azure Stack Usage APIs compare to the [Azure Usage API](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) (currently in public preview)?

-   The Tenant Usage API is consistent with the Azure API, with one
    exception: the *showDetails* flag currently is not supported in
    Azure Stack.

-   The Provider Usage API applies only to Azure Stack.

-   Currently, the [RateCard
    API](https://msdn.microsoft.com/en-us/library/azure/mt219004.aspx)
    that is available in Azure is not available in Azure Stack.

## What is the difference between Usage Time and Reported Time?

Usage data reports have two main time values:

-   **Reported Time**. The time when the usage event entered the usage
    system

-   **Usage Time**. The time when the Azure Stack resource was consumed

You might see a discrepancy in values for Usage Time and Reported Time
for a specific usage event. The delay can be as long as multiple hours
in any environment.

Currently, you can query *only by Reported Time*.

## What do these Usage API error codes mean?

| **HTTP status code** | **Error code** | **Description** |
| ---------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| 400/Bad Request        | *NoApiVersion*     | The *api-version* query parameter is missing.
| 400/Bad Request        | *InvalidProperty*  | A property is missing or has an invalid value. The message in the error code in the response body identifies the missing property.
| 400/Bad Request        | *RequestEndTimeIsInFuture*  | The value for *ReportedEndTime* is in the future. Values in the future are not allowed for this argument.
| 400/Bad Request        | *SubscriberIdIsNotDirectTenant*    | A provider API call used a subscription ID that is not a valid tenant of the caller.
| 400/Bad Request        | *SubscriptionIdMissingInRequest*   | The subscription ID of the caller is missing.
| 400/Bad Request        | *InvalidAggregationGranularity*   | An invalid aggregation granularity was requested. Valid values are daily and hourly.
| 503                    | *ServiceUnavailable*   | A retryable error occurred because the service is busy or the call is being throttled. |

## Next Steps
[Customer billing and chargeback in Azure Stack](azure-stack-billing-and-chargeback.md)

[Provider Resource Usage API](azure-stack-provider-resource-api.md)

[Tenant Resource Usage API](azure-stack-tenant-resource-usage-api.md)
