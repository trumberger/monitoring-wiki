# Monitoring Agent

## Overview

The monitoring agent is deployed to the customer's environment. The agent has capabilities to capture monitoring and logging data, automate certain tasks and triggers alerts. All captured monitoring data will stay in the customer's environment for a certain period of time. Each customer environment (PROD / UAT / etc) can have its own monitoring agent. In addition the agent will be deployed as close to the customer's workload as possible. If the customer's workload is distributed across multiple region, multiple instances of the monitoring agent will be deployed.

## Data Collection

The monitoring agent collects data from Azure in multiple data sources each with its own retention.

### Log Analytics

The Log Analytics data source has a retention that can be set for each environment. The default retention is 30 days and this can be extended to 730 days if customer requires. This data source is considered 'hot' data and can be queried any time. Log Analytics contains the following data:

| Data Type | Reference | Comment |
|-|-|-|
| Azure Resource Metrics | List with available metrics are captured [here](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-supported-metrics)
| Azure Resource Diagnostics | List and schema of available diagnostics are captured [here](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema)
| Azure Acitivity Logs | List and schema for activity log are captured [here](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-activity-log-schema)
| Virtual Machine Events | Security events from virtual machine are stored. Default collection is set to [Common](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-data-collection#data-collection-tier)
| SQL audit Logs | Schema for SQL audit log events are captured here | is optional |
| Azure Active Directory Audit Logs | Schema for AAD audit logs are captured here | is optional |
| Azure Acitive Directory Sign-in Logs | Schema for AAD sign-in logs are captured here | is optional |
| Azure Security Center events

### Storage Blob

The storage blob data source has a retention period for some of its data types. This data source is to be considered 'cold' data meaning it cannot be querried and is used for staging, archiving, auditing and configuration purposes. Storage Blob contains the following data:

| Data Type | Reference | Comment |
|-|-|-|
| SQL Audit Logs | | All SQL databases and servers will push audit data to this account. The account act acts as a staging environment for the SQL audit collector to process the logs and push it Log Analytics. Retention for these logs are set for two days. |
| Archive Data | | Datasets out within Log Analytics can be archived for longer period of time for audit purposes. No retention is set for data in the archive. |
| Configuration Data | Alert Definitions | All alert definitions for a particalur environment are stored a JSON file for alert framework to process. |

**Note:** Application instrumentation and telemetry is not captured by the monitoring agent, but should be captured as part of the applciation (Application Insights Agent)

## Functonality

The monitoring agent has the following functionality

| Functionality | Source | Explanation |
|-|-|-|
| Alerting Framework | Logic App |
| AAD Audit Collector | Azure Automation |
| SQL Audit Collector | Azure Automation |
| Archiving | Azure Automation |
| Diagnostics Dashboard | Log Analytics |
| Security Dashboard | Log Analytics |

## Azure Resources

The following azure resources are part of the monitoring agent

| Resource | Naming | Comments |
|-|-|-|
| Automation Account | AAA-{environment}-Automation-{serviceID} |
| Runbook: Archive Monitoring Data | RUN-ArchiveMonitoring |
| Runbook: Collect Audit Events from AAD | RUN-CollectAuditEventsAAD |
| Runbook: Collect Sign-in Events from AAD | RUN-CollectSigninEventsAAD |
| Runbook: Enable Diagnostics Azure Resources | RUN-EnableResourceMonitoring |
| Runbook: Disable Diagnostics Azure Resources | RUN-DisableResourceMonitoring |
| Runbook: Push Events to Log Analytics | RUN-PushEventsToMonitoring |
| Runbook: Retrieve URL customer integration | RUN-RetrieveAlertWebhook |
| Runbook: Enable SQL auditing | RUN-SQL-EnableAuditing |
| Runbook: Install agent on VM | RUN-VM-AddMonitorAgent |
| Log Analytics Workspace | OLA-{environment}-DataStore-{serviceID} |
| Solution: Anti Malware | AntiMalware(OLA-{environment}-DataStore-{serviceID}) |
| Solution: Azure Activity | AzureActivity(OLA-{environment}-DataStore-{serviceID}) |
| Solution: Azure Automation | AzureAutomation(OLA-{environment}-DataStore-{serviceID}) |
| Solution: Security & Audit | Security(OLA-{environment}-DataStore-{serviceID}) |
| Solution: Security Center | SecurityCenterFree(OLA-{environment}-DataStore-{serviceID}) |
| Solution: Update Management | Updates(OLA-{environment}-DataStore-{serviceID}) |
| Logic App: Alert Framework | FLO-{environment}-AlertFramework-{serviceID} |
| Logic App: Scheduler AAD Collector | FLO-{environment}-SchedulerAadAudit-{serviceID} |
| Logic App: Scheduler Archiving | FLO-{environment}-SchedulerArchiving-{sericeID} |
| API Connection: storage blob | CON-{environment}-AzureBlob |
| Key Vault | KVL-{environment}-{serviceID} | For future use (DOES NOT ADD CONSUMPTION) |
| App Service | FUN-{environment}-{serviceID} | For future use (DOES NOT ADD CONSUMPTION) |
| App Service Plan | APL-{environment}-{serviceID} | For future use (DOES NOT ADD CONSUMPTION) |
| App Service Plan | APL-{environment}-SqlAudit-{serviceID} | Only deploy if SQL audit is enabled |
| App Service | WES-{environment}-SqlAudit-{serviceID} | Only deploy if SQL audit is enabled |
| Job Scheduler | SJC-{environment}-SqlAudit-{serviceID} | Only deploy if SQL audit is enabled |