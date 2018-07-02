---
title: Bibliothèques Azure Event Grid pour .NET
description: Référence pour les bibliothèques Azure Event Grid pour .NET
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: 922e1a49a2b864d8cd408a8383d7cda27c7f89c2
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065299"
---
# <a name="azure-event-grid-libraries-for-net"></a>Bibliothèques Azure Event Grid pour .NET

Créez des applications pilotées par des événements, qui écoutent et réagissent aux événements venant des services Azure et de sources personnalisées à l’aide d’une gestion simple des événements basés sur HTTP avec Azure Event Grid.

[En savoir plus](/azure/event-grid/overview) sur Azure Event Grid et la prise en main avec le [didacticiel des événements de stockage d’objets Blob Azure](/azure/storage/blobs/storage-blob-event-quickstart-powershell). 

## <a name="publish-sdk"></a>Kit de développement logiciel de publication

Créez des événements, authentifiez-vous et faites des publications dans des rubriques à l’aide du kit de développement logiciel de publication de Azure Event Grid.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="sample-usage"></a>Exemple d’utilisation

Le code suivant s’authentifie auprès d’Azure et publie un `List` d’événements `EventGridEvent` d’un type personnalisé (dans cet exemple, `Contoso.Items.ItemsReceivedEvent` ) sur une rubrique. La clé de la rubrique et l’adresse du point de terminaison utilisés dans cet exemple peuvent être récupérées à partir d’Azure PowerShell :

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

```csharp
string topicEndpoint = "https://<topic-name>.<region>-1.eventgrid.azure.net/api/events";
string topicKey = "<topic-key>";
string topicHostname = new Uri(topicEndpoint).Host;

TopicCredentials topicCredentials = new TopicCredentials(topicKey);
EventGridClient client = new EventGridClient(topicCredentials);

client.PublishEventsAsync(topicHostname, GetEventsList()).GetAwaiter().GetResult();
Console.Write("Published events to Event Grid.");

static IList<EventGridEvent> GetEventsList()
{
    List<EventGridEvent> eventsList = new List<EventGridEvent>();
    for (int i = 0; i < 1; i++)
    {
        eventsList.Add(new EventGridEvent()
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Contoso.Items.ItemReceivedEvent",
            Data = new ContosoItemReceivedEventData()
            {
                ItemUri = "ContosoSuperItemUri"
            },

            EventTime = DateTime.Now,
            Subject = "Door1",
            DataVersion = "2.0"
        });
    }
    return eventsList;
}
```

Cet extrait de code gère les événements publiés lors de la création d’un nouvel objet blob dans [Azure Storage](/azure/storage/blobs/storage-blob-event-overview).

```csharp
string response = string.Empty;
const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

string requestContent = await req.Content.ReadAsStringAsync();
EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

foreach (EventGridEvent eventGridEvent in eventGridEvents)
{
    JObject dataObject = eventGridEvent.Data as JObject;

    // Deserialize the event data into the appropriate type based on event type 
    if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
        log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");

        // Do any additional validation (as required) and then return back the below response
        var responseData = new SubscriptionValidationResponseData();
        responseData.ValidationResponse = eventData.ValidationCode;
        return req.CreateResponse(HttpStatusCode.OK, responseData);
    }

    else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
    }
}
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>Kit de développement logiciel (SDK) de gestion

Créez, mettez à jour et supprimez des instances, des rubriques et des abonnements Event Grid avec le kit de développement logiciel de gestion.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].


#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>En savoir plus

- [Recevoir des événements avec le kit de développement logiciel Event Grid](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
