---
title: Bibliothèques de Cache Redis Azure pour .NET
description: Référence pour les bibliothèques de Cache Redis Azure pour .NET
keywords: Azure, .NET, SDK, API, Redis Cache
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: redis-cache
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 879f42aa254103239fb0dceeb25cb99a7d5e9814
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065919"
---
# <a name="azure-redis-cache-libraries-for-net"></a>Bibliothèques de Cache Redis Azure pour .NET

## <a name="overview"></a>Vue d'ensemble

Cache Redis Azure est un cache de données sécurisé et un répartiteur de messagerie qui permet aux applications d’accéder aux données via un débit élevé et une faible latence.  Pour plus d'informations, consultez [Utilisation de Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).

## <a name="client-library"></a>Bibliothèque cliente

Cache Redis Azure est compatible avec n’importe quelle API de client Redis, y compris `StackExchange.Redis`.

Installez le [package NuGet](https://www.nuget.org/packages/StackExchange.Redis) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a>Exemples

Cet exemple se connecte à une instance de la base de données de Cache Redis, ajoute des chaînes dans le cache par nom, puis les récupère à nouveau.

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

## <a name="management-library"></a>Bibliothèque de gestion

La bibliothèque de gestion de Cache Redis vous permet de gérer les ressources et les clés d’accès de Cache Redis .

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a>Exemples

Cet exemple crée un Cache Redis.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a>Exemples

* [Prise en main de Redis : Gérer Redis - dans .NET](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
