# Technical Details

## Overview

This sections provides an technical in-depth overview of the monitoring platform that is in use.

## Purpose of the ESS Monitoring and Automation platform

The purpose of the platform is to have standardized approach to monitor and manage our ESS customers workloads.

## Architectural Diagram

This [visio](https://microsoft.sharepoint.com/teams/ESSMonitoringAutomationTeam/Shared%20Documents/General/BPL%20-%20Reference%20Architecture%20Monitoring%20and%20Automation.vsdx) provides an overview of the architecture of the ESS Monitoring & Automation platform.

## Platform Components

The platform consists of three different components. Each component is described in more detail further on.

| Component | Purpose |
|-|-|
| Monitoring Agent | The monitoring agent is deployed to the customer's environment. The agent has capabilities to capture monitoring and logging data, automate certain tasks and triggers alerts. All captured monitoring data will stay in the customer's environment for a certain period of time. Each customer environment (PROD / UAT / etc) can have its own monitoring agent. In addition the agent will be deployed as close to the customer's workload as possible. If the customer's workload is distributed across multiple region, multiple instances of the monitoring agent will be deployed. |
| Customer Integration | Monitoring agents will push their events to the customer integration components. Each service / customer has its own integration components that consists of a number of APIs and functions communcating with the monitoring agent. Received events will be processed and enriched accordingly and passed through to the Business Logic layer. |
| Bussiness Logic | The Business Logic layer received events coming from the customer integration layer and applies business logic and correlation to it. The Bussines Logic is shared between all ESS customers and will automate ESS business processes and connectivity towards Microsoft internal tools. |   