## Intro
This section describes the Access control that Monitoring team uses.

## Architectural guidelines applied
- Subscription per environment (TEST / DEV / UAT / PROD)
- ARM template per resource group
- Working with least privileged access for users
- All admin activities should be logged
- Support resources in Azure in single resources group

## Access Model - Azure (internal subscriptions)

The access model is based on the [different personas](https://easplatform.visualstudio.com/Monitoring/_apps/hub/agile-extensions.personas.personas-work-hub)  that the monitoring team identified

| Group | Organization | Development | Staging (UAT) | Production | Comment
|---|---|---|---|---|---|
| Application Owner | Customer | - | - | - | |
| Developer | Customer / Microsoft | - | - | - | |
| EAS DevOps Engineer | Microsoft | - | - | Read-only | Option to elevate permissions to Key Vault writer in PROD |
| Monitoring Contributor | Microsoft | Contributor | Contributor | Read-only | |
| Monitoring Team Member | Microsoft | Owner | Owner | Read-only | Option to elevate permissions in PROD |
| Security Officer | Customer | - | - | Read-only | Only if required |
| Service Delivery Manager | Microsoft |  - |  - | Read-only | 
| Service Desk | Customer | - | - | - | |
| Support Engineer | Customer / Vendor / Microsoft | - | - | - | |
| Senior Leadership | Microsoft | - | - | Read-only | |

**NOTE**: Azure Privileged Identity manager will be used for to elevate permission. This is not implemented yet

### Service Principles
The following [Wiki article](https://easplatform.visualstudio.com/Monitoring/_wiki/wikis/Monitoring.wiki?wikiVersion=GBwikiMaster&pagePath=%2FWork%20Instructions%2FCustomer%20Activition%2F02.%20Customer%20Facing%2F03.%20Create%20Service%20Principles%20for%20Monitoring%20Platform) provides an overview of the Service Principles the monitoring platform uses within our customer's and our own tenant. 


TODO
VSTS and IcM access