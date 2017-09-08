---
title: "Bibliothèques Azure Event Hubs pour .NET"
description: "Référence pour les bibliothèques Azure Event Hubs pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Hubs d’événements"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 1dca44ed716e387d531661093d4c7cfc7780964b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="dcde5-104">Bibliothèques Azure Event Hubs pour .NET</span><span class="sxs-lookup"><span data-stu-id="dcde5-104">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="dcde5-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dcde5-105">Overview</span></span>

<span data-ttu-id="dcde5-106">Azure Event Hubs est une plateforme de diffusion des données hautement évolutives en continu et un service d’ingestion d’événements.</span><span class="sxs-lookup"><span data-stu-id="dcde5-106">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="dcde5-107">Pour en savoir plus sur Azure Event Hubs, consultez l’article [Qu’est-ce que Event Hubs ?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="dcde5-107">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="dcde5-108">Pour commencer, consultez le [Guide de programmation de Hubs d'événements](/azure/event-hubs/event-hubs-programming-guide).</span><span class="sxs-lookup"><span data-stu-id="dcde5-108">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="dcde5-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="dcde5-109">Client library</span></span>

<span data-ttu-id="dcde5-110">Le client Hubs d'événements permet d’envoyer et recevoir des messages vers et depuis les Hubs d’événements.</span><span class="sxs-lookup"><span data-stu-id="dcde5-110">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="dcde5-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="dcde5-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dcde5-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcde5-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="dcde5-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="dcde5-113">Code Example</span></span>

<span data-ttu-id="dcde5-114">Le code suivant crée un client de Hubs d'événements et envoie un message vers le hub.</span><span class="sxs-lookup"><span data-stu-id="dcde5-114">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

```csharp
EventHubsConnectionStringBuilder connectionStringBuilder = new EventHubsConnectionStringBuilder(eventHubConnectionString)
{
    EntityPath = eventHubEntityPath
};

EventHubClient eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
string message = $"Message {i}";
Console.WriteLine($"Sending message: {message}");
await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcde5-115">Explorer les API client</span><span class="sxs-lookup"><span data-stu-id="dcde5-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="dcde5-116">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="dcde5-116">Management library</span></span>

<span data-ttu-id="dcde5-117">Utilisez la bibliothèque de gestion de Hubs d'événements pour créer, mettre à jour et supprimer des hubs et des groupes de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="dcde5-117">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="dcde5-118">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="dcde5-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dcde5-119">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dcde5-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="dcde5-120">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="dcde5-120">Code Example</span></span>

<span data-ttu-id="dcde5-121">Le code suivant crée un nouveau hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="dcde5-121">The following code creates a new event hub.</span></span>

```csharp
TokenCredentials creds = new TokenCredentials(token);
EventHubManagementClient ehClient = new EventHubManagementClient(creds)
{
    SubscriptionId = subscriptionId
};

EventHubCreateOrUpdateParameters ehParams = new EventHubCreateOrUpdateParameters()
{
    Location = location
};

Console.WriteLine("Creating Event Hub...");
await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
Console.WriteLine("Created Event Hub successfully.");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcde5-122">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="dcde5-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="dcde5-123">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="dcde5-123">Tutorials</span></span>

* [<span data-ttu-id="dcde5-124">Envoyer des événements vers Azure Event Hubs à l’aide de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dcde5-124">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="dcde5-125">Recevoir des événements provenant d’Azure Event Hubs à l’aide de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dcde5-125">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="dcde5-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="dcde5-126">Samples</span></span>

* [<span data-ttu-id="dcde5-127">Exemples Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="dcde5-127">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="dcde5-128">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="dcde5-128">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
