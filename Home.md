# Introduction
Welcome to the ESS global monitoring team. This section provides an overview of the monitoring platform, the used technologies and the team structure. The ESS organization uses a standardized monitoring solution for all its global customers. This solution needs to be able to monitor

## References
### Documents
The following references can be used to better understand the monitoring solution
| Document| Comment |
|---|---|
|[High Level Overview](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationPlatform/_layouts/15/WopiFrame2.aspx?action=edit&sourcedoc={EC2E740B-6D65-4A39-BB29-3C7DBE81D1C6}) | Presentation that provides an high level overview of the goals of the monitoring environments, its capabilities and how it is used within EAS engagements.|
| [Architecture](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationPlatform/Shared%20Documents/General/BPL%20-%20Reference%20Architecture%20Monitoring%20and%20Automation.vsdx) | Visio diagram visualizing the architecture of the monitoring environment as it currently is.  

### Wiki
All other documentation regarding the monitoring platform, work instructions and policies are written in markdown and are part of this Wiki. The Wiki is setup in the following way.
| Wiki | Comment |
|---|---|
| [Policies](https://easplatform.visualstudio.com/Monitoring/_wiki/wikis/Monitoring.wiki?wikiVersion=GBwikiMaster&pagePath=%2FPolicies) | Describes the policies that ESS is using like naming conventions, access controls, etc.  |
| [Work Instructions](https://easplatform.visualstudio.com/Monitoring/_wiki/wikis/Monitoring.wiki?wikiVersion=GBwikiMaster&pagePath=%2FWork-Instructions) | Describes the work instructions for the monitoring. This can be either internal setup or instruction for EAS delivery teams within the customers subscription. |
| [Technical Details Platform](https://easplatform.visualstudio.com/Monitoring/_wiki/wikis/Monitoring.wiki?wikiVersion=GBwikiMaster&pagePath=%2FTechnical-Details-Monitoring-Platform) | Provides details information about the monitoring solution like used schema's, made decisions, restrictions that apply, etc. 
| [Research](https://easplatform.visualstudio.com/Monitoring/_wiki/wikis/Monitoring.wiki?wikiVersion=GBwikiMaster&pagePath=%2FResearch) | Provides a working directory for notes and other items that are collected during the research of new capabilities of the monitoring platform. |

### Environments & Repositories
The following environments and repositories are used by the platform
| Location | Comment |
|---|---|
| Monitoring Platform Production Environment | Azure Subscription where the monitoring platform production environment is hosted. |
| Monitoring Platform Test & Staging environments | Azure subscription where the monitoring platform test and staging environment is hosted. |
| [VSTS Project Repository](https://easplatform.visualstudio.com/Monitoring) |
| IcM Production Service |
| IcM Test & Staging environment |
| [Monitoring Team Site](https://teams.microsoft.com/_#/teamDashboard/ESS%20Monitoring%20%26%20Automation%20Platform) | 
| [Monitoring SharePoint Site](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationPlatform/Shared%20Documents/General) |
| Monitoring Team Alias | ess-monitoring@microsoft.com | 

### Internet
The monitoring platform is using native Azure capabilities. The following links provide more information regarding some key components of the platform. 

| Link | Comment |
|---|---|
| [VSTS](https://docs.microsoft.com/en-us/vsts/) | Used as repository and to fulfill all LSSM capabilities that the team is using; like release management, automated testing, day-to-day work tracking, etc. 
| [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/templates/) | Everything deployed to Azure is based on ARM. No manual activities are allowed in the production environment. |
| [IcM](https://icmdocs.azurewebsites.net/onboarding/Why%20IcM.html) | Incident Management tool that is used for our customers and internally. |
| [Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/) | Data Source for security and platform events and metrics
| [Azure Automation](https://docs.microsoft.com/en-us/azure/automation/) | Automation engine within customer subscription to automation operational activities.
| [Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/) | Data Source for application metric, instrumentation and user synthetics
| [Custom events & Telemetry](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics) | How to build instrumentation into application using Application Insights
| [Security Center](https://docs.microsoft.com/en-us/azure/security-center/) | tracks security of the application and azure subscription |
| [Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/) | All custom capabilities are written using Azure functions |
| [Logic App](https://docs.microsoft.com/en-us/azure/logic-apps/) | All (business) work flows are using Logic App | 

The following languages are currently used in the platform

| Language | Comment |
|---|---|
| PowerShell | Deployment and configuration scripts (either pre- or post deployment are written in PowerShell). In addition the automation engine's runbooks are also written in PowerShell. | 
| .NET C# | All Azure Functions use C# as coding language. |
| JSON | Deployment template (ARM) and configuration files are using JSON. |
| Mark Down | Documentation is written in Mark Down |
| Git | Communication between branches and local workstations is done with Git


