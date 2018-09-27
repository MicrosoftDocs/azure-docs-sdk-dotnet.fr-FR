---
title: Bibliothèques Azure Traffic Manager pour .NET
description: Référence pour les bibliothèques Azure Traffic Manager pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: traffic-manager
ms.openlocfilehash: a75b5c566496f73475d24d62288a00c7d5775168
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190814"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="c1b32-103">Bibliothèques Azure Traffic Manager pour .NET</span><span class="sxs-lookup"><span data-stu-id="c1b32-103">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c1b32-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c1b32-104">Overview</span></span>

<span data-ttu-id="c1b32-105">Microsoft Azure Traffic Manager vous permet de contrôler la répartition du trafic utilisateur pour les points de terminaison de service dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="c1b32-105">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="c1b32-106">Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud.</span><span class="sxs-lookup"><span data-stu-id="c1b32-106">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="c1b32-107">Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.</span><span class="sxs-lookup"><span data-stu-id="c1b32-107">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="c1b32-108">En savoir plus sur [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="c1b32-108">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="c1b32-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="c1b32-109">Management library</span></span>

<span data-ttu-id="c1b32-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c1b32-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c1b32-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1b32-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1b32-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="c1b32-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="c1b32-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="c1b32-113">Samples</span></span>

<span data-ttu-id="c1b32-114">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="c1b32-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package