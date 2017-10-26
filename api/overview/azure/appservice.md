---
title: "Bibliothèques Azure App Service pour .NET"
description: "Référence pour les bibliothèques Azure App Service pour .NET"
keywords: "Azure, .NET, SDK, API, applications web, service d’applications, mobile, asp.net"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 9f54fb6aca934f07c6ae23a4ae40dc29fa48ec8b
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="4605c-104">Bibliothèques Azure App Service pour .NET</span><span class="sxs-lookup"><span data-stu-id="4605c-104">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4605c-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4605c-105">Overview</span></span>

<span data-ttu-id="4605c-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) permet de déployer et mettre à l’échelle des sites web, des applications web, des services et des API REST.</span><span class="sxs-lookup"><span data-stu-id="4605c-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="4605c-107">API de gestion</span><span class="sxs-lookup"><span data-stu-id="4605c-107">Management API</span></span>

<span data-ttu-id="4605c-108">Déployez, gérez et mettez à l’échelle des éléments hébergés dans Azure App Service avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="4605c-108">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="4605c-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="4605c-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4605c-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4605c-110">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="4605c-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="4605c-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="4605c-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="4605c-112">Code Example</span></span>

<span data-ttu-id="4605c-113">Créez une application web.</span><span class="sxs-lookup"><span data-stu-id="4605c-113">Create a new web app.</span></span>

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
> [<span data-ttu-id="4605c-114">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="4605c-114">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="4605c-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="4605c-115">Samples</span></span>

* [<span data-ttu-id="4605c-116">Gérer vos applications web avec le Kit de développement logiciel (SDK) .NET pour Azure</span><span class="sxs-lookup"><span data-stu-id="4605c-116">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="4605c-117">Exemple ASP.NET pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4605c-117">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="4605c-118">Afficher la [liste complète](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=app%20service) des exemples Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4605c-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package