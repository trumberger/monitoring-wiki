
## Supported JSON Schema's
The following schema's are supported by ESS monitoring interface. 

###Azure Activity Log Alert
https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook#payload-schema

```
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}

```

###Azure Log Alert
https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-alerts-unified-log-webhook#sample-payloads

```
{
    "WorkspaceId":"12345a-1234b-123c-123d-12345678e",
    "AlertRuleName":"AcmeRule","SearchQuery":"search *",
    "SearchResult":
        {
        "tables":[
                    {"name":"PrimaryResult","columns":
                        [
                        {"name":"$table","type":"string"},
                        {"name":"Id","type":"string"},
                        {"name":"TimeGenerated","type":"datetime"}
                        ],
                    "rows":
                        [
                            ["Fabrikam","33446677a","2018-02-02T15:03:12.18Z"],
                            ["Contoso","33445566b","2018-02-02T15:16:53.932Z"]
                        ]
                    }
                ]
        },
    "SearchIntervalStartTimeUtc": "2018-03-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2018-03-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 2,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://workspaceID.portal.mms.microsoft.com/#Workspace/search/index?_timeInterval.intervalEnd=2018-03-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Warning"
 }

```

Example:

```
Request body: {"schemaId":"Microsoft.Insights/LogAlert","data":{
  "SubscriptionId": "c8cd80a0-4450-4b56-9245-2842d6f6357a",
  "AlertRuleName": "stag log alert test",
  "SearchQuery": "requests",
  "SearchResult": {
    "tables": [
      {
        "name": "PrimaryResult",
        "columns": [
          {
            "name": "timestamp",
            "type": "datetime"
          },
          {
            "name": "id",
            "type": "string"
          },
          {
            "name": "source",
            "type": "string"
          },
          {
            "name": "name",
            "type": "string"
          },
          {
            "name": "url",
            "type": "string"
          },
          {
            "name": "success",
            "type": "string"
          },
          {
            "name": "resultCode",
            "type": "string"
          },
          {
            "name": "duration",
            "type": "real"
          },
          {
            "name": "performanceBucket",
            "type": "string"
          },
          {
            "name": "itemType",
            "type": "string"
          },
          {
            "name": "customDimensions",
            "type": "dynamic"
          },
          {
            "name": "customMeasurements",
            "type": "dynamic"
          },
          {
            "name": "operation_Name",
            "type": "string"
          },
          {
            "name": "operation_Id",
            "type": "string"
          },
          {
            "name": "operation_ParentId",
            "type": "string"
          },
          {
            "name": "operation_SyntheticSource",
            "type": "string"
          },
          {
            "name": "session_Id",
            "type": "string"
          },
          {
            "name": "user_Id",
            "type": "string"
          },
          {
            "name": "user_AuthenticatedId",
            "type": "string"
          },
          {
            "name": "user_AccountId",
            "type": "string"
          },
          {
            "name": "application_Version",
            "type": "string"
          },
          {
            "name": "client_Type",
            "type": "string"
          },
          {
            "name": "client_Model",
            "type": "string"
          },
          {
            "name": "client_OS",
            "type": "string"
          },
          {
            "name": "client_IP",
            "type": "string"
          },
          {
            "name": "client_City",
            "type": "string"
          },
          {
            "name": "client_StateOrProvince",
            "type": "string"
          },
          {
            "name": "client_CountryOrRegion",
            "type": "string"
          },
          {
            "name": "client_Browser",
            "type": "string"
          },
          {
            "name": "cloud_RoleName",
            "type": "string"
          },
          {
            "name": "cloud_RoleInstance",
            "type": "string"
          },
          {
            "name": "appId",
            "type": "string"
          },
          {
            "name": "appName",
            "type": "string"
          },
          {
            "name": "iKey",
            "type": "string"
          },
          {
            "name": "sdkVersion",
            "type": "string"
          },
          {
            "name": "itemId",
            "type": "string"
          },
          {
            "name": "itemCount",
            "type": "int"
          }
        ],
        "rows": [
          [
            "2018-07-11T19:05:00.019Z",
            "1dc85814-a608-4049-9aec-0468a6cd11ce",
            "",
            "HostValidation",
            "",
            "False",
            "0",
            9.8013,
            "<250ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:05:00.0199909+00:00\",\"Succeeded\":\"False\",\"FullName\":\"HostValidation\",\"EndTime\":\"2018-07-11T19:05:00.0190000Z\"}",
            null,
            "HostValidation",
            "1dc85814-a608-4049-9aec-0468a6cd11ce",
            "1dc85814-a608-4049-9aec-0468a6cd11ce",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "60f02416-853d-11e8-911d-01103fe4f6d1",
            1
          ],
          [
            "2018-07-11T19:10:00.019Z",
            "847df215-187e-4b13-83ee-156aee258f9f",
            "",
            "HostValidation",
            "",
            "False",
            "0",
            3.7814,
            "<250ms",
            "request",
            "{\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:10:00.0192442+00:00\",\"Succeeded\":\"False\",\"FullName\":\"HostValidation\",\"EndTime\":\"2018-07-11T19:10:00.0190000Z\"}",
            null,
            "HostValidation",
            "847df215-187e-4b13-83ee-156aee258f9f",
            "847df215-187e-4b13-83ee-156aee258f9f",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "13c0d036-853e-11e8-8fee-21b2ce67ad7d",
            1
          ],
          [
            "2018-07-11T19:06:00.02Z",
            "4fee114e-8406-43d4-a248-820b7fb898d1",
            "",
            "BatchAlertFramework",
            "",
            "False",
            "0",
            372.4059,
            "250ms-500ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:06:00.0207520+00:00\",\"Succeeded\":\"False\",\"FullName\":\"BatchAlertFramework\",\"EndTime\":\"2018-07-11T19:06:00.3840000Z\"}",
            null,
            "BatchAlertFramework",
            "4fee114e-8406-43d4-a248-820b7fb898d1",
            "4fee114e-8406-43d4-a248-820b7fb898d1",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "84b3430b-853d-11e8-911d-01103fe4f6d1",
            1
          ],
          [
            "2018-07-11T19:09:00.023Z",
            "8c13f3a6-5d5a-4829-82d1-e5b9028d07e5",
            "",
            "BatchAlertFramework",
            "",
            "False",
            "0",
            363.7775,
            "250ms-500ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:09:00.0235190+00:00\",\"Succeeded\":\"False\",\"FullName\":\"BatchAlertFramework\",\"EndTime\":\"2018-07-11T19:09:00.3810000Z\"}",
            null,
            "BatchAlertFramework",
            "8c13f3a6-5d5a-4829-82d1-e5b9028d07e5",
            "8c13f3a6-5d5a-4829-82d1-e5b9028d07e5",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "effffb3b-853d-11e8-acfb-35a459ea5619",
            1
          ],
          [
            "2018-07-11T19:00:00.014Z",
            "be6634d0-c3f6-43c8-83b9-6a9a9c6fcd06",
            "",
            "HostValidation",
            "",
            "False",
            "0",
            11.0773,
            "<250ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:00:00.0148025+00:00\",\"Succeeded\":\"False\",\"FullName\":\"HostValidation\",\"EndTime\":\"2018-07-11T19:00:00.0140000Z\"}",
            null,
            "HostValidation",
            "be6634d0-c3f6-43c8-83b9-6a9a9c6fcd06",
            "be6634d0-c3f6-43c8-83b9-6a9a9c6fcd06",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "ae221005-853c-11e8-911d-01103fe4f6d1",
            1
          ],
          [
            "2018-07-11T19:00:00.046Z",
            "1b28d7be-a23c-46c1-b5c9-c1b7110c63f0",
            "",
            "BatchAlertFramework",
            "",
            "False",
            "0",
            348.0692,
            "250ms-500ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:00:00.0460016+00:00\",\"Succeeded\":\"False\",\"FullName\":\"BatchAlertFramework\",\"EndTime\":\"2018-07-11T19:00:00.3740000Z\"}",
            null,
            "BatchAlertFramework",
            "1b28d7be-a23c-46c1-b5c9-c1b7110c63f0",
            "1b28d7be-a23c-46c1-b5c9-c1b7110c63f0",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "ae221006-853c-11e8-911d-01103fe4f6d1",
            1
          ],
          [
            "2018-07-11T18:57:00.011Z",
            "4da9f8fa-9245-48bd-b719-e238fcae1a64",
            "",
            "BatchAlertFramework",
            "",
            "False",
            "0",
            382.4126,
            "250ms-500ms",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T18:57:00.0118064+00:00\",\"Succeeded\":\"False\",\"FullName\":\"BatchAlertFramework\",\"EndTime\":\"2018-07-11T18:57:00.3830000Z\"}",
            null,
            "BatchAlertFramework",
            "4da9f8fa-9245-48bd-b719-e238fcae1a64",
            "4da9f8fa-9245-48bd-b719-e238fcae1a64",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "42d816fb-853c-11e8-acfb-35a459ea5619",
            1
          ],
          [
            "2018-07-11T19:03:00.017Z",
            "3f2d61ae-3125-445c-abf4-a88e493f974b",
            "",
            "BatchAlertFramework",
            "",
            "False",
            "0",
            648.5111,
            "500ms-1sec",
            "request",
            "{\"LogLevel\":\"Error\",\"Category\":\"Host.Results\",\"{OriginalFormat}\":\"Executed '{FullName}' (Failed, Id={InvocationId})\",\"TriggerReason\":\"Timer fired at 2018-07-11T19:03:00.0179401+00:00\",\"Succeeded\":\"False\",\"FullName\":\"BatchAlertFramework\",\"EndTime\":\"2018-07-11T19:03:00.6520000Z\"}",
            null,
            "BatchAlertFramework",
            "3f2d61ae-3125-445c-abf4-a88e493f974b",
            "3f2d61ae-3125-445c-abf4-a88e493f974b",
            "",
            "",
            "",
            "",
            "",
            "",
            "PC",
            "",
            "",
            "0.0.0.0",
            "",
            "",
            "",
            "",
            "fun-stag-env-bpl-mon",
            "ad35009864d962717bf36085962320f36397c7fc102f89b938d447307ad4151d",
            "e0fbfdfa-545e-4089-8464-113762a9d7de",
            "AIS-STAG-BPL-MON",
            "93aee2ff-e554-43ad-8815-d5aea9c78e64",
            "azurefunctions: 1.0.11820.0",
            "196c302b-853d-11e8-8fee-21b2ce67ad7d",
            1
          ]
        ]
      }
    ]
  },
  "SearchIntervalStartTimeUtc": "2018-07-11T18:56:24",
  "SearchIntervalEndtimeUtc": "2018-07-11T19:11:24",
  "AlertThresholdOperator": "Less Than",
  "AlertThresholdValue": 9999,
  "ResultCount": 8,
  "SearchIntervalInSeconds": 900,
  "LinkToSearchResults": "https://analytics.applicationinsights.io/subscriptions/c8cd80a0-4450-4b56-9245-2842d6f6357a/resourceGroups/STAG-MonitoringAgent/components/AIS-STAG-BPL-MON?query=requests&prettify=1&timespan=2018-07-11T18:56:24.0000000Z/2018-07-11T19:11:24.0000000Z",
  "Description": "STAG Log Alert Test",
  "Severity": "High",
  "ApplicationId": "e0fbfdfa-545e-4089-8464-113762a9d7de"
}}

```

###Azure Application Insights Log Alert
https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitor-alerts-unified-log-webhook#log-alert-for-azure-application-insights

```
{
    "schemaId":"Microsoft.Insights/LogAlert","data":
    { 
    "SubscriptionId":"12345a-1234b-123c-123d-12345678e",
    "AlertRuleName":"AcmeRule","SearchQuery":"search *",
    "SearchResult":
        {
        "tables":[
                    {"name":"PrimaryResult","columns":
                        [
                        {"name":"$table","type":"string"},
                        {"name":"Id","type":"string"},
                        {"name":"TimeGenerated","type":"datetime"}
                        ],
                    "rows":
                        [
                            ["Fabrikam","33446677a","2018-02-02T15:03:12.18Z"],
                            ["Contoso","33445566b","2018-02-02T15:16:53.932Z"]
                        ]
                    }
                ]
        },
    "SearchIntervalStartTimeUtc": "2018-03-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2018-03-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 2,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://analytics.applicationinsights.io/subscriptions/12345a-1234b-123c-123d-12345678e/?query=search+*+&timeInterval.intervalEnd=2018-03-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Error",
    "ApplicationId": "123123f0-01d3-12ab-123f-abc1ab01c0a1"
    }
}
```

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
