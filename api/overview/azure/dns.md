---
title: Bibliothèques Azure DNS pour .NET
description: Référence pour les bibliothèques DNS Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190192"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="6b0fe-103">Bibliothèques Azure DNS pour .NET</span><span class="sxs-lookup"><span data-stu-id="6b0fe-103">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="6b0fe-104">Utilisez les bibliothèques Microsoft Azure DNS pour .NET pour créer et modifier des zones DNS et enregistrements hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6b0fe-104">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="6b0fe-105">Des zones et enregistrements sont gérés en tant que ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6b0fe-105">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="6b0fe-106">Pour en savoir plus, lisez la [vue d’ensemble de DNS Azure](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="6b0fe-106">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="6b0fe-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="6b0fe-107">Management library</span></span>

<span data-ttu-id="6b0fe-108">Utilisez la bibliothèque de gestion pour créer et modifier des zones DNS et les enregistrements hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6b0fe-108">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="6b0fe-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6b0fe-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6b0fe-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b0fe-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="6b0fe-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="6b0fe-111">Example</span></span>

<span data-ttu-id="6b0fe-112">L'exemple suivant crée une nouvelle zone DNS.</span><span class="sxs-lookup"><span data-stu-id="6b0fe-112">The following example creates a new DNS zone.</span></span>

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b0fe-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6b0fe-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="6b0fe-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="6b0fe-114">Samples</span></span>

* [<span data-ttu-id="6b0fe-115">Exemple de projet de SDK Azure DNS .NET</span><span class="sxs-lookup"><span data-stu-id="6b0fe-115">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="6b0fe-116">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="6b0fe-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
