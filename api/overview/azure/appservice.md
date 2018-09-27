---
title: Bibliothèques Azure App Service pour .NET
description: Référence pour les bibliothèques Azure App Service pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: app-service
ms.openlocfilehash: 82f8eccfafd2f7b1cf1df1ce0f40212509ccddd3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189992"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="07bff-103">Bibliothèques Azure App Service pour .NET</span><span class="sxs-lookup"><span data-stu-id="07bff-103">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="07bff-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="07bff-104">Overview</span></span>

<span data-ttu-id="07bff-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) permet de déployer et mettre à l’échelle des sites web, des applications web, des services et des API REST.</span><span class="sxs-lookup"><span data-stu-id="07bff-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="07bff-106">API de gestion</span><span class="sxs-lookup"><span data-stu-id="07bff-106">Management API</span></span>

<span data-ttu-id="07bff-107">Déployez, gérez et mettez à l’échelle des éléments hébergés dans Azure App Service avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="07bff-107">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="07bff-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="07bff-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="07bff-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07bff-109">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="07bff-110">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="07bff-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="07bff-111">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="07bff-111">Code Example</span></span>

<span data-ttu-id="07bff-112">Créez une application web.</span><span class="sxs-lookup"><span data-stu-id="07bff-112">Create a new web app.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="07bff-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="07bff-113">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="07bff-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="07bff-114">Samples</span></span>

* [<span data-ttu-id="07bff-115">Gérer vos applications web avec le Kit de développement logiciel (SDK) .NET pour Azure</span><span class="sxs-lookup"><span data-stu-id="07bff-115">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="07bff-116">Exemple ASP.NET pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="07bff-116">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="07bff-117">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) des exemples Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="07bff-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package