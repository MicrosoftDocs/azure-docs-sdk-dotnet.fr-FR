---
title: "Bibliothèques Azure Data Lake Store pour .NET"
description: "Référence pour les bibliothèques Azure Data Lake Store pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Store"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2b1c51575872b12a94eb44c7c082996bb879bcc9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="c7c8b-104">Bibliothèques Azure Data Lake Store pour .NET</span><span class="sxs-lookup"><span data-stu-id="c7c8b-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c7c8b-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c7c8b-105">Overview</span></span>

<span data-ttu-id="c7c8b-106">Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data.</span><span class="sxs-lookup"><span data-stu-id="c7c8b-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="c7c8b-107">Azure Data Lake vous permet de capturer les données de toute taille, de tout type et à toute vitesse d'ingestion dans un emplacement unique en vue d'une analyse opérationnelle et exploratoire.</span><span class="sxs-lookup"><span data-stu-id="c7c8b-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="c7c8b-108">Pour en savoir plus, consultez [Vue d’ensemble d’Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="c7c8b-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="c7c8b-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="c7c8b-109">Management library</span></span>

<span data-ttu-id="c7c8b-110">Utilisez la bibliothèque de gestion pour vous connecter à vos référentiels de données volumineuses et les gérer.</span><span class="sxs-lookup"><span data-stu-id="c7c8b-110">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="c7c8b-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c7c8b-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c7c8b-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7c8b-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a><span data-ttu-id="c7c8b-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="c7c8b-113">Code Example</span></span>

<span data-ttu-id="c7c8b-114">Cet exemple s’authentifie auprès d’un compte analytics et d’un magasin et crée les clients nécessaires pour la gestion.</span><span class="sxs-lookup"><span data-stu-id="c7c8b-114">This example authenticates to an analytics account and store and creates the clients necessary for management.</span></span>

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7c8b-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="c7c8b-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="c7c8b-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="c7c8b-116">Samples</span></span>

* [<span data-ttu-id="c7c8b-117">Exemple de Client Azure Data Lake .NET</span><span class="sxs-lookup"><span data-stu-id="c7c8b-117">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="c7c8b-118">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="c7c8b-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
