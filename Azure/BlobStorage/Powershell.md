# Azure blob storage Powershell Examples

## Upload file to blob storage
```
$context = New-AzureStorageContext -ConnectionString "<connection string>"
Set-AzureStorageBlobContent -File "<file name/path>" -Container "<container name>" -Context $context
```