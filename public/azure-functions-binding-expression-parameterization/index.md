# Azure Functions Binding Expression Parameterization


[Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview) is an event driven, serverless computing service provided by Microsoft Azure Cloud platform. Azure Functions allows developers to deploy code connecting to data sources or messaging solutions thus enabling easier implementation of event driven processing of messages. Azure Functions, like rest of serverless computing, is designed to accelerate and simplify application development by removing the responsibility of infrastructure management.

Azure Functions uses concept of [bindings](https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings) as a way of declaratively connecting another resource to the function. Bindings may be connected as input bindings, output bindings, or both, and can be used as triggers for message and event processing.

Few commonly used Azure Function bindings are:

Blog Storage
Cosmos DB
Event Grid
Event Hubs
If implementing in JavaScript, bindings are specified in function.json as shown in below example:

```json
{
    "type": "eventHubTrigger",
    "name": "eventHubMessages",
    "direction": "in",
    "eventHubName": "defaulthub",
    "connection": "eventsamples_defaultReadPolicy_EVENTHUB"
}
```

Here, `eventsamples_defaultReadPolicy_EVENTHUB` refers to the Azure Function Application Setting that specifies the Event Hub Connection strings. Similar binding definitions are available for other supported services.

It is possible to specify few other parameters in the binding definition. For example, the above trigger binding for Event Hubs can include additional parameters for cardinality or the consumer group:

```json
{
    ...
    "cardinality": "many",
    "consumerGroup": "default"
}
```

One issue arises if we wish to re-use the same function with only a single change that is the target consumer group. Ideally we would want to set the consumer group in an environmental variable in the application settings. How does one load in a consumer group from an Application setting?

Similar problem can occur with other binding sources. For example, `path` setting for Blob storage, `databaseName` or `collectionName` for Cosmos DB.

A nice trick I recently found was to use binding expressions. In your function.json file, you can specify consumer group name inside % symbol:

```json
{
    ...
    "consumerGroup": "%customGroupName%"
    ...
}
```

Then add an Application setting with corresponding name (`customGroupName` in this case).

Here are couple of screenshots of the function settings and application settings with these updates.

Consumer group will then be resolved to the value in Application Settings at startup.

Same method can be used for binding for other services and it works for trigger, input, and output bindings.

Hope this is helpful!
