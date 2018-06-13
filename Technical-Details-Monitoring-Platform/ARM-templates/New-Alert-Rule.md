
1. NEW Alert rule
a) ARM template file

```

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "Description": "Name of Log Analytics workspace"
      }
    },
    "workspaceregionId": {
      "type": "string",
      "metadata": {
        "Description": "Region of Log Analytics workspace"
      }
    },
    "actiongroup": {
      "type": "string",
      "metadata": {
        "Description": "List of action groups for alert actions separated by semicolon"
      }
    }
  },
  "resources": [
    {
      "name": "[concat('ESSMonitoringSolution', '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "2015-11-01-preview",
      "dependsOn": [
        "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), 'VirtualMachineisunavailable')]",
        "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), 'VirtualMachineisunavailable', 'myschedule-VirtualMachineisunavailable')]",
        "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), 'VirtualMachineisunavailable', 'myschedule-VirtualMachineisunavailable', 'myalert-VirtualMachineisunavailable')]"
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
        ],
        "containedResources": [
          "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), 'VirtualMachineisunavailable')]",
          "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), 'VirtualMachineisunavailable', 'myschedule-VirtualMachineisunavailable')]",
          "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), 'VirtualMachineisunavailable', 'myschedule-VirtualMachineisunavailable', 'myalert-VirtualMachineisunavailable')]"
        ]
      },
      "plan": {
        "name": "[concat('ESSMonitoringSolution', '[' ,parameters('workspaceName'), ']')]",
        "Version": "1.0",
        "product": "ESSMonitoringSolution",
        "publisher": "ESS",
        "promotionCode": ""
      }
    },
    {
      "name": "[concat(parameters('workspaceName'), '/', 'VirtualMachineisunavailable')]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
      "apiVersion": "2017-04-26-preview",
      "dependsOn": [ ],
      "tags": { },
      "properties": {
        "etag": "*",
        "query": "Heartbeat| summarize Beats = count() by Computer | where Beats < 5",
        "displayName": "Virtual Machine is unavailable",
        "category": "Samples"
      }
    },
    {
      "name": "[concat(parameters('workspaceName'), '/', 'VirtualMachineisunavailable', '/', 'myschedule-VirtualMachineisunavailable')]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
      "apiVersion": "2017-04-26-preview",
      "dependsOn": [
        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', 'VirtualMachineisunavailable')]"
      ],
      "properties": {
        "etag": "*",
        "interval": "15",
        "queryTimeSpan": "60",
        "enabled": true
      }
    },
    {
      "name": "[concat(parameters('workspaceName'), '/', 'VirtualMachineisunavailable', '/',  'myschedule-VirtualMachineisunavailable', '/',  'myalert-VirtualMachineisunavailable')]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
      "apiVersion": "2017-04-26-preview",
      "dependsOn": [
        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  'VirtualMachineisunavailable', '/schedules/', 'myschedule-VirtualMachineisunavailable')]"
      ],
      "properties": {
        "etag": "*",
        "Type": "Alert",
        "Name": "Virtual Machine is unavailable",
        "Description": "Check heartbeat signal send out by local agent",
        "Severity": "critical",
        "Threshold": {
          "Operator": "gt",
          "Value": "3",
          "MetricsTrigger": {
            "TriggerCondition": "Consecutive",
            "Operator": "gt",
            "Value": "3"
          }
        },
        "AzNsNotification": {
          "GroupIds": [
            "[parameters('actiongroup')]"            
          ],
          "CustomEmailSubject": "Virtual Machine is unavailable"
        }             
      }
    }
  ]
}
```

b) ARM template parameter file

```
{
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "OLA-DEV-DataStore-BP-BPL-MON"
            },
            "workspaceregionId": {
                "value": "eastus"
            },
            "actiongroup": {
                "value": "/subscriptions/632cc760-aa97-46a9-9c12-50b13163c9c7/resourceGroups/BP-DEV-MonitoringAgent/providers/microsoft.insights/actionGroups/BogdanActionGroup"
            }
        }
    }
```

c) Output

to be generated
