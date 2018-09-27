---
title: Bibliothèques Azure Service Bus pour .NET
description: Référence pour les bibliothèques Azure Service Bus pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 506be9a669a2418f2437271d128a963e351442e7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190872"
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="99a39-103">Bibliothèques Azure Service Bus pour .NET</span><span class="sxs-lookup"><span data-stu-id="99a39-103">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="99a39-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="99a39-104">Overview</span></span>

<span data-ttu-id="99a39-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) est une infrastructure de messagerie située entre des applications pour leur permettre d'échanger des messages. L'objectif est d'améliorer la mise à l'échelle et la résilience.</span><span class="sxs-lookup"><span data-stu-id="99a39-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="99a39-106">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="99a39-106">Client library</span></span>

<span data-ttu-id="99a39-107">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99a39-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="99a39-108">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99a39-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="99a39-109">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="99a39-109">Code Example</span></span>

<span data-ttu-id="99a39-110">Cet exemple envoie un message à une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="99a39-110">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="99a39-111">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="99a39-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="99a39-112">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="99a39-112">Management library</span></span>

<span data-ttu-id="99a39-113">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="99a39-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="99a39-114">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99a39-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="99a39-115">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="99a39-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="99a39-116">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="99a39-116">Code Example</span></span>

<span data-ttu-id="99a39-117">Cet exemple crée une file d’attente Service Bus avec une taille maximale de 1 024 Mo.</span><span class="sxs-lookup"><span data-stu-id="99a39-117">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

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
> [<span data-ttu-id="99a39-118">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="99a39-118">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="99a39-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="99a39-119">Samples</span></span>

- [<span data-ttu-id="99a39-120">Fonctions de base de la file d’attente Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="99a39-120">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="99a39-121">Fonctionnalités avancées de la file d’attente Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="99a39-121">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="99a39-122">Fonctions d’abonnement/de publication de base Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="99a39-122">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="99a39-123">Fonctionnalités avancées d’abonnement/de publication de base Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="99a39-123">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="99a39-124">Service Bus avec l’autorisation par revendications - .Net</span><span class="sxs-lookup"><span data-stu-id="99a39-124">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="99a39-125">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?term=service+bus) des exemples Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="99a39-125">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
