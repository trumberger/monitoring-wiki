## Introduction
IcM uses Service Tree for all "tenants".  Tenants are logically part of Service Categories in IcM allowing teams to have multiple tenants per category.  Services (used interchangeably with tenants) are required to onboard to Service Tree.  The onboarding to Service Tree doesn't equal completion of onboading to IcM.  The Service Tree entry is entered and then sent to IcM for approval and provisioning.  
 
## Procedure:
- Go to [aka.ms/servicetree]() 
- Click on 'Create a new Service'
- **organization**. Select 'Enterprise Services Delivery'
- **Service Type**. Select:
       Where is your service deployed --> Azure
       Targeted Locations --> Public
- **Profile Info**. Select:
       Service Name / Short Name --> Service-ID (See naming conventions, for example FIFA-DSP)
       Description --> Provide short overview of the Service
       Admin / PM Owner / Dev Owner / feature team alias --> Member of monitoring team
       Built By Microsoft / External Facing --> True
- **Metadata**. Select:
       Current Lifecycle Stage --> GA
- Submit

## Note
The service in service tree will be instantly provisioned. 

