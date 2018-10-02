---
title: Bibliothèques Azure Event Grid pour .NET
description: Référence pour les bibliothèques Azure Event Grid pour .NET
ms.date: 04/16/2018
ms.topic: reference
ms.service: event-grid
ms.openlocfilehash: 5b19f8aa8b28b3e4aef528da051b6e7d177f1a2f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190392"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="5a4ff-103">Bibliothèques Azure Event Grid pour .NET</span><span class="sxs-lookup"><span data-stu-id="5a4ff-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="5a4ff-104">Créez des applications pilotées par des événements, qui écoutent et réagissent aux événements venant des services Azure et de sources personnalisées à l’aide d’une gestion simple des événements basés sur HTTP avec Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="5a4ff-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="5a4ff-105">[En savoir plus](/azure/event-grid/overview) sur Azure Event Grid et la prise en main avec le [didacticiel des événements de stockage d’objets Blob Azure](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span><span class="sxs-lookup"><span data-stu-id="5a4ff-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="5a4ff-106">Kit de développement logiciel (SDK) client</span><span class="sxs-lookup"><span data-stu-id="5a4ff-106">Client SDK</span></span>

<span data-ttu-id="5a4ff-107">Créez des événements, authentifiez-vous et faites des publications dans des rubriques à l’aide du kit de développement logiciel client d’Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="5a4ff-107">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="5a4ff-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5a4ff-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5a4ff-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a4ff-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="5a4ff-110">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="5a4ff-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="publish-events"></a><span data-ttu-id="5a4ff-111">Publier des événements</span><span class="sxs-lookup"><span data-stu-id="5a4ff-111">Publish events</span></span>

<span data-ttu-id="5a4ff-112">Le code suivant s’authentifie auprès d’Azure et publie un `List` d’événements `EventGridEvent` d’un type personnalisé (dans cet exemple, `Contoso.Items.ItemsReceivedEvent` ) sur une rubrique.</span><span class="sxs-lookup"><span data-stu-id="5a4ff-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="5a4ff-113">La clé de la rubrique et l’adresse du point de terminaison utilisés dans cet exemple peuvent être récupérées à partir d’Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="5a4ff-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

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

### <a name="consume-events"></a><span data-ttu-id="5a4ff-114">Consommer des événements</span><span class="sxs-lookup"><span data-stu-id="5a4ff-114">Consume events</span></span>

<span data-ttu-id="5a4ff-115">Cet extrait de code consomme des événements, y compris un événement personnalisé `Contoso.Items.ItemsReceived`, ainsi que des événements déclenchés à partir d’autres services Azure, tels que Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="5a4ff-115">This snippet consumes events, including a custom event `Contoso.Items.ItemsReceived` as well as events triggered from other Azure services, such as Blob Storage.</span></span>

```csharp
string response = string.Empty;
string requestContent = await req.Content.ReadAsStringAsync();

EventGridSubscriber eventGridSubscriber = new EventGridSubscriber();

// Optionally add one or more custom event type mappings
eventGridSubscriber.AddOrUpdateCustomEventMapping("Contoso.Items.ItemReceived", typeof(ContosoItemReceivedEventData));

var events = eventGridSubscriber.DeserializeEventGridEvents(requestContent);            
 
foreach (EventGridEvent receivedEvent in events)
{
    if (receivedEvent.Data is SubscriptionValidationEventData)
    {
        SubscriptionValidationEventData eventData = (SubscriptionValidationEventData)receivedEvent.Data;
        log.Info($"Got SubscriptionValidation event data, validationCode: {eventData.ValidationCode},  validationUrl: {eventData.ValidationUrl}, topic: {eventGridEvent.Topic}");
        // Handle subscription validation
    }
    else if (receivedEvent.Data is StorageBlobCreatedEventData)
    {
        StorageBlobCreatedEventData eventData = (StorageBlobCreatedEventData)receivedEvent.Data;
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        // Handle StorageBlobCreatedEventData
    }
    else if (receivedEvent.Data is ContosoItemReceivedEventData)
    {
        ContosoItemReceivedEventData eventData = (ContosoItemReceivedEventData)receivedEvent.Data;
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a4ff-116">Explorer les API de publication</span><span class="sxs-lookup"><span data-stu-id="5a4ff-116">Explore the publishing APIs</span></span>](/dotnet/api/overview/azure/eventgrid/publish)

## <a name="management-sdk"></a><span data-ttu-id="5a4ff-117">Kit de développement logiciel (SDK) de gestion</span><span class="sxs-lookup"><span data-stu-id="5a4ff-117">Management SDK</span></span>

<span data-ttu-id="5a4ff-118">Créez, mettez à jour et supprimez des instances, des rubriques et des abonnements Event Grid avec le kit de développement logiciel de gestion.</span><span class="sxs-lookup"><span data-stu-id="5a4ff-118">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="5a4ff-119">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5a4ff-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5a4ff-120">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a4ff-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="5a4ff-121">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="5a4ff-121">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a4ff-122">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="5a4ff-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="5a4ff-123">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="5a4ff-123">Learn more</span></span>

- [<span data-ttu-id="5a4ff-124">Recevoir des événements avec le kit de développement logiciel Event Grid</span><span class="sxs-lookup"><span data-stu-id="5a4ff-124">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
