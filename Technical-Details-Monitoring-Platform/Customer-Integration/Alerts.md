
## Supported JSON Schema's
The following schema's are supported by ESS monitoring interface. 

###Azure Metric Alert
https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-near-real-time-metric-alerts#payload-schema

```
{"schemaId":"AzureMonitorMetricAlert","data":
    {
    "version": "2.0",
    "status": "Activated",
    "context": {
    "timestamp": "2018-02-28T10:44:10.1714014Z",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/microsoft.insights/metricAlerts/StorageCheck",
    "name": "StorageCheck",
    "description": "",
    "conditionType": "SingleResourceMultipleMetricCriteria",
    "condition": {
      "windowSize": "PT5M",
      "allOf": [
        {
          "metricName": "Transactions",
          "dimensions": [
            {
              "name": "AccountResourceId",
              "value": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
            },
            {
              "name": "GeoType",
              "value": "Primary"
            }
          ],
          "operator": "GreaterThan",
          "threshold": "0",
          "timeAggregation": "PT5M",
          "metricValue": 1.0
        },
      ]
    },
    "subscriptionId": "00000000-0000-0000-0000-000000000000",
    "resourceGroupName": "Contoso",
    "resourceName": "diag500",
    "resourceType": "Microsoft.Storage/storageAccounts",
    "resourceId": "/subscriptions/1e3ff1c0-771a-4119-a03b-be82a51e232d/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500",
    "portalLink": "https://portal.azure.com/#resource//subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Contoso/providers/Microsoft.Storage/storageAccounts/diag500"
  },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
    }
}
```

###Standard Log Analytics 
```
{
     "WorkspaceId":"{Guid}","
     "AlertRuleName":"{String}",
     "SearchQuery":"{String}",
     "AlertThresholdOperator":"{Enum}",
     "AlertThresholdValue":"{Integer}",
     "SearchIntervalStartTimeUtc":"{DateTime}",
     "SearchIntervalEndtimeUtc":"{DateTime}",
     "ResultCount":"{String}",
     "SearchIntervalInSeconds":"{Integer}",
     "LinkToResults":"{URL}",
     "Description":"{String}"
}
```
###ESS Custom
```
{
    "AlertRuleName": "{String}​",
    "Category": "{String}",
    "Description": "{String}​",
    "Entities": "{String}",
    "Environment": "{String}",
    "Instance": "{String}",
    "Resources": "{String}​",
    "Scenarios": "{String}",
    "SearchIntervalEndtimeUtc": "{DateTime}​",
    "SearchIntervalStartTimeUtc": "{DateTime}​",
    "Severity": "{Int}",
    "Source": "{String}"
}
```
**Values**

|Name | Type | Mandatory | Fixed Set of Values | Description |
|---|---|---|---|---|
|AlertRuleName| String | Yes | | Name of the alert |
|Category|String|Yes||Typically values such as 'availability', 'security', etc.
|Description | String | Yes | | The description of the alert for the support team to read. Either more detailed explanation or link to KB |
| Entities |	String | No || Entity that initiated the action that led to the alert. |
| Environment | String | Yes | STAG / PROD / DEV |	 The environment where the monitoring platform is deployed. |
| Instance | String | No | EMEA / US or 00 / 01 | The monitoring platform instance. (Default is single instance)|
| Resources | String | No	|| Impacted (Azure) resources; VM name, SQL Server, etc. for availability alerts. Impacted groups or users for security alerts. |
| Scenarios | String | No || Impacted business scenario (if known) |
| SearchIntervalEndtimeUtc | DateTime | Yes | |		
| SearchIntervalStartTimeUtc | DateTime | No	| |	
| Severity | Integer | Yes | |The alert severity. Set by the person creating the alert and should be an integer.	 |	
| Source | String | Yes | ApplicationInsights or LogAnalytics| The source of the data store that was queried for the alert
