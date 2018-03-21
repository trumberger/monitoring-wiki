# Title

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