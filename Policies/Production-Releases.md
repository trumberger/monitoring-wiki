# Introduction

This section describes the release process of the ESS monitoring platform to production.

## Frequency of releases

After every (2 weeks) sprint a production release is performed (unless there are no changes to the environment or an emergency change need to be performed). In the future the frequency will be increased.

## Versioning

Parts of the monitoring platform have multiple simular instances (monitoring agent) are running in customer subscriptions. To be able to support this the following versioning is defined for the monitoring platform.

`version #.x.y.z (example: v1.5.2.12)`

| letter | Type | Comment |
|-|-|-|
|#|Major Version| Major version of the monitoring platform. Version is determined by product manager. |
|x|Agent Changed|This number will be increased as the monitoring agent is changed compared to previous release. |
|y|Back-end Changed|This number will be increased as the ESS back-end (customer integration and/or busines) changed compared to previous release. |
|z|Revision|  |

## Process

The release process is as follows

```
PRODUCTION RELEASE
|--> FREEZE MASTER
|----> PERFORM INTEGRATION AND UAT TESTINGS IN STAGING
|------> TRIGGER PRODUCTION BUILD
|--------> NOTIFY AND RELEASE
```

### Freeze Master

All final code for sprint is commited to master and pushed to Staging Environment. This should happen last thursday of the sprint EoD.

### Perform Integration and UAT testing

All required integration and acceptance test are performed. The required UAT and Integration tests will be perform in staging. Someone from the monitoring team will be assigned to perform these tests. **TODO: Add the right tests to execute**

### Trigger Production Release

Production Release starts with a build that is manually triggered at the start of sprint planning (next sprint) with no objections from the team and / or bugs found during the tests. The production build will result in package that can used for the ESS VSTS release pipeline for the different components (business logic / customer integration / monitoring agent) in the ESS subscription and the monitoring agents in the customers subscriptions (according to the approvals setup in their pipeline).

For the monitoring agents that use the application VSTS instance to deploy the monitoring agent, the artifacts to deploy the monitoring agent will be copied to a common share for the different teams to download (See Monitoring Agent Artifacts below)

### Notify and release

A successfull build will automatically trigger the following releases:

- Production release of the ESS back-end services (business logic and customer integration)
- Monitoring agent release for ESS internal (no approval required for deployment).
- Monitoring agent release for customers (going to ask for EAS Delivery teams approval to proceed to their UAT).

A successfull build will automatically trigger the following notifications:

- To ESS monitoring team that production release is about to commence.
- To EAS delivery teams using ESS monitoring VSTS pipeline that new production release is awaiting there approval to move to their UAT.
- To EAS delivery teams using own VSTS pipeline that new production package is ready for them to download.

## Monitoring Agent Artifacts

All artifacts required to deploy the monitoring agent are copied to the following share in a folder with the version name:

`https://esscommonprod.blob.core.windows.net/agent/{version}`

The share is only used by EAS delivery teams that deploy the monitoring agent out of the application pipeline. They can download the artifacts and push them into their repository (as pull request).

The following artifacts will be used currently:

| Artifact | Explanation |
|-|-|
| deploy.monitoringagent.json | Template that deploys the monitoring agent|
| deploy.monitoringagent.parameters.json | Contains the parameters used to deploy the monitoring agent. This file will not contain actual parameters (except for default values).|
| scripts\Pre-Spn-CreationAndValidation.ps1 | The script that creates and assigns an SPN for the monitoring agent. |
| sqlaudit\deploy.sqlauditcollector.json | Template that deploys the SQL Audit Collector resources. |
| sqlaudit\deploy.sqlauditcollector.parameters.json | Contains the parameters used to deploy the SQL Audit Collector. This file will not contain actual parameters (except for default values). |
