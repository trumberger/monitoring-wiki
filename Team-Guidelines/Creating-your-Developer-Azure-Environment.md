# Introduction
When developing the ESS Monitoring Solution, each developer has their own Azure environment to develop and test new code before merging it to master. This helps ensure that master is always in a "potentially deployable state" by ensuring that only well-tested and complete code is merged. This article gives you the steps to create your own developer environment.

# Overview
A development environment consists of three main Resource Groups: **Business Logic, Customer Integration and Monitoring Agent.**

We use Release Pipelines to create all environments, including developer environments. For full technical details of their contents, see [Release Pipelines](/Technical-Details-Monitoring-Platform/Release-Pipelines).

At present, deployment of all three components is fully automated,  but the first time setting up your environment there is a manual step to do before deploying the Monitoring Agent.

Follow the steps below to deploy your developer environment:

- Deploy Business Logic and Customer Integration components 
- Create and customize an Environment Parameter file in the Configurations repository.
- Deploy the Monitoring Agent.

## Deploy Business Logic and Customer Integration Components

- [Log in to VSTS and navigate to the Releases tab](https://easplatform.visualstudio.com/Monitoring/_release)
- Clone `DEV - Reference - Release Pipeline to clone` 
- Edit your clone:
  - Rename it to `DEV - <your name> - Release Pipeline`
  - Go to Variables and set `OwnerInitials` to a unique two character string. Preferably your initials, unless someone else has already used those
  - Save your pipeline
- Create a release, and deploy Business Logic then Customer Integration

You now have BL + CI deployed. We now have to do a manual step before deploying Monitoring Agent:

## Deploying Monitoring Agent
### Customise Environment Parameter Files

**NOTE: you can't edit the Master branch directly, so you have to create a new branch, follow the next steps and then create a Pull Request for Master**

In the Configurations repository:

- Create a new folder inside BPL-MON and name it XXDV, where XX are your initials (note: it's critical to use the same initials you used in your pipeline!).
- Go to the `BPL-MON\DMDV` folder, copy both `alerts.monitoringagent.json` and `deploy.monitoringagent.parameters.json` files and paste them in your own folder
- Edit your `deploy.monitoringagent.parameters.json` file, updating it to match your deployment:
  - Replace “DM“ with your initials (this should change the three group names in the targetResourceGroup parameter, and the integrationURL parameter)

- Commit these changes to Git and Sync them.

### Complete the Deployment
Go back to your release pipeline and deploy the MonitoringAgent environment.
 
**NOTE: You may get a failure with a few resources saying "Conflict". If you get this, re-run the deployment and it will work second time. This is due to an as-yet undiagnosed occasional error deploying Azure PowerShell modules.**
## Conclusion
You should now have three fully deployed resource groups in the DEV subscription.