## Monitoring Agent Parameters

These are the parameters the monitoring agent uses to configure itself in the customer environment. 

| Parameter | Default | Source Type | Source Location | Resource/Task Name | 
|-|-|-|-|-|
|dashboardsSasToken|$(DashboardsSasToken)|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Copy OMS Dashboards to Blob Storage
|runbooksSasToken|$(RunbooksSasToken)|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Copy Automation Scripts to Blob Storage
|serviceID|$(ServiceID)|Variable Group VSTS|Customer Settings*|ServiceID
|customer|$(CustomerName)|Variable Group VSTS|Customer Settings*|CustomerName
|certificate|CER-\$(Environment)-MonitoringAgent-\$(ServiceID)|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Get-CertificateArgument
|certificateSubject|CER-\$(Environment)-MonitoringAgent-\$(ServiceID)|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Deploy Monitoring Agent Components
|thumbprint|SEC-\$(Environment)-MonitoringAgent-\$(ServiceID)-Thumbprint|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Get-CertificateThumbprintArgument
|integrationURL|https:// fun-$(Environment)-custint-\$(ServiceID).azurewebsites.net|ARM template
|integrationKey|\$(KEY-MSFT-IntegrationKey)|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Download from Key Vault: Integration Key
|automationName|Use ESS Naming Convention|ARM template
|monitoringName|Use ESS Naming Convention|ARM template
|monitoringRetention|30|ARM template
|monitoringLocation|$(DeploymentLocation)|Variable Group VSTS|Environment Settings*|DeploymentLocation
|environment|$(Environment)|Variable Group VSTS|Environment Settings*|Environment
|instance|Single Instance|ARM template
|version|1.0|ARM template
|capabilities|Everything disbabled|ARM template
|spnMonitoringAgentId|SEC-\$(Environment)-MonitoringAgent-\$(ServiceID)-SpnAppId|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Get-SPN-MonitoringAgentId
|spnMonitoringAgentSecret|KEY-\$(Environment)-MonitoringAgent-\$(ServiceID)-Pass|Task VSTS|ESS Monitoring: Deploy Monitoring Agent|Get-SPN-MonitoringAgentSecret
|spnReleasePipelineId|$(ReleasePipelineSPNObjectId)|Variable Group VSTS|Environment Settings*|ReleasePipelineSPNObjectId
|targetResourceGroups||ARM template|
