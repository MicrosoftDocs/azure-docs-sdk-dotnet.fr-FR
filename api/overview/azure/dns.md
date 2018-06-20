---
title: Bibliothèques Azure DNS pour .NET
description: Référence pour les bibliothèques DNS Azure pour .NET
keywords: Azure, .NET, SDK, API, DNS
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dns
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 34b50defa5f1524ab70c212b091f26016d59e81b
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487052"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="62bba-104">Bibliothèques Azure DNS pour .NET</span><span class="sxs-lookup"><span data-stu-id="62bba-104">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="62bba-105">Utilisez les bibliothèques Microsoft Azure DNS pour .NET pour créer et modifier des zones DNS et enregistrements hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="62bba-105">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="62bba-106">Des zones et enregistrements sont gérés en tant que ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="62bba-106">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="62bba-107">Pour en savoir plus, lisez la [vue d’ensemble de DNS Azure](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="62bba-107">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="62bba-108">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="62bba-108">Management library</span></span>

<span data-ttu-id="62bba-109">Utilisez la bibliothèque de gestion pour créer et modifier des zones DNS et les enregistrements hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="62bba-109">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="62bba-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="62bba-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="62bba-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62bba-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="62bba-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="62bba-112">Example</span></span>

<span data-ttu-id="62bba-113">L'exemple suivant crée une nouvelle zone DNS.</span><span class="sxs-lookup"><span data-stu-id="62bba-113">The following example creates a new DNS zone.</span></span>

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
> [<span data-ttu-id="62bba-114">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="62bba-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="62bba-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="62bba-115">Samples</span></span>

* [<span data-ttu-id="62bba-116">Exemple de projet de SDK Azure DNS .NET</span><span class="sxs-lookup"><span data-stu-id="62bba-116">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="62bba-117">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="62bba-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
