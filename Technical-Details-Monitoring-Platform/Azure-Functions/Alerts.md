
# Supported JSON Schema's

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
    "Description": "{String}​",
    "Entities": "{String}",
    "Environment": "{String}",
    "Instance": "{String}",
    "Resources": "{String}​",
    "Scenarios": "{String}",
    "SearchIntervalEndtimeUtc": "{DateTime}​",
    "SearchIntervalStartTimeUtc": "{DateTime}​"
}
```
**Values**

|Name | Type | Mandatory | Fixed Set of Values | Description |
|---|---|---|---|---|
|AlertRuleName| String | Yes | | Name of the alert |
|Description | String | Yes | | The description of the alert for the support team to read. Either more detailed explanation or link to KB |
| Entities |	String | No || Entity that initiated the action that led to the alert. |
| Environment | String | Yes | STAG / PROD / DEV |	 The environment where the monitoring platform is deployed. |
| Instance | String | No | EMEA / US or 00 / 01 | The monitoring platform instance. (Default is single instance)|
| Resources | String | No	|| Impacted (Azure) resources; VM name, SQL Server, etc. for availability alerts. Impacted groups or users for security alerts.  |
| Scenarios | String | No || Impacted business scenario (if known) | 
| SearchIntervalEndtimeUtc | DateTime | Yes |||		
| SearchIntervalStartTimeUtc | DateTime | No	|||	
