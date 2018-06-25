This research was done in regards with [US755 [Research] Extend customer template with Health Service Alerts using new Azure alerting framework](https://easplatform.visualstudio.com/Monitoring/_backlogs/taskboard/Sprint%201806-1?_a=requirements)

Q: Can the health Alerts be templatized in ARM?

A: Yes, actually the type of alert rule is Microsoft.Insights/ActivityLogAlerts. Please see below:

  
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

Note: A Service Health Alert deployed from ARM template is visible ONLY from GUI and is not returned when using resources.azure.com or doing https queries:

 ![image.png](/.attachments/image-69f4a332-0a47-4cd8-887f-69274c0b1b2b.png)
______________________________________________________________________________________________________________________________________________________________________________

Q: The Service Health alerts have three event types (Service Issue / Planned Maintenance / Health Advisories). What do those types mean and are there any policies?

A: 
Service Health tracks three types of health events that may impact your resources:

**Service issues** - Problems in the Azure services that affect you right now. 
**Planned maintenance** - Upcoming maintenance that can affect the availability of your services in the future. 
**Health advisories** - Changes in Azure services that require your attention. Examples include when Azure features are deprecated or if you exceed a usage quota.

If you select at Event Type the following values, you will have the following ARM template:

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
______________________________________________________________________________________________________________________________________________________________________________

Q: The Health History allows you to list the history of all event for the different types. Is there an API / source to query this history programmatically?

A:

Documentation:
[Service Health](https://docs.microsoft.com/en-us/azure/service-health/service-health-overview)
[Resource types and health checks in Azure resource health](https://docs.microsoft.com/en-us/azure/service-health/resource-health-checks-resource-types)
[Availability Statuses](https://docs.microsoft.com/en-us/rest/api/resourcehealth/availabilitystatuses/list)