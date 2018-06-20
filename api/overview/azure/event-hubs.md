---
title: Bibliothèques Azure Event Hubs pour .NET
description: Référence pour les bibliothèques Azure Event Hubs pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Hubs d’événements
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2ec234959ffc46d2399d1c763e05f173a311b0d2
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487292"
---
# <a name="azure-event-hubs-libraries-for-net"></a>Bibliothèques Azure Event Hubs pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Event Hubs est une plateforme de diffusion des données hautement évolutives en continu et un service d’ingestion d’événements.

Pour en savoir plus sur Azure Event Hubs, consultez l’article [Qu’est-ce que Event Hubs ?](/azure/event-hubs/event-hubs-what-is-event-hubs).  Pour commencer, consultez le [Guide de programmation de Hubs d'événements](/azure/event-hubs/event-hubs-programming-guide).

## <a name="client-library"></a>Bibliothèque cliente

Le client Hubs d'événements permet d’envoyer et recevoir des messages vers et depuis les Hubs d’événements.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a>Exemple de code

Le code suivant crée un client de Hubs d'événements et envoie un message vers le hub.

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
> [Explorer les API client](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion de Hubs d'événements pour créer, mettre à jour et supprimer des hubs et des groupes de consommateurs.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a>Exemple de code

Le code suivant crée un nouveau hub d’événements.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a>Didacticiels

* [Envoyer des événements vers Azure Event Hubs à l’aide de .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [Recevoir des événements provenant d’Azure Event Hubs à l’aide de .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a>Exemples

* [Exemples Azure Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
