
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


2) NEW Metric Alert rule
a) ARM template file

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "This is a metric alert",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "alertSeverity": {
            "type": "int",
            "defaultValue": 3,
            "allowedValues": [
                0,
                1,
                2,
                3,
                4
            ],
            "metadata": {
                "description": "Severity of alert {0,1,2,3,4}"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether the alert is enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Full Resource ID of the resource emitting the metric that will be used for the comparison. For example /subscriptions/00000000-0000-0000-0000-0000-00000000/resourceGroups/ResourceGroupName/providers/Microsoft.compute/virtualMachines/VM_xyz"
            }
        },
        "metricName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric used in the comparison to activate the alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterThan",
            "allowedValues": [
                "Equals",
                "NotEquals",
                "GreaterThan",
                "GreaterThanOrEqual",
                "LessThan",
                "LessThanOrEqual"
            ],
            "metadata": {
                "description": "Operator comparing the current value with the threshold value."
            }
        },
        "threshold": {
            "type": "string",
            "defaultValue": "0",
            "metadata": {
                "description": "The threshold value at which the alert is activated."
            }
        },
        "timeAggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Minimum",
                "Maximum",
                "Total"
            ],
            "metadata": {
                "description": "How the data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "evaluationFrequency": {
            "type": "string",
            "defaultValue": "PT1M",
            "metadata": {
                "description": "how often the metric alert is evaluated represented in ISO 8601 duration format"
            }
        },
        "actionGroupId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The ID of the action group that is triggered when the alert is activated or deactivated"
            }
        }
    },
    "variables": {  },
    "resources": [
        {
            "name": "[parameters('alertName')]",
            "type": "Microsoft.Insights/metricAlerts",
            "location": "global",
            "apiVersion": "2018-03-01",
            "tags": {},
            "properties": {
                "description": "[parameters('alertDescription')]",
                "severity": "[parameters('alertSeverity')]",
                "enabled": "[parameters('isEnabled')]",
                "scopes": ["[parameters('resourceId')]"],
                "evaluationFrequency":"[parameters('evaluationFrequency')]",
                "windowSize": "[parameters('windowSize')]",
                "criteria": {
                    "odata.type": "Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria",
                    "allOf": [
                        {
                            "name" : "1st criterion",
                            "metricName": "[parameters('metricName')]",
                            "dimensions":[],   
                            "operator": "[parameters('operator')]",
                            "threshold" : "[parameters('threshold')]",
                            "timeAggregation": "[parameters('timeAggregation')]"
                        }
                    ]
                },
                "actions": [
                    {
                        "actionGroupId": "[parameters('actionGroupId')]"                
                    }
                ]
            }
        }
    ]
}
```

b) ARM template parameter file

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "value": "New Metric Alert"
        },
        "alertDescription": {
            "value": "New metric alert created via template"
        },
        "alertSeverity": {
            "value":3
        },
        "isEnabled": {
            "value": true
        },
        "resourceId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/replace-with-resourceGroup-name/providers/Microsoft.Compute/virtualMachines/replace-with-resource-name"
        },
        "metricName": {
            "value": "Percentage CPU"
        },
        "operator": {
          "value": "GreaterThan"
        },
        "threshold": {
            "value": "80"
        },
        "timeAggregation": {
            "value": "Average"
        },
        "actionGroupId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/resource-group-name/providers/Microsoft.Insights/actionGroups/replace-with-action-group"
        }
    }
}
```

c) Output

