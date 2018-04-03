##Overview: 
This section provides an overview on how to enable and validate Resource Monitoring in a subscription.

##Activities

- Execute runbook: **RUN-EnableResourceMonitoring** to enable diagnostics (manual step) :
Navigate to [Resource Group](https://ms.portal.azure.com/#@microsoft.onmicrosoft.com/resource/subscriptions/c8cd80a0-4450-4b56-9245-2842d6f6357a/resourceGroups/MonitoringPlatform-STAG/providers/Microsoft.Automation/automationAccounts/AAA-STAG-Automation-BPL-MON/runbooks/RUN-EnableResourceMonitoring/overview) named `MonitoringPlatform-$(Environment)`
Select the runbook **RUN-EnableResourceMonitoring** and click Start. (see Notes 1)

- Validate if Azure activity log for subscription is pointing to Log Analytics in staging (manual step)
Navigate to each [Resource Group](https://ms.portal.azure.com/#@microsoft.onmicrosoft.com/resource/subscriptions/c8cd80a0-4450-4b56-9245-2842d6f6357a/resourceGroups/MonitoringPlatform-STAG/diagnostics) in the subscription and in the Diagnostic Logs blade and you can check for the correct Log Analytics target by clicking on each resource. (see Notes 2)

 - Validate if Security Center for subscription is pointing to Log Analytics in staging (manual step)
Navigate to the [Security Policy](https://ms.portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/1) blade in Security Center, click on the desired Subscription and under Data Collection check the workspace name. (see Notes 2)

##Notes: 
1. Not all resources can have monitoring enabled so some resources will show as failed. 
2. **Workspace/LogAnalytics** target naming is similar to `OLA-$(Environment)-DataStore-$(serviceID)`

