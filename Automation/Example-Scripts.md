**Retrieve Azure Function Keys in PowerShell**

```
function Get-KuduApiAuthorisationHeaderValue($resourceGroupName, $webAppName)
{
    $publishingCredentials = Get-PublishingProfileCredentials $resourceGroupName $webAppName
    return ("Basic {0}" -f [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $publishingCredentials.Properties.PublishingUserName, $publishingCredentials.Properties.PublishingPassword))))
}

function Get-MasterAPIKey($kuduApiAuthorisationToken, $webAppName )
{
    $apiUrl = "https://$webAppName.scm.azurewebsites.net/api/functions/admin/masterkey"
    $result = Invoke-RestMethod -Uri $apiUrl -Headers @{"Authorization"=$kuduApiAuthorisationToken;"If-Match"="*"} 
    return $result`
}
 
function Get-HostAPIKeys($kuduApiAuthorisationToken, $webAppName, $masterKey )
{
    $apiUrl = "https://$webAppName.azurewebsites.net/admin/host/keys?code=$masterKey"
    $result = Invoke-WebRequest $apiUrl
    return $result`
}

 
$accessToken = Get-KuduApiAuthorisationHeaderValue $resourceGroupName $webAppname

$adminCode = Get-MasterAPIKey $accessToken $webAppname
Write-Host "masterKey = " $adminCode.Masterkey
 
$result = Get-HostAPIKeys $accessToken $webAppname $adminCode.Masterkey
$keysCode =  $result.Content | ConvertFrom-Json
Write-Host "default Key = " $keysCode.Keys[0].Value
```

**Retrieve Azure Function Keys in ARM template (output file)**

```
"outputs": {
    "FunctionAppName": {
        "type": "string",
        "value": "[parameters('functionName')]"
    },
    "Key": {
        "type": "string",
        "value": "[listsecrets(resourceId('Microsoft.Web/sites/functions', parameters('existingFunctionAppName'), parameters('functionName')),'2015-08-01').key]"
    },        
    "Url": {
        "type": "string",
        "value": "[listsecrets(resourceId('Microsoft.Web/sites/functions', parameters('existingFunctionAppName'), parameters('functionName')),'2015-08-01').trigger_url]"
    }
```
   
