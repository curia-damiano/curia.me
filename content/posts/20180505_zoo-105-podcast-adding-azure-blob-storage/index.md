---
title: "Zoo 105 Podcast: adding Azure Blob storage"
slug: "zoo-105-podcast-adding-azure-blob-storage"
draft: false
date: "2018-05-05T18:49:00Z"
categories:
  - "Software Development"
tags:
  - "Azure"
author: "Curia Damiano"
image: "img/zoo105.jpg"
---

In this last step of my application, I wanted to save the podcast episodes (the real mp3 files) in an Azure Blob storage. I didn't want to slow down my optimized Azure Function, so I decided to download the mp3 files in a separate function.

How to invoke this second function? The first idea was to invoke it automatically when saving in CosmosDB (there is a CosmosDB trigger), but this solution is not fault resistant (or at least: you need to implement fault resistance yourself).

Azure provides fault resistance out-of-the-box with queues, so I chose to use them. Azure storage is already there when creating a Function, so I needed only to create a function to create the queue (if not existing):

```csharp
public static async Task<CloudQueue> GetAzureQueueAsync(IConfigurationRoot config)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(config["AzureWebJobsStorage"]);
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    CloudQueue queue = queueClient.GetQueueReference(queueName);
    await queue.CreateIfNotExistsAsync();
    return queue;
}
```

Once I have a queue, it's easy to add items:

```csharp
public static async Task EnqueueItemAsync(CloudQueue queue, Podcast2Download episode)
{
    string serializedObj = JsonConvert.SerializeObject(episode);
    CloudQueueMessage message = new CloudQueueMessage(serializedObj);
    await queue.AddMessageAsync(message);
}
```

Item retrieval and eventual re-enqueuing in case of errors is automatically managed by Azure; all you need is to write a Function that has the queue trigger:

```csharp
[FunctionName("Download2Blob")]
public static async Task Run([QueueTrigger("podcast2download", Connection = "AzureWebJobsStorage")]
    string myQueueItem, ILogger logger, Microsoft.Azure.WebJobs.ExecutionContext context)
{
    logger.LogInformation($"C# Queue trigger function processed: {myQueueItem}");

    ...

    Podcast2Download episode2download = AzureQueueHelper.DeserializeItem(myQueueItem);

    ...
}
```

**UPDATE**: as described [here](https://github.com/Azure/app-service-announcements/issues/129), in Azure Functions v2 the QueueTriggerAttribute requires the NuGet package [Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage).

Finally, after having downloaded the file, to save it in an Azure Blob, you need to get a container:

```csharp
public static CloudBlobContainer GetBlobContainer(IConfigurationRoot config)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(config["AzureWebJobsStorage"]);
    CloudBlobClient cloudBlobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer cloudBlobContainer = cloudBlobClient.GetContainerReference(blobContainerName);
    return cloudBlobContainer;
}
```

With the container, you can call multiple methods to manage its files. In my case, I wanted to only upload new files:

```csharp
public static async Task<long> StoreFileAsync(CloudBlobContainer cloudBlobContainer, DateTime dateUtc, string fileName, Stream stream)
{
    // If the container does't exist, create it
    if (!await cloudBlobContainer.ExistsAsync())
        try { await cloudBlobContainer.CreateAsync(); } catch { }

    string pathFileName = ...;
    CloudBlockBlob cloudBlockBlob = cloudBlobContainer.GetBlockBlobReference(pathFileName);
    await cloudBlockBlob.UploadFromStreamAsync(stream);

    return stream.Position;
}
```

The source code for this step is available in the dedicated [GitHub repository](https://github.com/curia-damiano/Zoo105Podcast), under the tag [3.AzureBlobStorage](https://github.com/curia-damiano/Zoo105Podcast/releases/tag/3.AzureBlobStorage).
