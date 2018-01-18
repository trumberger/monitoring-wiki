# Overview

# Activities
Prepare parameters files in `configuration\{service-ID}`
Setup Service principle in Azure
Open monitoring release pipeline and clone BPL-MON environment
Configure environment for customer instance
trigger release in VSTS
Enable managed API connections for Application Insights / Kusto / LA 

# Notes
**Region**

**Region code**

**Start DateTime of Daily scheduler**
This always need to be at least 5 minutes in the future on the moment of deployment. 

**Job Scheduler Name**
For every runbook that is associated with a schedule a job schedule need to be created. The job schedule needs a GUID as name.
