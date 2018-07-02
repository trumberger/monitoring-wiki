The variable **targetResourceGroups** is used by the following runbooks:

RUN-VM.AddMonitorAgent
RUN-SQL.EnableAudit
RUN-CheckForPublicIPChange
RUN-EnableResourceMonitoring

The variable accepts regex  as per example below (select all resource groups that starts with letter G).

    "targetResourceGroups": {
      "value": [
        {
          "name": "regex:^G",
          "subscription": "632cc760-aa97-46a9-9c12-50b13163c9c7"
        },
        {
          "name": "BP-DEV-CustomerIntegration",
          "subscription": "632cc760-aa97-46a9-9c12-50b13163c9c7"
        },
        {
          "name": "BP-DEV-MonitoringAgent",
          "subscription": "632cc760-aa97-46a9-9c12-50b13163c9c7"
        }
      ]
    }

Regex information: https://technet.microsoft.com/en-us/library/2007.11.powershell.aspx

