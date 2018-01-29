## Solution Overview
Below is a reference architecture for the monitoring platform:  
![Reference Architecture](.../Assets/ReferenceArchitecture.png "Reference Architecture")

## Guiding Principles
**Monitor everything on Azure - resources, applications, custom events, etc.**  
The base platform allows monitoring the full spectrum within Azure.  It will natively monitor all resource and infrastrucure relatedd metrics and events using Azure Monitor.
Using agents, it can collect any type of event and metric on bot hWindows and Linux.  Finally using Applicaiton Insights integration, it can monitor custom events and telemetry that is put into the application

**Automation Engine**  
Using the Operations Management Suite (OMS) the platform not only provides monitoring capabilities, but aslo an automatoin engine that can be used within the customer's environment.

**Monitoring User Synthetics and business KPIs**  
The platform allows for user synthetics and business KPIs to be monitored and reported on.

**Standardized and flexible**  
The platform itself consists of a numbe of components both shared and dedicated to customer.  All of these components are under version control and have automated release processes to ensure consistency and predictability.

**Toolbox for Microosft Delivery Teams**  
No two applications are the same, thus the platform can be easily extended to fit the applicaiton or workload needs.
The goal of hte platform is to provide delivery teams with the right tool and guidance on how to implement in the form of readmes, examples scripts, how-tos, code snippets, etc.

**24x7 On-Call notification capabilities**  
The monitoring platform has the capability to call out to ensure that Microsoft support is responding to any alerts triggered outside business hours.

**Server-less design**  
The entire platform is serverless, meaning no operational maintenance like patching is required.

# Roadmap
| Feature | Status | ETA |
|---------|--------|-----|
| Add alerts into monitoring templates | Backlog | TBD |
| Enable hybrid and multi cloud scenarios | Backlog | TBD |
| Adopt broadly accepted instrumentation library | Backlog | TBD |
| Enable O365 and Dynamics365 monitoring | Backlog | TBD |
| Enable advanced analytics and machine learning on Kusto data set| Backlog | TBD |
| Enable PowerBI for multi-tenant scenarios | Backlog | TBD |
| Enable transactional montoring (using Zipkin or native .Net capabilities) | Backlog | TBD |