---
title: "Bibliothèques de Cache Redis Azure pour .NET"
description: "Référence pour les bibliothèques de Cache Redis Azure pour .NET"
keywords: Azure, .NET, SDK, API, Redis Cache
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: redis-cache
ms.openlocfilehash: 2316a179712b143b7e099f4592035c489d270bc3
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="9d77f-104">Bibliothèques de Cache Redis Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="9d77f-104">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9d77f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9d77f-105">Overview</span></span>

<span data-ttu-id="9d77f-106">Cache Redis Azure est un cache de données sécurisé et un répartiteur de messagerie qui permet aux applications d’accéder aux données via un débit élevé et une faible latence.</span><span class="sxs-lookup"><span data-stu-id="9d77f-106">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="9d77f-107">Pour plus d'informations, consultez [Utilisation de Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="9d77f-107">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="9d77f-108">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="9d77f-108">Client library</span></span>

<span data-ttu-id="9d77f-109">Cache Redis Azure est compatible avec n’importe quelle API de client Redis, y compris `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="9d77f-109">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="9d77f-110">Installez le [package NuGet](https://www.nuget.org/packages/StackExchange.Redis) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9d77f-110">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9d77f-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d77f-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="9d77f-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d77f-112">Example</span></span>

<span data-ttu-id="9d77f-113">Cet exemple se connecte à une instance de la base de données de Cache Redis, ajoute des chaînes dans le cache par nom, puis les récupère à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9d77f-113">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

```csharp
/* Include this "using" directive.
using StackExchange.Redis;
*/

ConnectionMultiplexer connection = 
    ConnectionMultiplexer.Connect("contoso.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    IDatabase cache = connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

## <a name="management-library"></a><span data-ttu-id="9d77f-114">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="9d77f-114">Management library</span></span>

<span data-ttu-id="9d77f-115">La bibliothèque de gestion de Cache Redis vous permet de gérer les ressources et les clés d’accès de Cache Redis .</span><span class="sxs-lookup"><span data-stu-id="9d77f-115">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="9d77f-116">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9d77f-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9d77f-117">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d77f-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="9d77f-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="9d77f-118">Example</span></span>

<span data-ttu-id="9d77f-119">Cet exemple crée un Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="9d77f-119">This example creates a new Redis Cache.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.Redis.Fluent;
*/

IRedisCache redisCache1 = azure.RedisCaches.Define("RedisCacheName")
    .WithRegion(Region.USCentral)
    .WithNewResourceGroup("ResourceGroupName")
    .WithBasicSku()
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d77f-120">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="9d77f-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="9d77f-121">Exemples</span><span class="sxs-lookup"><span data-stu-id="9d77f-121">Samples</span></span>

* [<span data-ttu-id="9d77f-122">Prise en main de Redis : Gérer Redis - dans .NET</span><span class="sxs-lookup"><span data-stu-id="9d77f-122">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
