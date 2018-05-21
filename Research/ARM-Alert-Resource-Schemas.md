## Overview

This article describes the different alert schema that ARM uses to configure alerts in Azure. Following types are currently supported:

- Metric Alerts
- Diagnostics and Activity Alerts
- Scheduled Query Rule Alerts (Application Insights only)

## Alert Types

### Metric Alerts

The following API call can be used to retrieve all metric alerts within a resource group:

```
GET
https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/metricAlerts?api-version=2018-03-01
```

The following schema is used for metric alerts

```
{
    "location": "global",
    "type": "Microsoft.Insights/metricAlerts",
    "name": "ENTER NAME OF THE ALERT",
    "tags": {},
    "properties": {
        "description": "ENTER DESCRIPTION OF THE ALERTS",
        "severity": 3, # allowed values are 0-4
        "enabled": true,
        "scopes": [
            "ENTER AZURE RESOURCE ID"
        ],
        "evaluationFrequency": "PT5M",
        "windowSize": "PT5M",
        "templateType": 8,
        "templateSpecificParameters": {},
        "criteria": {
            "allOf": [
                {
                    "name": "Metric1",
                    "metricName": "METRIC NAME",
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
                "actionGroupId": "ACTION GROUP ID",
                "webHookProperties": {}
            }
        ]
    }
}
```

### Diagnostics and Activity Alerts

The following API call can be used to retrieve all diagnotics and activity alerts within a resource group:

```
GET
https://resources.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/activityLogAlerts
```

The following schema is used for activity and diagnostics alerts

```
{
  "type": "Microsoft.Insights/ActivityLogAlerts",
  "name": "ENTER NAME ALERT",
  "location": "Global",
  "kind": null,
  "tags": {},
  "properties": {
    "scopes": [
      "/subscriptions/SUBSCRIPTIONID",
      "AZURE RESOURCE ID"
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
          "equals": "AZURE RESOURCE ID",
          "containsAny": null
        },
        {
          "field": "operationName",
          "equals": "Microsoft.KeyVault/vaults/delete", # Example of action
          "containsAny": null
        }
      ]
    },
    "actions": {
      "actionGroups": [
        {
          "actionGroupId": "ACTION GROUP ID",
          "webhookProperties": {}
        }
      ]
    },
    "enabled": true,
    "description": "ENTER DESCRIPTION OF ALERT"
  },
  "identity": null
}
```

### Scheduled Query Rules
The following API call can be used to retrieve all scheduled (custom) query alerts within a resource group:

```
GET https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/scheduledqueryrules?api-version=2017-09-01-preview
```

The following schema is used for scheduled query alerts

```
{
    "name": "ENTER NAME ALERT",
    "type": "microsoft.insights/scheduledqueryrules",
    "location": "eastus",
    "tags": { },
    "properties": {
        "description": "ENTER DESCRIPTION ALERT",
        "enabled": "true",
        "skuType": "L3",
        "source": {
            "query": "ENTER KUSTO QUERY HERE",
            "authorizedResources": null,
            "resourceId": null,
            "dataSourceId": "AZURE RESOURCE ID OF DATA SOURCE",
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
                    "ACTION GROUP ID"
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
```