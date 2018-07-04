## Overview

This article describes the different alert schema that ARM uses to configure alerts in Azure. Following types are currently supported:

- Metric Alerts
- Diagnostics and Activity Alerts
- Scheduled Query Rule Alerts 

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
These alert rules are mainly queries against Log Analytics and Application Insights. 
The alert rule itself has three components:

a) Microsoft.OperationalInsights/workspaces/savedSearches

API call to get all savedSearches within a resource group:

`GET https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceID}/savedSearches?api-version=2015-03-20`

b) Microsoft.OperationalInsights/workspaces/savedSearches/schedules

API call to get the schedules for a saved search:

`GET https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceID}/savedSearches/{savedSearchID}/schedules?api-version=2015-03-20`

c) Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions

API call to get the actions performed for a schedule within a saved search.

`GET https://management.azure.com/subscriptions/{subscriptionID}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceID}/savedSearches/{savedSearchID}/schedules/{schedulesID}/actions?api-version=2015-03-20`

Microsoft.OperationalInsights/workspaces/savedSearches template reference

```
{
  "name": "string",
  "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
  "apiVersion": "2015-03-20",
  "properties": {
    "Category": "string",
    "DisplayName": "string",
    "Query": "string",
    "Version": "integer",
    "Tags": [
      {
        "Name": "string",
        "Value": "string"
      }
    ]
  }
}
```

Microsoft.OperationalInsights/workspaces/savedSearches/shedules template reference

```
{
    "name": "string",
    "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
    "apiVersion": "2015-03-20",
    "dependsOn": [
        "string"
    ],
    "properties": {
        "etag": "*",
        "Interval": "integer",
        "QueryTimeSpan": "integer",
        "Enabled": true
    }
}
```
Microsoft.OperationalInsights/workspaces/savedSearches/shedules/actions template reference


```
{
    "name": "string",
    "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
    "apiVersion": "2015-03-20",
    "dependsOn": [
        "string"
    ],
    "properties": {
        "etag": "*",
        "Type": "Alert",
        "Name": "string",
        "Description": "string",
        "Severity": "string",
        "Threshold": {
            "Operator": "string",
            "Value": "integer",
            "MetricsTrigger": {
                "string",
                "Operator": "string",
                "Value": "integer"
            }
        },
        "Throttling": {
            "DurationInMinutes": integer
        },
        "EmailNotification": {
            "Recipients": [
                "string"
            ],
            "Subject": "string"
        }
    }
}
```
