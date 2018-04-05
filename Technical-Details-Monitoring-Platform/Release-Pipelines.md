# Introduction
The Monitoring Solution is deployed using a series of Release Pipelines.

At present we have the following types of pipeline:

| Release Pipeline Type |  Description |  
|:---------------|:----------|
| Development | Deploys a developer's work from any branch into their personal development environment. Deploys three architectural components (Business Logic, Integration for BPL-MON, Monitoring Agent)   
| Staging  | Deploys the master branch into the Microsoft Staging environment. Deploys three components (Business Logic, Integration for BPL-MON, Monitoring Agent)
| Production (Business Logic) | Deploys Business Logic components from the production branch into the Production environment. 
| Production (Customer Integration v2) | Deploys Customer Integration components for all customers from the production branch into the Production environment. 
| Production (Customer Integration) | Obsolete pipeline which deploys Customer Integration components for all customers from the production branch into the Production environment.
| Production (Monitoring Agent) | One pipeline per-service. Deploys Monitoring Agent components into all customer environments for that service (for example Accor-FOLS deploys to 7 distinct customer environments, including UAT, Training, Production LATAM, etc.) 
| (Coming soon) Production| Deploys master branch into the shared Staging environment. Deploys three components (Business Logic, Integration for BPL-MON, Monitoring Agent)