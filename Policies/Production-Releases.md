# Introduction

This section describes the release process of the ESS monitoring platform to production.

## Trunk Based Development

The ESS monitoring team have adopted the [trunk based development model](https://trunkbaseddevelopment.com/). 

<IMG src="https://trunkbaseddevelopment.com/trunk1.png"/>

This means that development always takes place in the master branch. Every User Story has it's own branch that will be merged into the master branch afterwards (using a Pull Request). Separate branches will be created for releases to production. If necessary updates out of the master can be cherry picked into these release branches. 


## Frequency of releases

After every (2 weeks) sprint a production release is performed (unless there are no changes to the environment or an emergency change need to be performed). In the future the frequency will be increased.

## Versioning

Parts of the monitoring platform have multiple simular instances (monitoring agent) are running in customer subscriptions. To be able to support this the following versioning is defined for the monitoring platform.

`version x.y.z (example: v1.5.12)`

| letter | Type | Comment |
|-|-|-|
|x|Major Version| Major version of the monitoring platform. Version is determined by product manager. |
|y|Minor Version| This number will be increased for every release (if it is not a major version change). |
|z|Revision|  |

## Process

The release process is as follows

```
PRODUCTION RELEASE
|--> TAG AND CREATE RELEASE BRANCH
|----> PERFORM INTEGRATION AND UAT TESTINGS IN STAGING
|------> CREATE RELEASE NOTES
|--------> TRIGGER PRODUCTION BUILD
|----------> NOTIFY AND RELEASE
```

### Tag and Create Release Branch

At the end of each sprint, all pull requests to the master branch are created Wednesday end of day, so the development lead can review and approve these requests on Thursday. All approved PRs are merged into master and make up the production release. Thursday at 2pm Pacific Time the team lead will tag the master branch with the labels `release` and `vx.y` if there are no errors in staging. Next a new branch will be created named `release.x.y`. This branch will be released into Pre-Prod (using production pipeline).

### Perform Integration and UAT testing

All required integration and acceptance tests are performed on Friday. The required UAT and Integration tests will be performed in pre-prod. Someone from the team will be assigned to perform these tests. 

### Create Release Notes

During the integration and uat testing the team lead will create release notes of the upcoming production release, based on the user story that the team has worked on. The release notes will be extended in ReleaseNotes.md file in the root.  

### Trigger Production Release

Production Release starts with the approval of the Dev Lead or Product Manager at the start of the sprint planning (next sprint) with no objections from the team and / or bugs found during the tests. After approval the production release pipeline will continue where it left of from the Pre-Prod to deploy the different components (business logic / customer integration / monitoring agent) in the ESS PROD subscription.  In parallel the Dev Lead or Product Manager will start the releases for the monitoring agents in the customers subscriptions (according to the approvals setup in their pipeline).

For the monitoring agents that don't use the ESS VSTS instance to deploy the monitoring agent, the artifacts to deploy the monitoring agent will be copied to a common share for the different teams to download (See Monitoring Agent Artifacts below)

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

[https://esscommonprod.blob.core.windows.net/releases/latest](https://ms.portal.azure.com/#blade/Microsoft_Azure_Storage/ContainerMenuBlade/overview/storageAccountId/%2Fsubscriptions%2F16b26395-68e3-45e2-81c1-54729c26aba8%2FresourceGroups%2FPROD-CommonArtifacts%2Fproviders%2FMicrosoft.Storage%2FstorageAccounts%2Fesscommonprod/path/releases/etag/%220x8D60D3177D6721E%22)

The share is only used by EAS delivery teams that deploy the monitoring agent out of the application pipeline. They can download the artifacts and push them into their repository (as pull request).

The following artifacts will be used currently:

| Artifact | Explanation |
|-|-|
| deploy.monitoringagentprerequisites.json | Template that deploys storage account where artifacts are copied towards.
| deploy.monitoringagent.json | Template that deploys the monitoring agent|
| deploy.monitoringagent.parameters.json | Contains the parameters used to deploy the monitoring agent. This file will not contain actual parameters (except for default values).|
| scripts\Pre-Spn-CreationAndValidation.ps1 | The script that creates and assigns an SPN for the monitoring agent. |
| script\Pre-Spn-CustomRoleCreation.ps1| The script that creates the ESS Custom Role for least privileged use |
| runbooks\* | All runbooks that will be available in the Azure Automation Account of the monitoring agent. |
| views\* | All OMS dashboards that will be available in the monitoring agent. |
