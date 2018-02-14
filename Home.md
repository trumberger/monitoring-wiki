# Introduction
Welcome to the ESS global monitoring team. This section provides an overview of the monitoring platform, the used technologies and the team structure. The ESS organization uses a standardized monitoring solution for all its global customers. This solution needs to be able to monitor

## References
### Documents
The following references can be used to better understand the monitoring solution
| Document| Comment |
|---|---|
|High Level Overview | Presentation that provides an high level overview of the goals of the monitoring environments, its capabilities and how it is used within EAS engagements.|
| Architecture | Visio diagram visualizing the architecture of the monitoring environment as it currently is.  

### Wiki
All other documentation regarding the monitoring platform, work instructions and policies are written in markdown and are part of this Wiki. The Wiki is setup in the following way.
| Wiki | Comment |
|---|---|
| Policies | Describes the policies that ESS is using like naming conventions, access controls, etc.  |
| Work Instructions | Describes the work instructions for the monitoring. This can be either internal setup or instruction for EAS delivery teams within the customers subscription. |
| Technical Details Platform | Provides details information about the monitoring solution like used schema's, made decisions, restrictions that apply, etc. 
| Research | Provides a working directory for notes and other items that are collected during the research of new capabilities of the monitoring platform. |

### Internet
The monitoring platform is using native Azure capabilities. The following links provide more information regarding some key components of the platform. 

| Link | Comment |
|---|---|
| VSTS | Used as repository and to fulfill all LSSM capabilities that the team is using; like release management, automated testing, day-to-day work tracking, etc. 
| Azure Resource Manager | Everything deployed to Azure is based on ARM. No manual activities are allowed in the production environment. |
| IcM | Incident Management tool that is used for our customers and internally. |
| Log Analytics | Data Source for security and platform events and metrics
| Azure Automation | Automation engine within customer subscription to automation operational activities.
| Application Insights | Data Source for application metric, instrumentation and user synthetics
| Custom events & Telemetry | How to build instrumentation into application using Application Insights
| Security Center | tracks security of the application and azure subscription |
| Azure Function | All custom capabilities are written using Azure functions |
| Logic App | All (business) work flows are using Logic App | 

The following languages are currently used in the platform

| Language | Comment |
|---|---|
| PowerShell | Deployment and configuration scripts (either pre- or post deployment are written in PowerShell). In addition the automation engine's runbooks are also written in PowerShell. | 
| .NET C# | All Azure Functions use C# as coding language. |
| JSON | Deployment template (ARM) and configuration files are using JSON. |
| Mark Down | Documentation is written in Mark Down |
| Git | Communication between branches and local workstations is done with Git

## Monitoring Team Setup 
Discuss with Tyler

