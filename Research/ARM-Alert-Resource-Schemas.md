## Overview
This article describes the different alert schema that ARM uses to configure alerts in Azure. Following types are currently supported:

- Metric Alerts. 
- Diagnostics and Activity Alerts
- Scheduled Query Rule Alerts (Application Insights only)

## Alert Types

### Metric Alerts

The following API can be used to retrieve all metric alerts within a resource group:
```
GET
https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/metricAlerts?api-version=2018-03-01
```

The following schema is used for metric alerts
```
        {
            "location": "global",
            "type": "Microsoft.Insights/metricAlerts",
            "name": "Test Availability Storage Queue",
            "id": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/Nielsn-DEV-BusinessLogic/providers/microsoft.insights/metricAlerts/Test%20Availability%20Storage%20Queue",
            "tags": {},
            "properties": {
                "description": "test",
                "severity": 3,
                "enabled": true,
                "scopes": [
                    "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/Nielsn-DEV-BusinessLogic/providers/Microsoft.Storage/storageAccounts/stadevtuavgpehxx7ia"
                ],
                "evaluationFrequency": "PT5M",
                "windowSize": "PT5M",
                "templateType": 8,
                "templateSpecificParameters": {},
                "criteria": {
                    "allOf": [
                        {
                            "name": "Metric1",
                            "metricName": "Availability",
                            "dimensions": [],
                            "operator": "LessThan",
                            "threshold": 50,
                            "timeAggregation": "Average",
                            "monitorTemplateType": 8
                        }
                    ],
                    "odata.type": "Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria"
                },
                "actions": [
                    {
                        "actionGroupId": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourcegroups/default-activitylogalerts/providers/microsoft.insights/actiongroups/email%20action%20group",
                        "webHookProperties": {}
                    }
                ]
            }
        }
```


Diagnostics and Activity Alerts

GET
https://resources.azure.com/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/Nielsn-DEV-CustomerIntegration/providers/microsoft.insights/activityLogAlerts

{
  "id": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/Nielsn-DEV-CustomerIntegration/providers/microsoft.insights/activityLogAlerts/Diagnostics test",
  "type": "Microsoft.Insights/ActivityLogAlerts",
  "name": "Diagnostics test",
  "location": "Global",
  "kind": null,
  "tags": {},
  "properties": {
    "scopes": [
      "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7"
    ],
    "condition": {
      "allOf": [
        {
          "field": "category",
          "equals": "Autoscale",
          "containsAny": null
        },
        {
          "field": "resourceId",
          "equals": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/Nielsn-DEV-CustomerIntegration/providers/Microsoft.KeyVault/vaults/KVL-DEV-CustInt-BPL-MON",
          "containsAny": null
        },
        {
          "field": "operationName",
          "equals": "Microsoft.KeyVault/vaults/delete",
          "containsAny": null
        }
      ]
    },
    "actions": {
      "actionGroups": [
        {
          "actionGroupId": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourcegroups/default-activitylogalerts/providers/microsoft.insights/actiongroups/email%20action%20group",
          "webhookProperties": {}
        }
      ]
    },
    "enabled": true,
    "description": "ertert"
  },
  "identity": null
}

Scheduled Query Rules
GET https://management.azure.com/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/BusinessLogic-PROD/providers/microsoft.insights/scheduledqueryrules?api-version=2017-09-01-preview

{
    "value": [
        {
            "id": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/BusinessLogic-PROD/providers/microsoft.insights/scheduledqueryrules/Exceptions in Environment",
            "name": "Exceptions in Environment",
            "type": "microsoft.insights/scheduledqueryrules",
            "location": "eastus",
            "tags": {
                "hidden-link:/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/BusinessLogic-PROD/providers/microsoft.insights/components/AIS-PROD-NativeMonitoring": "Resource"
            },
            "kind": null,
            "etag": "\"7c00eee6-0000-0000-0000-5abc29aa0000\"",
            "properties": {
                "description": "Test Alert",
                "enabled": "true",
                "skuType": "L3",
                "lastUpdatedTime": "2018-03-28T23:47:54.0842964Z",
                "ProvisioningState": "Succeeded",
                "source": {
                    "query": "exceptions\n| where timestamp < ago(2d)",
                    "authorizedResources": null,
                    "resourceId": null,
                    "dataSourceId": "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourceGroups/BusinessLogic-PROD/providers/microsoft.insights/components/AIS-PROD-NativeMonitoring",
                    "queryType": "ResultCount"
                },
                "metricName": null,
                "schedule": {
                    "frequencyInMinutes": 60,
                    "timeWindowInMinutes": 360
                },
                "action": {
                    "lastFiredTime": null,
                    "severity": "3",
                    "status": "Active",
                    "aznsAction": {
                        "actionGroup": [
                            "/subscriptions/16b26395-68e3-45e2-81c1-54729c26aba8/resourcegroups/default-activitylogalerts/providers/microsoft.insights/actiongroups/prod%20mail"
                        ],
                        "emailSubject": null,
                        "customWebhookPayload": null
                    },
                    "actionGroup": null,
                    "alertStateManagement": null,
                    "throttlingInMin": null,
                    "trigger": {
                        "thresholdOperator": "GreaterThan",
                        "threshold": 0,
                        "consecutiveBreach": 1,
                        "metricTrigger": null
                    },
                    "odata.type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.Microsoft.AppInsights.Nexus.DataContracts.Resources.ScheduledQueryRules.AlertingAction"
                }
            }
        }
    ],
    "nextLink": null
}

