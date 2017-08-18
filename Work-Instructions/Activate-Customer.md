## Introduction
IcM uses Service Tree for all "tenants".  Tenants are logically part of Service Categories in IcM allowing teams to have multiple tenants per category.  Services (used interchangeably with tenants) are required to onboard to Service Tree.  The onboarding to Service Tree doesn't equal completion of onboading to IcM.  The Service Tree entry is entered and then sent to IcM for approval and provisioning.  

Pre Requisites:
- Team Alias (Triage Team / Incident Manager Team / executive incident manager in ICM)
- List of regions 
 
Internal Roles in Tools

|Role |Tool |Default |
|---|---|---|
|Admin Alias |Service Tree |Monitoring Team Alias |
|Dev Owner Alias |Service Tree |Monitoring Team Alias | 
|PM Owner Alias |Service Tree |Monitoring Team Alias | 
|Feature Team Alias |Service Tree |Monitoring Team Alias | 
|Triage Team |IcM |Delivery Team Alias | 
|Incident Manager Team |IcM |Delivery Team Alias | 
|Executive Incident Manager |IcM |Delivery Team Alias | 


# Procedure 03: Create Certificate

## Overview
For every service a unique certificate is required to connect to the IcM tenant. 

## Activities
[Create Certificate](https://microsoft.sharepoint.com/teams/WAG/EngSys/IncidentManagement/IcM%20User%20Guide/Obtaining%20a%20certificate.aspx)

## Notes
- Use Internet Explorer in Administration mode to perform activities

## Parameters
The following parameters are used
|Item|Value|Comment|
|---|---|---|
|Approving Manager|Gene Schoepp|If you are in Cross Domain Organization|
|Subject / CommonName|{ServiceID}connector|Example: FIFA-DSPConnector|
|Notification| ADD GROUP Alias| Monitoring Team (group alias is required)| 

