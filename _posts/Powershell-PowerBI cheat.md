Install-Module -Name MicrosoftPowerBIMgmt

Get-Module PowerBIPS* -ListAvailable | Uninstall-Module -Force




Login-PowerBI

$result = Invoke-PowerBIRestMethod -Url "<ENTER URL HERE>" -Method Get
$workspaceContents = $result | ConvertFrom-Json

$firstWorspace = $worspaceContents.value[0]
$firstWorspace





New-AzResourceGroup -Name pmldockerhub -Location WestEurope