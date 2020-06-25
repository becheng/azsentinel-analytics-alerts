# Importing/Exporting Azure Sentinel Analytics Alert Rules

1.	Install the [AzSentinel](https://github.com/wortell/AZSentinel) module as per the repo instructions.

2.	Sign in the Azure subscription with contains the Sentinel workspace that you want to export/import the Analytics Alert Rules.
```
Connect-AzAccount -Tenant {tenantId} -Subscription {subscriptionId}
```

3.	Set the follow variables since the ps scripts require a valid auth token.
```
$context = Get-AzContext
$profile = [Microsoft.Azure.Commands.Common.Authentication.Abstractions.AzureRmProfileProvider]::Instance.Profile
$profileClient = New-Object -TypeName Microsoft.Azure.Commands.ResourceManager.Common.RMProfileClient -ArgumentList ($profile)
$token = $profileClient.AcquireAccessToken($context.Subscription.TenantId)
$authHeader = @{
  'Content-Type' = 'application/json'
  'Authorization' = 'Bearer ' + $token.AccessToken 
} 
```

4.	Run the desired ps scripts as documented in the repo.

Examples: 
```
Get-AzSentinelAlertRule -SubscriptionId {subscriptionId} -WorkspaceName {workspaceName}
```
```
Import-AzSentinelAlertRule -WorkspaceName {workspaceName} -SettingsFile "{alerts rule jsonFile}"
```
