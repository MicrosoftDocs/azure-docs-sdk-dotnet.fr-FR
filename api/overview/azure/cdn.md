---
title: Bibliothèques Azure CDN pour .NET
description: Référence pour les bibliothèques Azure CDN pour .NET
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: cdn
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4e5b56ca7e316f3a53d8c6d37fdd90c5d7130e1e
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065819"
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="0e916-104">Bibliothèques Azure CDN pour .NET</span><span class="sxs-lookup"><span data-stu-id="0e916-104">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0e916-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0e916-105">Overview</span></span>

<span data-ttu-id="0e916-106">Le réseau de distribution de contenu (CDN) Azure met en cache le contenu web statique à des emplacements stratégiques afin de fournir un débit maximal pour la distribution de contenu aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0e916-106">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="0e916-107">Le CDN offre aux développeurs une solution globale pour la distribution de contenu haut débit en mettant en cache le contenu sur des nœuds physiques dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="0e916-107">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="0e916-108">Pour en savoir plus sur Azure CDN, consultez l’article [Vue d'ensemble du réseau de distribution de contenu](https://docs.microsoft.com/azure/cdn/cdn-overview).</span><span class="sxs-lookup"><span data-stu-id="0e916-108">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="0e916-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="0e916-109">Management library</span></span>

<span data-ttu-id="0e916-110">Vous pouvez utiliser la bibliothèque Azure CDN pour .NET pour automatiser la création et la gestion des points de terminaison et profils CDN.</span><span class="sxs-lookup"><span data-stu-id="0e916-110">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="0e916-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0e916-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0e916-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e916-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="0e916-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="0e916-113">Example</span></span>

<span data-ttu-id="0e916-114">Cet exemple crée un nouveau profil CDN avec un nouveau point de terminaison pointé vers `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="0e916-114">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e916-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="0e916-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="0e916-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="0e916-116">Samples</span></span>

* [<span data-ttu-id="0e916-117">Prise en main de CDN - Gérer CDN - dans .NET</span><span class="sxs-lookup"><span data-stu-id="0e916-117">Getting started with CDN - Manage CDN - in .NET</span></span>](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
