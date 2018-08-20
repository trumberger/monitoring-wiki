# Introduction
Welcome to the ESS global monitoring team. This section provides an overview of the monitoring platform, the used technologies and the team structure. The ESS organization uses a standardized monitoring solution for all its global customers. This solution needs to be able to monitor

## References
### Documents
The following references can be used to better understand the monitoring solution
| Document| Comment |
|---|---|
|[High Level Overview](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationPlatform/_layouts/15/WopiFrame2.aspx?action=edit&sourcedoc={EC2E740B-6D65-4A39-BB29-3C7DBE81D1C6}) | Presentation that provides an high level overview of the goals of the monitoring environments, its capabilities and how it is used within EAS engagements.|
| [Architecture](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationTeam/Shared%20Documents/General/BPL%20-%20Reference%20Architecture%20Monitoring%20and%20Automation.vsdx) | Visio diagram visualizing the architecture of the monitoring environment as it currently is. |
| [FAQ](/Work-Instructions/FAQ) | FAQ

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
| [Monitoring Platform Production Environment](https://ms.portal.azure.com) | Azure subscription where the monitoring platform production environment is hosted: <br/>**ID: 16b26395-68e3-45e2-81c1-54729c26aba8** <br/> **Name: ESS Monitoring Platform - Production** |
| [Monitoring Platform Staging environment](https://ms.portal.azure.com) | Azure subscription where the monitoring platform staging environment is hosted: <br/>**ID: c8cd80a0-4450-4b56-9245-2842d6f6357a**  <br/> **Name: ESS Monitoring Platform - Staging** <br/> <br/>Test & development environments are hosted in this subscription too. They are not always present and are created when required.  |
| [VSTS Project Repository](https://easplatform.visualstudio.com/Monitoring) | VSTS instance and project that is used by the monitoring team. 
| [IcM Production Service](https://icm.ad.msft.net/imp/v3/incidents/search/basic) | The IcM instance where all incidents come in for the Monitoring team regarding the monitoring platform. This can be both incidents triggered by the monitoring itself or transferred from other (EAS) teams. 
| [IcM Test environment](https://icm.ad.msoppe.msft.net/imp/v3/incidents/search/advanced?basicSearchInAdvancedSearch=true) | The IcM instance that can be used to test if incident creation and enrichment functionality of the monitoring platform is working. This environment is used by staging environment of the monitoring platform.  |
| [Monitoring Team Site](https://teams.microsoft.com/_#/teamDashboard/ESS%20Monitoring%20%26%20Automation%20Platform) | The team site that is used to collaborate between team members
| [Monitoring SharePoint Site](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationPlatform/Shared%20Documents/General) |The SharePoint site that is used to share documents. 
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
| [PowerShell](https://docs.microsoft.com/en-us/powershell/) | Deployment and configuration scripts (either pre- or post deployment are written in PowerShell). In addition the automation engine's runbooks are also written in PowerShell. | 
| [.NET C#](https://docs.microsoft.com/en-us/dotnet/csharp/) | All Azure Functions use C# as coding language. |
| [JSON](http://json.org/) | Deployment template (ARM) and configuration files are using JSON. |
| [Markdown](http://commonmark.org/help/) | Documentation is written in Markdown |
| [Git](https://git-scm.com/about) | Communication between branches and local workstations is done with Git


