---
title: Bibliothèques Azure Service Bus pour .NET
description: Référence pour les bibliothèques Azure Service Bus pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Service Bus
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 5ebd659121019c74ad607dc2a553f7e305a34021
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065469"
---
# <a name="azure-service-bus-libraries-for-net"></a>Bibliothèques Azure Service Bus pour .NET

## <a name="overview"></a>Vue d'ensemble

[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) est une infrastructure de messagerie située entre des applications pour leur permettre d'échanger des messages. L'objectif est d'améliorer la mise à l'échelle et la résilience.

## <a name="client-library"></a>Bibliothèque cliente

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio.

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a>Exemple de code

Cet exemple envoie un message à une file d’attente Service Bus.

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a>Exemple de code

Cet exemple crée une file d’attente Service Bus avec une taille maximale de 1 024 Mo.

```csharp
// using Microsoft.Azure.Management.ServiceBus.Fluent;
// using Microsoft.Azure.Management.ServiceBus.Fluent.Models;

using (ServiceBusManagementClient client = new ServiceBusManagementClient(credentials))
{
    client.SubscriptionId = subscriptionId;
    QueueInner parameters = new QueueInner
    {
        MaxSizeInMegabytes = 1024
    };
    await client.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, queueName, parameters);
}
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a>Exemples

- [Fonctions de base de la file d’attente Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [Fonctionnalités avancées de la file d’attente Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [Fonctions d’abonnement/de publication de base Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [Fonctionnalités avancées d’abonnement/de publication de base Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [Service Bus avec l’autorisation par revendications - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?term=service+bus) des exemples Azure Service Bus.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
