Here are some brief notes on how to add a PowerShell-based test to a Release Pipeline. Please add to them as you complete this yourself.

# Overview
Building tests has the following steps:

Test creation:
- Create PowerShell scripts to set up/start your tests. Use TestRunId (see below) to inject a unique value into your test data.
- Create PowerShell scripts to validate the results, using the Pester framework (see below)

Release Pipeline
- Create a Guid Test Run ID
- Run your custom PowerShell script(s) to set up your test(s) 
- Add a delay long enough for your tests to complete
- Use the "ESS Monitoring: Run PowerShell-based test" task group to validate your results
- Use the "ESS Monitoring: Publish PowerShell-based test results." task group to publish the results

In detail:
## Create PowerShell scripts to set up/start your tests

Create a PowerShell script with your test in. It should follow the naming scheme similar to:
<Solution Area>.IntegrationTest.<Test Name>.Setup.ps1
Store the script in a project called Microsoft.EAS.Monitoring.<Solution Area>.IntegrationTests (creating it if it doesn't already exist)

e.g.:
MonitoringAgent.IntegrationTest.EndToEndValidation.Setup.ps1 in project Microsoft.EAS.Monitoring.MonitoringAgent.IntegrationTests

The script should take any parameters you think it needs, for example a Test Run Id so you can use unique values in the script. Here's one example of a parameter set you may wish to use:

```
#region parameters
Param(
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $TestRunId,
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $ResourceGroupName,
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $Environment
)
#endregion
```

## Create PowerShell scripts to validate your test results
Validation scripts use the "Pester" test framework. That allows you to write code like this:
`Find-AzureRmResource -ResourceGroupNameContains "$ResourceGroupName" | Should Not Be $null`
The above line of code verifies that the Resource Group exists (i.e. that Find-AzureRmResource does not return null). See Pester documentation for more info.

So, create a PowerShell script with your validation test/tests in. It should follow the naming scheme similar to:
<Solution Area>.IntegrationTest.<Test Name>.Validate.ps1


Your script MUST follow the template in the below code block (including parameters. If you need additional parameters, speak to Duncan).
```
#region parameters
Param(
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $TestRunId,
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $ResourceGroupName,
	[parameter(mandatory=$true, ValueFromPipelineByPropertyName=$true)] [string] $Environment
)
#endregion

Describe -Name '<suitable name here>' -Tags '<suitable tags here>' -Fixture {
    It -name '<suitable name here>' -test {
        <your powershell here to validate... e.g.: Find-AzureRmResource -ResourceGroupNameContains "$ResourceGroupName" | Should Not Be $null>
    }
}
```
 
Then, in your release pipeline:

## Create a Guid to represent the Test Run Id
Add the "GUID Generator" task to your pipeline and name the variable TestRunId

![image.png](.attachments/image-89885041-b121-49e2-b939-37844a7043d9.png)

## Run your custom PowerShell scripts to set up your tests
Simply use the Azure PowerShell task to do this:
![image.png](.attachments/image-954cb771-040f-4b8b-bd08-e91e62273c99.png)

## Delay long enough for your tests to complete
- Add an "Agentless Phase"

![image.png](.attachments/image-71ec113b-0269-4413-b290-7aff56ec3b3d.png)

- Add a delay task to it
![image.png](.attachments/image-4d166db9-cfdf-4d4d-b84e-c8fd5a5b5492.png)

## Use the "ESS Monitoring: Run PowerShell-based test" task group to validate your results using your Pester scripts (the ones that end .Validate.ps1)
![image.png](.attachments/image-e32dbe90-1656-49e8-81df-69b1e0315c7a.png)

## Use the "ESS Monitoring: Publish PowerShell-based test results." task group to publish the results
(no configuration is needed)
![image.png](.attachments/image-bb87d39e-e7d0-409f-8be7-bbebd0ca1801.png)

## Run your pipeline
If all is well, you'll see something like this on the output:
![image.png](.attachments/image-e487c2c6-7814-463d-8bfc-6f86a214092a.png)