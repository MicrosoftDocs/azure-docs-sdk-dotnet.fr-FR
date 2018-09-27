---
title: Bibliothèques de Cache Redis Azure pour .NET
description: Référence pour les bibliothèques de Cache Redis Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: redis-cache
ms.openlocfilehash: cc043bbc6ea5915f7b6c2265b606210efb72d9d0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190522"
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="13646-103">Bibliothèques de Cache Redis Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="13646-103">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="13646-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="13646-104">Overview</span></span>

<span data-ttu-id="13646-105">Cache Redis Azure est un cache de données sécurisé et un répartiteur de messagerie qui permet aux applications d’accéder aux données via un débit élevé et une faible latence.</span><span class="sxs-lookup"><span data-stu-id="13646-105">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="13646-106">Pour plus d'informations, consultez [Utilisation de Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="13646-106">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="13646-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="13646-107">Client library</span></span>

<span data-ttu-id="13646-108">Cache Redis Azure est compatible avec n’importe quelle API de client Redis, y compris `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="13646-108">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="13646-109">Installez le [package NuGet](https://www.nuget.org/packages/StackExchange.Redis) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="13646-109">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="13646-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13646-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="13646-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="13646-111">Example</span></span>

<span data-ttu-id="13646-112">Cet exemple se connecte à une instance de la base de données de Cache Redis, ajoute des chaînes dans le cache par nom, puis les récupère à nouveau.</span><span class="sxs-lookup"><span data-stu-id="13646-112">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="13646-113">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="13646-113">Management library</span></span>

<span data-ttu-id="13646-114">La bibliothèque de gestion de Cache Redis vous permet de gérer les ressources et les clés d’accès de Cache Redis .</span><span class="sxs-lookup"><span data-stu-id="13646-114">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="13646-115">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="13646-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="13646-116">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13646-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="13646-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="13646-117">Example</span></span>

<span data-ttu-id="13646-118">Cet exemple crée un Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="13646-118">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="13646-119">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="13646-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="13646-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="13646-120">Samples</span></span>

* [<span data-ttu-id="13646-121">Prise en main de Redis : Gérer Redis - dans .NET</span><span class="sxs-lookup"><span data-stu-id="13646-121">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
