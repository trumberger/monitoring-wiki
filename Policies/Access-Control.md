## Intro
This section describes the Access control that ESS uses when no other customer RBAC model or Access Control policy is in place

## Subscription Setup
- Subscription per environment (TEST / DEV / UAT / PROD)
- ARM template per resource group
- Application Monitoring resources part of application 
- Monitoring components in single resources group

## Standard Model
Default model used by ESS 
| Group | non-UAT & PROD | Staging (UAT) | Production | Comment
|---|---|---|---|---|
| End-User | - | - | - |
| Customer L1 | - | - | Read-only |
| Customer App Support | - | Read-only | Read-only |
| Development | Contributor | Contributor | Read-only |
| Operations | Read-only |  Contributor |  Contributor | 
| Monitoring | Read-only | Read-only | Read-only | Only contributor in monitoring resource group | 

TODO..

Not sure there is much to review about privileged access policies. What I tested and we can go over when you want:
-	We can have users who are always allowed to elevate rights (such as I and Attila)
-	These users can be regular users in the AD and normal readers/contributors to the subscriptions
-	When a user needs to elevate their rights, he needs to go through an approval process that takes 2-3 minutes. There are separate (albeit similar) processes that allow the user to get admin rights on the subscription or on the resources (I could in theory become a global administrator in the tenant without permissions on the subscription and vice-versa)
-	The access is time limited, for up to 8 or 12 hours (I don’t remember)
-	Every 3 months, the privileged access model needs to be granted again, otherwise users won’t be able to elevate their rights any more
-	The user who configures privileged access for the first time automatically becomes the security administrator

My personal suggestion:
-	Use admin@kpmg... To configure privileged access for me and Attila.
-	Put an alert in place so that all logins for this account triggers an incident. We should only access this account once every 3 months, when granting ourselves rights again. Everything else we can do with our own accounts in an audited manner.
