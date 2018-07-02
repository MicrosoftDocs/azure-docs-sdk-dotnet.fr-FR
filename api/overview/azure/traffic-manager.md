---
title: Bibliothèques Azure Traffic Manager pour .NET
description: Référence pour les bibliothèques Azure Traffic Manager pour .NET
keywords: Azure, .NET, SDK, API, Traffic Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 05856cbe48a5cf5f0c9ebf43609a029928f490f9
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065869"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="30d68-104">Bibliothèques Azure Traffic Manager pour .NET</span><span class="sxs-lookup"><span data-stu-id="30d68-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="30d68-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="30d68-105">Overview</span></span>

<span data-ttu-id="30d68-106">Microsoft Azure Traffic Manager vous permet de contrôler la répartition du trafic utilisateur pour les points de terminaison de service dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="30d68-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="30d68-107">Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud.</span><span class="sxs-lookup"><span data-stu-id="30d68-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="30d68-108">Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.</span><span class="sxs-lookup"><span data-stu-id="30d68-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="30d68-109">En savoir plus sur [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="30d68-109">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="30d68-110">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="30d68-110">Management library</span></span>

<span data-ttu-id="30d68-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="30d68-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="30d68-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30d68-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="30d68-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="30d68-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="30d68-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="30d68-114">Samples</span></span>

<span data-ttu-id="30d68-115">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="30d68-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package