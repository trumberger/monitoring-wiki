##Overview
This section describes the processes for Keys and Secrets rotation, to be in compliance with Security best practices.
This means resetting and recreating keys/secrets/passwords for all the resources that use them:

Ess-Mon Service Account
...... To be added ....


##Activities

###Ess-Mon Service Account
This account is currently enrolled in the 70 day password policy. This means that once every 70 days the password needs to be reset.

####Steps
1. Login to the corp network using your own user account.
2. Strike **Ctrl+Alt+Delete** keys simultaneously. This will launch the Windows Security dialog.
3. Click on **Change a password** button.
4. In user name field, replace your domain\alias with **REDMOND\ess-mon**
5. Type in the old password. (See Notes 1) 
    Type in the new password twice in the respective fields. (See Notes 2)
6. Confirm the new password by clicking on the **->** button.
7. Edit the **EssServiceAccountSecret** variable in the **Global Settings** variable group and save the new value.


##Notes
1. The current (old) password for the Ess-Mon account is found in the [VSTS Library](https://easplatform.visualstudio.com/Monitoring/_library?itemType=VariableGroups) in **Global Settings** -> **EssServiceAccountSecret**. 
2. Generate a new password with a high complexity making use of upper case and lower case letter, symbols and numbers. **!!!** Do not include the **$** symbol inside the password **!!!**
