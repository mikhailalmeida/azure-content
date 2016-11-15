<properties 
	pageTitle="Custom tracking schema| Microsoft Azure" 
	description="Learn more about custom tracking schema" 
	authors="padmavc" 
	manager="erikre" 
	editor="" 
	services="logic-apps" 
	documentationCenter=""/>

<tags
	ms.service="logic-apps"
	ms.workload="integration"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="10/31/2016"
	ms.author="padmavc"/>


# Custom tracking schema

## Supported custom tracking schema  

````java

        {
            "sourceType": "",
            "source": { 
                
            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Property | Description |
| -------- | ------- |
| sourceType | Mandatory.  It indicates the type of the run source, the allowed values are Microsoft.Logic/workflows or custom |
| Source | Mandatory - If the source type is Microsoft.Logic/workflows then the source information need to follow this schema. This schema will be a JToken if the source type is 'custom' |
| systemId | Mandatory, string.  It indicates the logic app system id |
| runId | Mandatory, string.  It indicates the logic app run id |
| operationName | Mandatory, string.  It indicates the name of the operation (for example action or trigger) |
| repeatItemScopeName | Mandatory, string. It indicates the repeat item name if the action is inside a foreach/until loop |
| repeatItemIndex| Mandatory, int.  It indicates the repeat item index if the action is inside a foreach/until loop |
| trackingId | Optional, string. It indicates the tracking id to correlate the messages |
| correlationId | Optional, string. It indicates the correlation id to correlate the messages |
| clientRequestId | Optional, string.  Client can populate it to correlate messages |
| eventLevel | Mandatory. It indicates the level of the event |
| eventTime | Mandatory. It indicates the time of the event in UTC format YYYY-MM-DDTHH:MM:SS.00000Z |
| recordType | Mandatory, It indicates the type of the track record. The allowed values are AS2Message, AS2MDN, X12Interchange, X12FunctionalGroup, X12TransactionSet, X12InterchangeAcknowledgment, X12FunctionalGroupAcknowledgment, X12TransactionSetAcknowledgment, Custom |
| record | Mandatory.  It indicates the custom record type and the allowed format is JToken |
|

## Supported B2B protocol Tracking Schemas
 
* [AS2 Tracking Schema](./app-service-logic-track-integration-account-as2-tracking-shemas.md)   
* [X12 Tracking Schema](./app-service-logic-track-integration-account-x12-tracking-shemas.md) 


## Next steps

[Learn more about tracking B2B messages](./app-service-logic-track-b2b-message.md "Learn more about tracking B2B messages")   
[Learn more about the Enterprise Integration Pack](./app-service-logic-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")   
