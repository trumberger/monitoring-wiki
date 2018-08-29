In order to generate an ARM template for new alert rule you will need two files:

- Pre-GenerateArmTemplateForAlertRules.ps1
- An Excel file with a sheet 'Alerts' in it and 3 columns (Alert Name (2nd), Alert Description (5th) and Query (12th). 
**Example**: 
[ESS.Master.MonitoringAlertsF.xlsx](.attachments/ESS.Master.MonitoringAlertsF-d007bbfa-412f-4410-a786-785dcfe18a05.xlsx)

The command used in order to generate the ARM template is the following:
.\Pre-GenerateArmTemplateForAlertRules.ps1 -pathExcel "full_path_to_excel_file"

**Example**:
.\Pre-GenerateArmTemplateForAlertRules.ps1 -pathExcel "C:\Users\bopetres\desktop\Master.MonitoringAlertF.xlsx"
