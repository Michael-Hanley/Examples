# Examples of Azure FunctionApp Bindings

## **Triggers**

### HTTP Request Trigger
```
{
    "authLevel": "function",
    "type": "httpTrigger",
    "direction": "in",
    "name": "req"
}
```

### Timer Trigger
Uses cron syntax. [[Wiki]](https://en.wikipedia.org/wiki/Cron)
```
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

### Blob Trigger
The Blob storage trigger starts a function when a new or updated blob is detected. The blob contents are provided as input to the function.
```
{
    "name": "myBlob",
    "type": "blobTrigger",
    "direction": "in",
    "path": "samples-workitems/{name}",
    "connection":"MyStorageAccountAppSetting"
}
```

### Queue Trigger
Anytime data is added to the storage queue the function is ran. 

```
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"MyStorageConnectionAppSetting"
}
```

### Cosmos DB Trigger
Function runs anytime Cosmos DB records are modified.
```
{
    "type": "cosmosDBTrigger",
    "name": "documents",
    "direction": "in",
    "leaseCollectionName": "leases",
    "connectionStringSetting": "<connection-app-setting>",
    "databaseName": "Tasks",
    "collectionName": "Items",
    "createLeaseCollectionIfNotExists": true
}
```

## **Outputs**
### Blob
File extension can be added to file name to specify file type.
```
{
    "name": "imageSmall",
    "type": "blob",
    "path": "sample-images-sm/{filename}",
    "direction": "out",
    "connection": "MyStorageConnection"
}
```

### SendGrid
```
{
    "name": "$return",
    "type": "sendGrid",
    "direction": "out",
    "apiKey" : "MySendGridKey",
    "to": "{ToEmail}",
    "from": "{FromEmail}",
    "subject": "SendGrid output bindings"
}
```

### Queue
Creates a queue item for each item returned.
```
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionAppSetting"
}
```

### HTTP Response
```
{
    "type": "http",
    "direction": "out",
    "name": "res"
}
```

### Cosmos DB
```
{
    "name": "inputDocumentOut",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "createIfNotExists": false,
    "partitionKey": "{queueTrigger_payload_property}",
    "connectionStringSetting": "MyAccount_COSMOSDB",
    "direction": "out"
}
```

## **Inputs**
### Blob 
```
{
    "name": "myInputBlob",
    "type": "blob",
    "path": "samples-workitems/{queueTrigger}",
    "connection": "MyStorageConnectionAppSetting",
    "direction": "in"
}
```

### Cosmos DB
```    
{
    "name": "inputDocumentIn",
    "type": "cosmosDB",
    "databaseName": "MyDatabase",
    "collectionName": "MyCollection",
    "id" : "{queueTrigger_payload_property}",
    "partitionKey": "{queueTrigger_payload_property}",
    "connectionStringSetting": "MyAccount_COSMOSDB",
    "direction": "in"
}
```