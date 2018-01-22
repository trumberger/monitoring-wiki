
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
