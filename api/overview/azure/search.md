---
title: Bibliothèques Recherche Azure pour .NET
description: Référence pour les bibliothèques Recherche Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Recherche
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: search
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 5062d444b859711d7f87a0ecbd65e6b204c04b16
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065279"
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="30b3e-104">Bibliothèques Recherche Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="30b3e-104">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="30b3e-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="30b3e-105">Overview</span></span>

<span data-ttu-id="30b3e-106">[Recherche Azure](https://docs.microsoft.com/azure/search/search-what-is-azure-search) est un service de recherche cloud entièrement géré qui fournit une expérience de recherche riche sur les données dans les applications web, mobiles et d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="30b3e-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="30b3e-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="30b3e-107">Client library</span></span>

<span data-ttu-id="30b3e-108">Utilisez la bibliothèque cliente Recherche Azure pour accéder à l’indexation et aux opérations de recherche, puis pour les exécuter sur un service de recherche, un index, des documents ou un autre objet.</span><span class="sxs-lookup"><span data-stu-id="30b3e-108">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="30b3e-109">Pour une présentation pas à pas, consultez [Comment utiliser Azure Search à partir d'une application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="30b3e-109">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="30b3e-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="30b3e-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="30b3e-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30b3e-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="30b3e-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="30b3e-112">Code Example</span></span>

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="30b3e-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="30b3e-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="30b3e-114">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="30b3e-114">Management library</span></span>

<span data-ttu-id="30b3e-115">Utilisez la bibliothèque de gestion Recherche Azure pour approvisionner un service, gérer les clés API et ajuster les ressources.</span><span class="sxs-lookup"><span data-stu-id="30b3e-115">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="30b3e-116">Gestion du service possède une dépendance sur Azure Resource Manager pour l’identification de l’abonné et du client.</span><span class="sxs-lookup"><span data-stu-id="30b3e-116">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="30b3e-117">En règle générale, l’authentification et l’inscription de l’application avec Azure Active Directory est également nécessaire pour prendre en charge le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="30b3e-117">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="30b3e-118">Pour vous familiariser avec l’approvisionnement du service Recherche Azure, consultez [Comment utiliser l’API REST de gestion](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span><span class="sxs-lookup"><span data-stu-id="30b3e-118">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="30b3e-119">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="30b3e-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="30b3e-120">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30b3e-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="30b3e-121">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="30b3e-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="30b3e-122">Exemples</span><span class="sxs-lookup"><span data-stu-id="30b3e-122">Samples</span></span>

 + [<span data-ttu-id="30b3e-123">Exemples Azure / recherche-dotnet-mise-en-route</span><span class="sxs-lookup"><span data-stu-id="30b3e-123">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="30b3e-124">Exemples Azure / recherche-dotnet-api-de-gestion</span><span class="sxs-lookup"><span data-stu-id="30b3e-124">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="30b3e-125">Rechercher d’autres exemples de recherche dans le [référentiel d’exemples Azure](https://github.com/Azure-Samples/) sur Github.</span><span class="sxs-lookup"><span data-stu-id="30b3e-125">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
