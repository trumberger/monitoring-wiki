In order to generate an ARM template for new alert rule you will need two files:

- Pre-GenerateArmTemplateForMetricAlertRules.ps1
- An Excel file with a sheet 'MetricAlerts' in it.

Example:
 [ESS.Master.MonitoringAlertsF.xlsx](.attachments/ESS.Master.MonitoringAlertsF-97fde74f-9f00-479f-a45a-1c1b970fc511.xlsx)

The command used in order to generate the ARM template is the following:
.\Pre-GenerateArmTemplateForMetricAlertRules.ps1 -pathExcel "full_path_to_excel_file"

**Example**:
.\Pre-GenerateArmTemplateForMetricAlertRules.ps1 -pathExcel "C:\Users\bopetres\desktop\Master.MonitoringAlertF.xlsx"