# Technical Overview

## Flow

The source of the picture below can be found [here](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationTeam/Shared%20Documents/General/BPL%20-%20Reference%20Architecture%20Monitoring%20and%20Automation.vsdx)

![image.png](.attachments/image-b7d333cb-7fac-46e4-ad4f-e339dae78277.png)

## Schema

The following schema is used for log **SQLAuditLog_CL**

```
[
  {
    "TenantId": "{GUID}",
    "SourceSystem": "{string}",
    "TimeGenerated": "{DateTime}",
    "ClientIp_s": "{string}",
    "ServerPrincipalName_s": "{string}",
    "DatabasePrincipalName_s": "{string}",
    "ServerInstanceName_s": "{string}",
    "DatabaseName_s": "{string}",
    "ObjectName_s": "{string}",
    "ClassTypeDescription_s": "{string}",
    "SecurableClassType_s": "{string}",
    "ActionName_s": "{string}",
    "ApplicationName_s": "{string}",
    "Succeeded_b": "{bool}",
    "SequenceNumber_d": "{double}",
    "ActionId_d": "{double}",
    "SessionId_d": "{double}",
    "ServerPrincipalId_d": "{double}",
    "DatabasePrincipalId_d": "{double}",
    "ObjectId_d": "{double}",
    "ClassType_d: ": "{double}",
    "Type": "SQLAuditLog_CL"
  }
]
```