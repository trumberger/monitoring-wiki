# Overview

# Activities
Prepare parameters files in `configuration\{service-ID}`
Setup Service principle in Azure
Open monitoring release pipeline and clone BPL-MON environment
Configure environment for customer instance
trigger release in VSTS
Enable managed API connections for Application Insights / Kusto / LA
Create Run As Account in Azure Automation account
Execute configuration scripts:
- Enable monitoring resources
- Enable SQL audit (if applicable)
- Enable VM monitoring (if applicable)
Enable Activity Log monitoring to platform
Validate security Center monitoring to platform
 

# Notes
**Region**

**Region code**

**Start DateTime of Daily scheduler**
This always need to be at least 5 minutes in the future on the moment of deployment. 

**Job Scheduler Name**
For every runbook that is associated with a schedule a job schedule need to be created. The job schedule needs a GUID as name.
