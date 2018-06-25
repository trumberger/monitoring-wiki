The following where found in my research:

A valid ARM template:

  
```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
      }
    }
  },
"resources": [ 
  {
    "type": "Microsoft.Insights/ActivityLogAlerts",
    "name": "ServiceHealthAlert_ARM",
    "apiVersion": "2017-04-01",
    "location": "Global",
    "kind": null,
    "tags": {},
    "properties": {
      "scopes": [
        "[concat('/subscriptions/', subscription().subscriptionId)]"
      ],
      "condition": {
        "allOf": [
          {
            "field": "category",
            "equals": "ServiceHealth",
            "containsAny": null
          },
          {
            "anyOf": [
              {
                "field": "properties.incidentType",
                "equals": "value",
                "containsAny": null
              }
            ]
          },
          {
            "field": "properties.impactedServices[*].ServiceName",
            "equals": null,
            "containsAny": [
              "Azure DNS",
              "Container Instances",
              "Data Catalog",
              "Data Factory"
            ]
          },
          {
            "field": "properties.impactedServices[*].ImpactedRegions[*].RegionName",
            "equals": null,
            "containsAny": [
              "East US",
              "East US 2",
              "West US"
            ]
          }
        ]
      },
      "actions": {
        "actionGroups": [
          {
            "actionGroupId": "[parameters('actionGroupId')]",
            "webhookProperties": {}
          }
        ]
      },
      "enabled": true,
      "description": "ServiceHealthAlert_ARM"
    },
    "identity": null
  }
]
}
```

If you select at Event Type the following values

**Service Issue**


```
[
              {
                "field": "properties.incidentType",
                "equals": "Incident",
                "containsAny": null
              }
]
```


**Planned maintenance**


```
[
              {
                "field": "properties.incidentType",
                "equals": "Maintenance",
                "containsAny": null
              }
]
```


**Health Advisories**


```
[
              {
                "field": "properties.incidentType",
                "equals": "Informational",
                "containsAny": null
              },
              {
                "field": "properties.incidentType",
                "equals": "ActionRequired",
                "containsAny": null
              }
]
```


