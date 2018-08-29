**History**
Since US1517, the ARM generators where combined into one script which can generate the following:

- Metric Alert Rules ARM template (standard)
- Alert Rules ARM template (standard)
- Alert Framework ARM template (our custom format)

**Location:**
The script can be found here:

https://easplatform.visualstudio.com/_git/Monitoring?path=%2Fsrc%2FMicrosoft.EAS.Automation%2FPipeLineScripts%2FPre-GenerateARMTemplatePipeline.ps1&version=GBmaster

**Usage:**

a) **Parameters**

```
Param(
[string] [Parameter(Mandatory=$true)] $PathExcel,
[string] [Parameter(Mandatory=$true)] $Scope,
[string] [Parameter(Mandatory=$true)] $PathJSON,
[switch] [Parameter(Mandatory=$false)] $OverwriteExisting,
[switch] [Parameter(Mandatory=$false)] $WarnIfInputFileNotFound,
[string] [Parameter(Mandatory=$true)] $sourceInstance
)
```

$**PathExcel** -> the input file (i.e : https://easplatform.visualstudio.com/_git/Configurations?path=%2FBPL-MON%2FBBDV%2FBPL-MON.MonitoringAlerts.xlsx&version=GBmaster)

!Note: The Excel file needs to have an exact format in terms of columns.

$**Scope** -> Possible values: AlertFramework, AlertRules, MetricAlertRules

$**PathJSON** -> the output file

Example: [af.json](/.attachments/af-c27bb658-2524-4390-ba60-a7318dd46e26.json)

$**OverwriteExisting** -> It is required if the JSON file already exists, in order to be replaced.

$**WarnIfInputFileNotFound** ->
If the Excel is not provided/is not found and the parameter is set then only a warning is displayed.
If the Excel is not provided/is not found and the parameter is NOT set then an exception is thrown.

$**sourceInstance**
The Application Insights ID

b) **Command line**:

.\Pre-GenerateARMTemplates_WE.ps1 -Scope AlertFramework -PathExcel "full_path_to_Excel_file" -PathJSON "full_path_to_JSON_file" -OverwriteExisting -WarnIfInputFileNotFound -sourceInstance "appinsightsid"