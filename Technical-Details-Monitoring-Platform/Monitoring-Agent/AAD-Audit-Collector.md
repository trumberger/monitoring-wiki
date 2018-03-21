# Technical Overview

## Flow

The source of the picture below can be found [here](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationTeam/Shared%20Documents/General/BPL%20-%20Reference%20Architecture%20Monitoring%20and%20Automation.vsdx)

![image.png](.attachments/image-f4597f7d-9772-452e-8fb5-4fd0e824ab91.png)

## Schema

### AAD Audit Logs

The following schema is used for log **AADAuditLogs_CL**

```
[
  {
    "TenantId": "{GUID}",
    "SourceSystem": "{string}",
    "TimeGenerated [UTC]": "{DateTime}",
    "Activity_s": "{string}",
    "ActorType_s": "{string}",
    "ActorName_s": "{string}",
    "SourceType_s": "{string}",
    "SourceName_s": "{string}",
    "TargetType_s": "{string}",
    "TargetName_s": "{string}",
    "ActivityDate_t [UTC]": "{DateTime}",
    "Type": "AADAuditLogs_CL"
  }
]
```

### AAD Sign-in Logs

The following schema is used for log **AadSignInLogs_CL**

```
[
  {
    "TenantId": "{GUID}",
    "SourceSystem": "{string}",
    "TimeGenerated [UTC]": "{string}",
    "UserPrincipleName_s": "{string}",
    "AppName_s": "{string}",
    "IPAddress": "{string}",
    "LoginStatus_s": "{string}",
    "FailureReason_s": "{string}",
    "Country_s": "{string}",
    "SigninDateTime_t [UTC]": "{DateTime}",
    "Type": "AadSignInLogs_CL"
  }
]
```