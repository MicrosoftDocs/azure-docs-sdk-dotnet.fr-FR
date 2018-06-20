---
title: Bibliothèques Azure Service Bus Relay pour .NET
description: Référence pour les bibliothèques Azure Service Bus Relay pour .NET
keywords: Azure, .NET, SDK, API, Service Bus Relay
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 1a869d5939e357c98ec417e6474f711b9ac8c466
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566160"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="8008b-104">Bibliothèques Azure Service Bus Relay pour .NET</span><span class="sxs-lookup"><span data-stu-id="8008b-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8008b-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8008b-105">Overview</span></span>

<span data-ttu-id="8008b-106">Le service Azure Relay crée des applications hybrides en offrant la possibilité d’exposer les services qui résident dans un réseau d’entreprise sur le cloud public en toute sécurité, sans avoir à ouvrir une connexion de pare-feu ni à exiger des modifications intrusives dans une infrastructure de réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8008b-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="8008b-107">Azure Relay prend en charge une grande variété de protocoles de transport et normes de services web.</span><span class="sxs-lookup"><span data-stu-id="8008b-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="8008b-108">En savoir plus sur [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span><span class="sxs-lookup"><span data-stu-id="8008b-108">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="8008b-109">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="8008b-109">Client library</span></span>

<span data-ttu-id="8008b-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8008b-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8008b-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8008b-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8008b-112">Explorer les API client</span><span class="sxs-lookup"><span data-stu-id="8008b-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="8008b-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="8008b-113">Samples</span></span>

<span data-ttu-id="8008b-114">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="8008b-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package